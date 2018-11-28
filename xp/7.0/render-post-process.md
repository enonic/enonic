
# XP Server Rendering 

Rendering is the process of generating the HTML markup of a page, on the backend. It involves executing one or more JS controllers. 
The execution has multiple phases that may insert custom content in different parts of the target HTML document (content from parts, layouts, macros, page contributions).

## Rendering Post-Process

Post-Process is a part of the rendering that is executed for HTML content.

It is executed at the end of:
- **Page** rendering
- **Controller Mapping** rendering
- **Component** rendering
- **Exception** handler (site/error/error.js)

What Post process does:
1. Evaluates **Post Process Instructions**  
2. Evaluates **Response Processors** (aka Response Filters)
3. Evaluates **Page Contributions**


### Post Process Instructions
Currently there are 2 Post Process Instruction types:
- _Component instruction_: expands to render a component (Part or Layout)
- _Macro instruction_: expands to render a macro

Notes:
- Only done for GET requests
- Only if response body of type String

### Response Processors

Executes response-processor scripts found in all the applications of a Site.

Response processors are located in the app directory `src/main/resources/site/processors/<name>.js`

- The processors are executed in order. 
- Every processor receives the current Request and Response, and returns a new Response
- A processor can set `applyFilters` to false in its response to skip all other processors.

### Page Contributions

- Iterates over contributions that have been set in the Response object
- Page contributions can be added by: 
  + Page controller
  + Part controller
  + Layout controller
  + Response processors
- Injects contributions (strings) into 4 different points: 
  + headBegin: After the \<head> opening tag
  + headEnd: Before the \</head> closing tag
  + bodyBegin: After the \<body> opening tag
  + bodyEnd: Before the \</body> closing

Notes:
- Only done for GET requests
- Only if response `"Content Type: text/html"`
- Only if response body of type String

### Post-Process Steps by rendering type  

**Page**
1. Post process Instructions
2. Response processors
3. Page Contributions

**Mapping**
1. Post process Instructions
2. Response processors
3. Page Contributions

**Component**
1. Post process Instructions

**Error handler**
1. Post process Instructions
2. Page Contributions

## Response object property switches
- `postProcess` (default true) : If set to `false` it will skip Post process instructions and Page contributions
- `applyFilters` (default true) : If set to `false` it will skip Response-processors

## Component rendering

In order to render a page with components (parts and layouts) that are defined independently, 
the page controller generates HTML and in the position where the components should be placed it sets what we call *Post Process Instructions*. 

These instructions are just some special HTML tags that are recognized by the rendering engine. At a later stage in the rendering process, they are replaced with the desired content.

A Post Process Instruction is represented as an HTML comment element, where its tag body starts with a hash symbol # and the type of instruction. Currently there are 2 valid types: COMPONENT and MACRO. 

For example, this will indicate rendering of the component with path /main/0 :

```<!--#COMPONENT /main/0 -->```

Normally these component instructions will appear in Page and Layout HTML view files.

### Thymeleaf

The XP Thymeleaf library adds an extension to simplify component rendering. 

By setting the `data-portal-component` or `portal:component` attribute, it will generate the Post Process Instruction to render the component. 

These tags will be converted by Thymeleaf:

```<div data-portal-component="${component.path}" data-th-remove="tag" />```

```<div portal:component="${component.path}" data-th-remove="tag" />```

Into this (assuming component.path == '/main/0'):

```<!--#COMPONENT /main/0 -->```

### Mustache and other template engines

Mustache and other template engines do not have the built-in support that Thymeleaf has. In that case we should just add the HTML comment tag for the Post Process Instruction in the Mustache template: 

```<!--#COMPONENT {{path}} -->```
 
 
