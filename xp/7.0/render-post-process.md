
# Page rendering 

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

### Response Processors

Executes response-processor scripts found in all the applications of a Site.

Response processors are located in the app directory `src/main/resources/site/processors/<name>.js`

- The processors are executed in order. 
- Every processor receives the current Request and Response, and returns a new Response
- A processor can set `applyFilters` to false in its response to skip all other processors.

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
