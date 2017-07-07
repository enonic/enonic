# Image Styles (WIP)

Image styles define a combination of client side CSS and server image generation parameters.

# Custom image styles

Developers may add styles to their app, simply by adding a new file resources/site/image.xml to his app.
Styles from multiple apps should be merged, where the highest sorted app wins if there are styles with same name.


```xml
<image>
	<styles editor-css="assets/somefile.css">
		<style name="cinema"><!-- Same as CSS class -->
			<display-name>Cinema</display-name>
			<aspect-ratio>21:9</aspect-ratio>
			<size mode="auto|relative|*exact*">media.imageWidth?</width>
			<filter>pixelate(10)</filter>
		</style>
		<style name="thumbnail"><!-- Same as CSS class -->
			<display-name>Thumbnail</display-name>
			<aspect-ratio>1:1</aspect-ratio>
			<size mode="relative">20%</width>
		</style>
		<style name="bubble">
			<display-name>Bubble</display-name>
			<aspect-ratio>1:1</aspect-ratio>
		<style>
	</styles>
</image>
```

For each defined style, developers _may_ implement an editor css, using the same name. 
This will be loaded into the insert dialogue and editor frame and must be tested extensively.


# Standard image styles

We need to define standard image styles such as *widescreen*, *square* etc.
These are placed in "system" app, similar to how system content types are delivered.


## Alignment styles

Use the following pre-defined classes for use by editor, ships with xp by default + developer has to implement this on all sites.

* image-left
* image-justify
* image-center
* image-right


When user choose an app-defined style from the list of image-styles, this is also added to the figure element.

If user chooses "advanced" and toggles the various settings, the following classes are added to the markup.


## User customized sizes

Users may customize the image size when deviating from "automatic" mode.
User can choose either "Relative" in percent, or exact size in PX. This setting will be stored as an inline style, effectively overriding any other classes etc.


## ImageService

To simplify how styles are understood and handled, we can update the 

* Add a new parameter??? to the imageService endpoint, "style" that will automatically lookup and apply the proper rendering to the image. Style will additionally need to know both width and dpr. Need to figure out if this is a parameter or url-path-thing.
* Add DPR support (maybe just use headers? override support?)

## ProcessHTML

* Needs a new parameter to set default "width" in px when processing markup. This can be used to set a default image size for simple server-side image size handling. This is currently hard-coded in processHTML (may be an issue with text component and imageComponent?)

* Needs a new parameter, to specify "client-side" rendered mode vs "server-side" render mode. If invoked with client-side mode, it will simply create a imagePlaceholder, and pass settings as data-image?? on the element. This mode will require the developer to add a "renderImage" or similar javascript on the pages, that will automatically find and replace all placeholder with proper images.


## Backwards compatibility
### Migration from XP 6.x if needed?
- Implement an upgrade model that processes content nodes
- Look for String fields in content data that contain "img" tags with "image://" URL
- Set attributes in figure style attribute according to what was set in 6.x.

### Migration from CMS - cms2xp
- Create image style descriptors that match the functionality in CMS (scaling + CSS)
- Include those styles in the generated app that comes out of the export
- Convert the HtmlArea during export using the new image styles
