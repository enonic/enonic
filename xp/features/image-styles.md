

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



## Alignment styles

The following pre-defined classes will also be used by the editor, ships with xp by default
Developer has to implement these css styles on all sites in order for it to work properly live. The styles will be added to the `<figure>` element wrapping the image.

* editor-align-left
* editor-align-justify
* editor-align-center
* editor-align-right

The editor and image insert dialogue must refer to a standard css file in order to provide a preview when the styles are selected.


## Raw style

Some images need to be served without processing, i.e. Gif animations, svg's etc. For these cases, the user can choose the style "raw" from the dropdown list (optionally we suggest it automatically)

This style will essentially affect the url-generation, so that an attachementUrl will be created rather than an imageUrl.

The following style will be set to the figure element (possibly in addition to alignment styles)

* editor-raw

No css should be required in the editor or insert dialogue for editor-raw

# Custom image styles

Developers may add styles to their app, simply by adding a new file resources/site/styles.xml to their app.
Styles from multiple apps should be merged when working on a site. If in conflict, the highest sorted app wins if there are styles with same name.

When user choose an app-defined style from the list of image-styles, this is will be added to the figure element in addition to any alignment. i.e. class="editor-align-left widescreen"

The styles.xml file will be designed to support styles for both images and other element types (separate task)

```xml
<styles editor-css="assets/somefile.css">
	<style name="warning"> <!-- Example of generic non-image style -->
		<display-name>Warning</display-name>
	</style>
	<image name="cinema"><!-- Same name as CSS class -->
		<display-name>Cinema</display-name>
		<aspect-ratio>21:9</aspect-ratio>
		<filter>pixelate(10)</filter>
	</image>
	<image name="thumbnail"><!-- Same as CSS class -->
		<display-name>Thumbnail</display-name>
		<aspect-ratio>1:1</aspect-ratio>
	</image>
	<image name="bubble">
		<display-name>Bubble</display-name>
		<aspect-ratio>1:1</aspect-ratio>
	<image>
</styles>
```

The editor-css file can/should provide a css definition for each style in style.xml. These styles will be used by the editor and the insert dialogue. Specifically, the "cinema" style above would look like this:


```css
figure.cinema {background-color:#233333}
.warning {}
h1 {}
```

NB! The editor-css file will not be loaded when in inline mode (only style.xml will be used)

# Editor CSS

For each defined style, developers _may??_ implement an editor css, using the same name for their classes. 
This will be loaded into the insert dialogue and editor frame and must be tested extensively.

Questions:
- Are these figure styles or img styles for images? 
- What will determine which styles may be used for what elements in the editor? i.e. p.cool or img.thumbnail?


## User customized sizes

The user may optionally choose between automatic, actual and custom width for images. To store this information we will add the following classes


Sample with auto size
```
<figure class="editor-align-left editor-size-auto">
	<img src="image://c137bb3a-19ee-4cd4-bb7f-b3f34056ee71" />
	<figcaption>GraphQL request using a connection</figcaption>
</figure>
```

Sample with alignment, style and actual size
```
<figure class="editor-align-left bubble editor-size-actual">
	<img src="image://c137bb3a-19ee-4cd4-bb7f-b3f34056ee71" />
	<figcaption>GraphQL request using a connection</figcaption>
</figure>
```

Sample with custom size
```
<figure class="editor-align-left bubble editor-size-custom" style="width:70%">
	<img src="image://c137bb3a-19ee-4cd4-bb7f-b3f34056ee71" />
	<figcaption>GraphQL request using a connection</figcaption>
</figure>
```


## ImageService

IMPORTANT: Currently, admin uses a different image service than the portal, we must remove this and use the standard image service instead.

As styles are added to images, we can use this information when generating the server request URL:



Possible solutions:

* ProcessHTML must now be able to interpret the new styles.xml format and new figure classes.
* Insert dialogue must be able to generate a proper url for rendering images (through standard image service)
* Editor must be able to generate url to image service as well.

What is needed:
* A contextual max size
* DPR information if available
* The editor classes
* Optionally the custom size (to optimize the image generated even more, or maybe use contextual max size?)

In processHTML:
* Find figure element and extract known classes 8 predefined + custom styles in style.xml
* Find image element annd extract "key"
* New option for "server mode" vs "client mode", in server mode a max-width must be supported (defaults to 1024px)
* If DPR headers are available, consider using these to multiply max-width - (must also have option to disable this)
* Finally, after processing image data, it can call "imageUrl" to create a proper url.

If running in client-side (admin will need to use this approach)


* Add a new parameter to the imageService endpoint, "style" that will automatically lookup and apply the proper rendering to the image. Style will additionally need to know both width and dpr. We need to figure out if this is a parameter or url-path-thing.

* Add DPR support (maybe just use headers? What about override support?)

* The style could simply be handled on the url like we handle other scaling
image/71352714-39f2-42a9-a95a-4bf7d1d849e5:0ae184529474ab999a557105f464ab40ba241ff7/style-nnnn/image-name.jpg.jpeg?quality=90
NB! This will not work due to caching and CDN issues (if you change a style)


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
