# Image Styles (WIP)


Create definitions for server side image generation, and use same name for css style.

```xml
<image-styles editor-css="assets/somefile.css">
	<style name="thumbnail"><!-- Same as CSS class -->
		<display-name>Thumbnail</display-name>
		<scale>block(400,500)</scale><!-- Only mandatory config -->
		<quality>85</quality><!-- Only applies to jpg -->
		<format>jpg</format>
	</style>
	<style name="portrait">
		<display-name>Portrait</display-name>
		<scale relative="true">widescren</scale><!-- Only mandatory config -->
		<quality>85</quality><!-- Only applies to jpg -->
		<format>jpg</format>
	<style>
</image-styles>
```


Use the following pre-defined classes for use by editor

* image-left
* image-justify
* image-center
* image-right


When user choose an app-defined style from the list of image-styles, this is also added to the figure element.

If user chooses "advanced" and toggles the various settings, the following classes are added to the markup.

image-scale-xx
image-scale-widescreen
etc


For custom adjustments to image size in px or %

image-size-original
image-size-custom???

Finally, store width adjustments inline as absolute or relative i.e. width: 80% or 321px


- Need to support client vs server side processHtml() with optional width parameter


## Image Style Descriptors
- Located in a new directory in the app for image styles: **/site/images/**
- One folder per image style, similar to other descriptors (parts, pages, layouts, macros)
- The descriptors are loaded when the app is installed (same as parts,etc).
- The CSS is specified by pointing to a CSS file and a class name
- Refering to CSS file should work for LESS & SASS because their compiled result is included in the app (point to compiled CSS instead of source SASS)

Examples: /site/images/portrait/portrait.xml

```xml
<image>
  <display-name>Portrait</display-name>
  <description>Portrait image</description>

  <scaling>
    <width size="100"/>
  </scaling>
  
  <css src="/assets/css/portrait.css" class="myapp-portrait-img"/>
 
  <format type="jpeg" quality="90"/>
  <effects>
    <grayscale/>
  </effects>
</image>
```

Discarded alternative:
```xml
<image>
  <display-name>Portrait</display-name>
  <description>Portrait image</description>
  
  <cropping>
    <block width="21" height="9"/>
  </cropping>
  
  <scaling>
    <width size="100"/>
  </scaling>
  
  <css>
    <style scope="admin">
      width: 60%;
      border-radius: 50%;
    </style>
    <style scope="live" src="/assets/css/portrait.css" class="myapp-portrait-img"/>
  </css>
  
  <format type="jpeg" quality="90"/>
  <effects>
    <grayscale/>
  </effects>
</image>
```

- What XP will keep in memory for the styles is a list of CSS attribute-value pairs and a class name (not the whole css file).
- ~~We can specify different sets of CSS styles for: admin, live, preview?~~

### Alternative: Single file for all image styles (@bwe)
- Instead of one xml file per image style, have a common images.xml at the same level as site.xml
- There could be a `<images>` wrapping all the `<image>` elements
- This would allow us to add other config files in future for other things.
- This doesn't introduce yet another set of folders, or multiple files to look through.
- Alternative: collect all these configs in a `/site/config/` location, each xml with a logic name. Like editor.xml, images.xml, components.xml, responsive.xml ... and so on. Whatever might come up in the future.
- Also, I strongly suggest to leave everything about classes and css out for now, rather introduce this in the future editor config where you can add classes to editor (tinyMCE). An image config can add one or more classes to the figure element, but that's it. Styling in admin is not changed, only thing that is visual is that the image get correct cropping/scaling. Additional css for round corners and such is left out, only visible in preview/live. At a later stage custom styles inside admin can be introduced, but then we are in more need of that setting on text, headings, and links etc, not images. So feels odd to fix it for images now but not the other things. So I vote strongly for a separation. Images now, styles in admin later - and then we fix it for all elements - p, div, img, whatnot.

If it was configured in the same file, it could look something like this. TIghtly coupled with the portal.imageUrl function:

```xml
<image-formats>
	<format name="thumbnails"><!-- Programatic name -->
		<display-name>Thumbnail</display-name>
		<config>
			<scale>block(400,500)</scale><!-- Only mandatory config -->
			<quality>85</quality><!-- Only applies to jpg -->
			<format>jpg</format>
			<type>absolute</type><!-- Generate absolute or server relative URLs in processHtml - HOWEVER, maybe not let image config control this at all since we do that in processHtml call? -->
			<!-- setting for background-color ... who needs that when we have CSS? Same with "filter". Could be skipped and implemented if demaned for it comes up -->
			<!-- Future addition is to here define a class name from some CSS file that will be used inside Image Wizard and TinyMCE. This is (2) and we could live without it on first implementation. However we already now need to add the class when processHtml runs. -->
			<css-class>myClass</css-class><!-- This will add .myClass to the list of classes on the figure element when inserting -->
		</config>
	</format>
	<format name="portrait"><!-- Another example with less settings-->
		<display-name>Portrait</display-name>
		<config>
			<scale>width(640)</scale>
			<css-class>portraits</css-class><!-- Do we perhaps need to think about being able to add multiple classes? -->
		</config>
</image-formats>
```

## Admin Editor
For showing the styles in Admin Html Editor we need:
- REST resource that return list of image styles, for dropdown selection
- REST resource that returns image style descriptor as JSON, including list of CSS styles
- The REST requests take the descriptors from the apps installed based on the current site context 
- When an image style is selected:
  - ~~Option A: the CSS styles are added to the img tag~~
  - Option B: the `class` is added as an attribute to the figure element, and the styles loaded in the Editor frame.
- 2 possible ways to store the image style in the HTML
  - Option A: add parameter to image://<id> URL -> `image://a76ec725-b7f9-45dd-8ffd-e173476535e5?style=portrait`
  - Option B: add data attribute to img tag:  ```<img src="image://a76ec725-b7f9-45dd-8ffd-e173476535e5" data-xp-img-style="portrait"/>```

### Custom styles
- The user can in addition select an existing image style, select "Custom" and specify properties in detail
- The selected CSS styles will be set in the standard `style` attribute in the figure element. 
- E.g. `<figure style="width: 100%; float: left;" ...`

## Portal Rendering
- For rendering, `processHtml` will take care of generating the right imageUrl and adding CSS styles
- The imageUrl generation is basically as it works now
- In addition, based on the image style name, it will add inline CSS styles or set the class specified in the descriptor in the `<img/>` tag
- If custom attributes have been set in the figure element they will be left untouched. Other custom changes (e.g. scaling parameter) will be applied.

## Backwards compatibility
### Migration from XP 6.x
- Implement an upgrade model that processes content nodes
- Look for String fields in content data that contain "img" tags with "image://" URL
- Set attributes in figure style attribute according to what was set in 6.x.

### Migration from CMS - cms2xp
- Create image style descriptors that match the functionality in CMS (scaling + CSS)
- Include those styles in the generated app that comes out of the export
- Convert the HtmlArea during export using the new image styles
