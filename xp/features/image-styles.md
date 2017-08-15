

# Image Styles (Work In Progress)

This tasks aims to improve how images are inserted and styled using the HTML editor in XP. The main concept is to introduce styles. The styles concept is also relevant for the editor in general, but for images in particular this is more complex as there is also a server-side aspect we need to relate to.

Image styles will as such define a combination of client side CSS and server image rendering parameters.

# Editor image dialogue

Here are screenshots on how we imagine the actual new insert dialogue should appear. The alignment and style dropdown should be "similar" when working directly in the document. Meaning when an image is selected the image styles will be listed there too.

![](https://github.com/enonic/enonic/blob/master/xp/features/html-image-editor.001.jpeg) "Initial dialogue"

![](https://github.com/enonic/enonic/blob/master/xp/features/html-image-editor.002.jpeg) "After alignment"

![](https://github.com/enonic/enonic/blob/master/xp/features/html-image-editor.003.jpeg) "After style selection"

![](https://github.com/enonic/enonic/blob/master/xp/features/html-image-editor.004.jpeg) "Relative Width"

![](https://github.com/enonic/enonic/blob/master/xp/features/html-image-editor.005.jpeg) "Exact width"



# Custom image styles

Developers may add styles to their app, simply by adding a new file resources/site/styles.xml to their app.
Styles from multiple apps should be merged when working on a site. If in conflict, the highest sorted app wins if there are styles with same name.

The styles.xml file will be designed to support styles for both images and other element types


```xml
<styles editor-css="assets/somefile.css">
	<image name="cinema"><!-- Same name as CSS class -->
		<display-name>Cinema</display-name>
		<aspect-ratio>21:9</aspect-ratio>
		<size mode="auto|relative|*exact*">media.imageWidth?</width>
		<filter>pixelate(10)</filter>
	</image>
	<image name="thumbnail"><!-- Same as CSS class -->
		<display-name>Thumbnail</display-name>
		<aspect-ratio>1:1</aspect-ratio>
		<size mode="relative">20%</width>
	</image>
	<image name="bubble">
		<display-name>Bubble</display-name>
		<aspect-ratio>1:1</aspect-ratio>
	<image>
</styles>
```

# Editor CSS

For each defined style, developers _may??_ implement an editor css, using the same name for their classes. 
This will be loaded into the insert dialogue and editor frame and must be tested extensively.

Questions:
- Are these figure styles or img styles for images? 
- What will determine which styles may be used for what elements in the editor? i.e. p.cool or img.thumbnail?

# Standard image styles

XP currently ships with severand "standard styles" when it comes to images such as *widescreen*, *square* etc.

These should by default be available for all sites, and it is up to the user to implement the CSS for the actual site!
The standard styles can be considered part of the "site" app which will can be considered part of every site. In a similar way to how system content types are delivered.

We should probably use the "site" app to change settings such as disabling standard styles for instance!


## Alignment styles

The following pre-defined classes will also be used by the editor, ships with xp by default + developer has to implement this on all sites. This will be added to the `<figure>` element wrapping the image.

* editor-left
* editor-justify
* editor-center
* editor-right


When user choose an app-defined style from the list of image-styles, this is will be added to the figure element in addition to any alignment.


## User customized sizes

Users may customize the image size when deviating from "automatic/responsive" mode.
User can choose either "Relative" in percent, or exact size in PX. This setting will be stored as an inline style, effectively overriding any other classes etc.

```
<figure class="editor-left thumbnail|bubble|list|square" style="width:450px;">
	<img src="image://c137bb3a-19ee-4cd4-bb7f-b3f34056ee71" />
	<figcaption>GraphQL request using a connection</figcaption>
</figure>
```


## ImageService

As styles are added to images, we can use this information when generating the server request URL:

Possible solutions:

* Add a new parameter to the imageService endpoint, "style" that will automatically lookup and apply the proper rendering to the image. Style will additionally need to know both width and dpr. We need to figure out if this is a parameter or url-path-thing.

* Add DPR support (maybe just use headers? What about override support?)

* The style could simply be handled on the url like we handle other scaling
image/71352714-39f2-42a9-a95a-4bf7d1d849e5:0ae184529474ab999a557105f464ab40ba241ff7/style-nnnn/image-name.jpg.jpeg?quality=90

Hmm.. how will this affect custom croppings? Ban mixing of styles og custom cropping effects?

## ProcessHTML

* Needs a new optional parameter to set default "width" in px when processing markup. This can be used to set a default image size for simple server-side image size handling. This is currently hard-coded in processHTML (may be an issue with text component and imageComponent?)

* Add a new parameter, to specify "client-side" mode vs "server-side" mode. If invoked with client-side mode, it will simply create an image placeholder, and pass settings as @data-image attributes?? on the element. This mode will require the developer to add a "renderImage" or similar javascript on the pages, that will automatically find and replace all placeholders with proper images.

* Need to figure out if there should be a "site wide" setting for this stuff, or if it is on a per-app basis? Would be cool if one could register a clientImageRenderer somewhere, and that htmlProcessor would understand this somehow?

## Editor handling

When alignment, styles and custom settings are chosen in the editor, these will be stored as classes, and inline styles.
NB! We need to consider if the style should also be stored directly on the image url or not?


## Backwards compatibility
### Migration from XP 6.x if needed?
- Implement an upgrade model that processes content nodes
- Look for String fields in content data that contain "img" tags with "image://" URL
- Set attributes in figure style attribute according to what was set in 6.x.

### Migration from CMS - cms2xp
- Create image style descriptors that match the functionality in CMS (scaling + CSS)
- Include those styles in the generated app that comes out of the export
- Convert the HtmlArea during export using the new image styles
