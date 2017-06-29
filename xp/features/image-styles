# Image Styles (WIP)

## Image Style Descriptors
- Located in a new directory in the app for image styles: **/site/images/**
- One folder per image style, similar to other descriptors (parts, pages, layouts, macros)
- The descriptors are loaded when the app is installed (same as parts,etc).
- We can specify CSS classes either inline in XML, or point to a CSS file and a class name
- Refering to CSS file should work for LESS & SASS because their compiled result is included in the app (point to compiled CSS instead of source SASS)

Example: /site/images/portrait/portrait.xml

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

- What XP will keep in memory for the styles is a list of CSS attribute-value pairs, no matter where they come from (file or inline). And a class name.
- We can specify different sets of CSS styles for: admin, live, preview?

### Alternative: Single file for all image styles (@bwe)
- Instead of one xml file per image style, have a common images.xml at the same level as site.xml
- There could be a <images> wrapping all the <image> elements

## Admin Editor
For showing the styles in Admin Html Editor we need:
- REST resource that return list of image styles, for dropdown selection
- REST resource that returns image style descriptor as JSON, including list of CSS styles
- The REST requests take the descriptors from the apps installed based on the current site context 
- When an image style is selected:
  - Option A: the CSS styles are added to the img tag
  - Option B: the `class` is added as an attribute to the img element, and the styles loaded in the Editor frame.
- If there are CSS styles inlined for admin preview, they should be removed when saving
- 2 possible ways to store the image style in the HTML
  - Option A: add parameter to image://<id> URL -> `image://a76ec725-b7f9-45dd-8ffd-e173476535e5?style=portrait`
  - Option B: add data attribute to img tag:  ```<img src="image://a76ec725-b7f9-45dd-8ffd-e173476535e5" data-xp-img-style="portrait"/>```

### Custom styles
- The user can in addition to select an existing image style, select "Custom" and specify properties in detail
- The selected CSS styles will be set in a data attribute in the image element, when saving. 
- E.g. `<img data-xp-img-custom="width: 100%; float: left;" ...`

## Portal Rendering
- For rendering, `processHtml` will take care of generating the right imageUrl and adding CSS styles
- The imageUrl generation is basically as it works now
- In addition, based on the image style name, it will add inline CSS styles or set the class specified in the descriptor in the `<img/>` tag
- If custom attributes have been set, they will be moved from the `data-xp-img-custom` attribute to `styles` in the img element.

## Backwards compatibility
### Migration from XP 6.x
- Implement an upgrade model that processes content nodes
- Look for String fields in content data that contain "img" tags with "image://" URL
- Move attributes from style to custom data attribute

### Migration from CMS - cms2xp
- Create image style descriptors that match the functionality in CMS (scaling + CSS)
- Include those styles in the generated app that comes out of the export
- Convert the HtmlArea during export using the new image styles
