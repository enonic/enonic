# Request Filters

Request filters will allow **intercepting HTTP requests** sent to XP, and adding custom logic to handle the request **with JavaScript code**.

## Background

Currently there are 3 alternatives to request filters that can be used in XP:

### Response filters

Existing XP [Response Filters](https://xp.readthedocs.io/en/stable/developer/site/filters.html) :

- They are limited to rendering of pages and controller mappings in portal.
- They are executed at the end of the HTTP processing in XP.
- They only work for site requests, the app containing the filter script needs to be configured for the site.
- They cannot modify the request or abort the HTTP processing in XP.

### Request filter with Java

It is possible to implement request filters using Java but it requires good knowledge of Java and how XP portal works.

Tine made a small app with something similar to a request filter with Java: https://github.com/tineikt/xp-app-requestfilter
Posten has created Java filters based on the app from Tine.

### Request filter in lib-router

Lib router has support for filters (same as in PurpleJS).

Lib router filters are JavaScript functions.

It is limited to the controller where it is used, normally main.js. It cannot intercept requests outside that base endpoint.

## Requirements

- Request filters are coded in JavaScript
- Request filters are defined in XP applications
- Request filters can intercept traffic to any HTTP endpoint in XP (?)
- Request filters can modify the request and response (HTTP headers and body)
- Request filters can skip the rest of the HTTP execution and send a response directly to the client

## Use cases

- Access control and authentication
- ...

## Implementation

- It can be implemented in XP as a WebHandler (like TraceWebFilter for example)
- WebRequest and WebResponse classes encapsulate HttpServletRequest and HttpServletResponse, making it easy to modify request and response in the HTTP chain.
- To support filtering for all endpoints in XP, it cannot depend on a site. That means that all the filters found in any installed apps should be put in a global registry. This is different than Response filters, which is based on Site resolving to find the apps that may apply.
- In principle the implementation does not require any API breaking changes
- The JavaScript function handler could follow the pattern of lib-router or PurpleJs: A function receives the request, the response, and the next handler. It can either return a new response or call the next handler and then return its response.

Example of JavaScript filter:

```Javascript
exports.filter = function (request, response, next) {
    if (!request.headers['X-Auth-Token'] === authToken) {

        return {            // skips other portal handlers
            status: 403
        }
    }

    request.headers['Authenticated'] = true;

    var nextResponse = next(request, response); // continue normal portal processing and get the response

    nextResponse.body = injectStuff(nextResponse.body);

    return nextResponse;
};
```

### Performance

- If the request filters are global, a bad implementation could make all the XP requests slow.
- The filters should be applied after TraceWebFilter, so that we can get some tracing info to debug performance issues.


## Notes

Feature request from Zendesk: https://enonic.zendesk.com/agent/tickets/2273
