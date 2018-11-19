# Implemented solution
See Page serialization implemented here: https://github.com/enonic/xp/issues/6697
Changes to JavaScript JSON serialization here: https://github.com/enonic/xp/issues/6652
----

# Flatten page structure

Currently the content page object is serialized as a tree structure when it is stored.
This tree structure makes it difficult to create search queries looking for values in components that are deeply nested.

To search for config value in a component, the query needs to specify a long property-tree path to the value, and only works for a expected location of the part in the page. If a component is moved to another region in the page, the query will not work anymore.

## Current tree structure

- There is one or more top regions in the page. 
- Components are nested inside regions.
- Layouts components contain regions, that again contain other components.

```json
{
  "page": {
    "region": {
      "name": "main",
      "component": [
        {
          "type": "PartComponent",
          "PartComponent": {
            "name": "Featured",
            "template": "com.enonic.app.superhero:featured",
            "config": {
            }
          }
        },
        {
          "type": "LayoutComponent",
          "LayoutComponent": {
            "name": "Two column",
            "template": "com.enonic.app.superhero:two-column",
            "config": {
            },
            "region": [
              {
                "name": "left",
                "component": {
                  "type": "PartComponent",
                  "PartComponent": {
                    "name": "Posts list",
                    "template": "com.enonic.app.superhero:posts-list",
                    "config": {
                    }
                  }
                }
              },
              {
                "name": "right",
                "component": [
                  {
                    "type": "PartComponent",
                    "PartComponent": {
                      "name": "Search form",
                      "template": "com.enonic.app.superhero:search-form",
                      "config": {
                      }
                    }
                  },
                  {
                    "type": "PartComponent",
                    "PartComponent": {
                      "name": "Categories",
                      "template": "com.enonic.app.superhero:categories",
                      "config": {
                        "showPostCount": false,
                        "showHierarchy": false
                      }
                    }
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  }
}
```

## Use cases

1. Search for content containing a specific component. _E.g. content contains part 'article-list'_
2. Search for content for which a specific component's config has a certain value. _E.g. content contains part 'article-list' with config 'showPostCount' = true_

## Solution

To simplify search page queries, and make them more predictable, the page should be flattened and serialized as an array or map of components.

The regions may also be included as an item in the array.
Each item object should include the path (ComponentPath or RegionPath).

### Proposal 1 - Flatten stored page as *array*, keep JS object as tree

- Serialize the page when storing, but keep the JS object as it is

```json
{
  "page": {
    "components": [
      {
        "path": "main",
        "type": "Region",
        "name": "main"
      },
      {
        "path": "main/0",
        "type": "PartComponent",
        "name": "Featured",
        "template": "com.enonic.app.superhero:featured",
        "config": {
        }
      },
      {
        "path": "main/1",
        "type": "LayoutComponent",
        "name": "Two column",
        "template": "com.enonic.app.superhero:two-column",
        "config": {
        }
      },
      {
        "path": "main/1/left",
        "type": "Region",
        "name": "left"
      },
      {
        "path": "main/1/left/0",
        "type": "PartComponent",
        "name": "Posts list",
        "template": "com.enonic.app.superhero:posts-list",
        "config": {
        }
      },
      {
        "path": "main/1/right",
        "type": "Region",
        "name": "right"
      },
      {
        "path": "main/1/right/0",
        "type": "PartComponent",
        "name": "Search form",
        "template": "com.enonic.app.superhero:search-form",
        "config": {
        }
      },
      {
        "path": "main/1/right/1",
        "type": "PartComponent",
        "name": "Categories",
        "template": "com.enonic.app.superhero:categories",
        "config": {
          "showPostCount": false,
          "showHierarchy": true
        }
      }
    ]
  }
}
```

Query examples:

- `page.components.template = 'com.enonic.app.superhero:categories'`
- `page.components.template = 'com.enonic.app.superhero:categories' AND page.components.config.showHierarchy = true` 

Pros:
- No need to make changes in JS code
- Possibility to use query functions. E.g:
+ `pageContains('com.enonic.app.superhero:categories')` 
+ `pageContainsConfig('com.enonic.app.superhero:categories', 'showHierarchy', 'true')` 

Cons:
- Mismatch between JS model and search model
- Not possible to query for e.g.: page has a specific component AND component contains config value 

### Proposal 2 - Flatten stored page as *object*, keep JS as tree

- Serialize the page when storing, but keep the JS object as it is
- Component name is not unique, so we need to use path as key 

```json
{
  "page": {
    "components": {
      "main": {
        "path": "main",
        "type": "Region",
        "name": "main"
      },
      "main/0": {
        "path": "main/0",
        "type": "PartComponent",
        "name": "Featured",
        "template": "com.enonic.app.superhero:featured",
        "config": {
        }
      },
      "main/1": {
        "path": "main/1",
        "type": "LayoutComponent",
        "name": "Two column",
        "template": "com.enonic.app.superhero:two-column",
        "config": {
        }
      },
      "main/1/left": {
        "path": "main/1/left",
        "type": "Region",
        "name": "left"
      },
      "main/1/left/0": {
        "path": "main/1/left/0",
        "type": "PartComponent",
        "name": "Posts list",
        "template": "com.enonic.app.superhero:posts-list",
        "config": {
        }
      },
      "main/1/right": {
        "path": "main/1/right",
        "type": "Region",
        "name": "right"
      },
      "main/1/right/0": {
        "path": "main/1/right/0",
        "type": "PartComponent",
        "name": "Search form",
        "template": "com.enonic.app.superhero:search-form",
        "config": {
        }
      },
      "main/1/right/1": {
        "path": "main/1/right/1",
        "type": "PartComponent",
        "name": "Categories",
        "template": "com.enonic.app.superhero:categories",
        "config": {
          "showPostCount": false,
          "showHierarchy": true
        }
      }
    }
  }
}
```

Pros:
- No need to make changes in JS code

Cons:
- Mismatch between JS model and search model
- Not possible to query for e.g.: page has a specific component AND component contains config value
- Queries require knowing the structure of the page, so no real improvement over current model 

### Proposal 3 - Flatten stored page and JS objects

- Serialize the page when storing, do the same for the JavaScript object.

```json
{
  "page": {
    "components": [
      {
        "path": "main",
        "type": "Region",
        "name": "main"
      },
      {
        "path": "main/0",
        "type": "PartComponent",
        "name": "Featured",
        "template": "com.enonic.app.superhero:featured",
        "config": {
        }
      },
      {
        "path": "main/1",
        "type": "LayoutComponent",
        "name": "Two column",
        "template": "com.enonic.app.superhero:two-column",
        "config": {
        }
      },
      {
        "path": "main/1/left",
        "type": "Region",
        "name": "left"
      },
      {
        "path": "main/1/left/0",
        "type": "PartComponent",
        "name": "Posts list",
        "template": "com.enonic.app.superhero:posts-list",
        "config": {
        }
      },
      {
        "path": "main/1/right",
        "type": "Region",
        "name": "right"
      },
      {
        "path": "main/1/right/0",
        "type": "PartComponent",
        "name": "Search form",
        "template": "com.enonic.app.superhero:search-form",
        "config": {
        }
      },
      {
        "path": "main/1/right/1",
        "type": "PartComponent",
        "name": "Categories",
        "template": "com.enonic.app.superhero:categories",
        "config": {
          "showPostCount": false,
          "showHierarchy": true
        }
      }
    ]
  }
}
```

Query examples:

- `page.components.template = 'com.enonic.app.superhero:categories'`
- `page.components.template = 'com.enonic.app.superhero:categories' AND page.components.config.showHierarchy = true` 

Pros:
- Unified model for JS and queries

Cons:
- Requires changes in JS controllers. Adding lib functions might help: getPageTree() getComponentTree()
- Not possible to query for e.g.: page has a specific component AND component contains config value

### Proposal 4 - Keep current format, add additional fields for searching

- Serialize the page as now. Add extra fields under "page" to allow searching for components.
- Aggregate configs of multiple components of the same type in the page

```json
{
  "page": {
    "configs": {
      "com-enonic-app-superhero_featured": {
      },
      "com-enonic-app-superhero_two-column": {
      },
      "com-enonic-app-superhero_posts-list": {
      },
      "com-enonic-app-superhero_search-form": {
      },
      "com-enonic-app-superhero_categories": {
        "showPostCount": false,
        "showHierarchy": false
      }
    },
    "components": [
      "com-enonic-app-superhero_featured",
      "com-enonic-app-superhero_two-column",
      "com-enonic-app-superhero_posts-list",
      "com-enonic-app-superhero_search-form",
      "com-enonic-app-superhero_categories"
    ],
    "region": {
      "name": "main",
      "component": [
        {
          "type": "PartComponent",
          "PartComponent": {
            "name": "Featured",
            "template": "com.enonic.app.superhero:featured",
            "config": {
            }
          }
        },
        {
          "type": "LayoutComponent",
          "LayoutComponent": {
            "name": "Two column",
            "template": "com.enonic.app.superhero:two-column",
            "config": {
            },
            "region": [
              {
                "name": "left",
                "component": {
                  "type": "PartComponent",
                  "PartComponent": {
                    "name": "Posts list",
                    "template": "com.enonic.app.superhero:posts-list",
                    "config": {
                    }
                  }
                }
              },
              {
                "name": "right",
                "component": [
                  {
                    "type": "PartComponent",
                    "PartComponent": {
                      "name": "Search form",
                      "template": "com.enonic.app.superhero:search-form",
                      "config": {
                      }
                    }
                  },
                  {
                    "type": "PartComponent",
                    "PartComponent": {
                      "name": "Categories",
                      "template": "com.enonic.app.superhero:categories",
                      "config": {
                        "showPostCount": false,
                        "showHierarchy": false
                      }
                    }
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  }
}
```

Query examples:

- `page.components.com-enonic-app-superhero_categories LIKE "*"` 
- `page.configs.com-enonic-app-superhero_categories.showHierarchy = true` 

Pros:
- No need to make changes in JS code
- Possible to query for: page has a specific component AND component contains config value

Cons:
- Mismatch between JS model and search model
- Not obvious query format, can be improved with query language functions 

