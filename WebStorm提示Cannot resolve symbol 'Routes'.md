---
title: WebStorm提示Cannot resolve symbol 'Routes'
date: 2022-02-27 13:05:42
summary: 
categories: 
  - Error

tags:
  - solution
---

### WebStorm提示Cannot resolve symbol 'Routes'

#### Solution:

1. Inside the jetbrains product, press **shift two times** to open the search everywhere window, search for **registry** and open the first result.

2. In the registry, look for **typescript.external.type.defintions.packages** key and in the *value* of that field, **only remove** the **react-router-dom** field from the values.

3. Also **Delete** the react-router-dom package folder from this location, 

   > &lt;system directory&gt;/users/{name}/AppData/Local/jetbrains/intellij/javascript/typings

Now, the *jetbrains product* will **read the type file** from `node_modules` of project, rather than reading it from its `internal typings folder`. In the future, It will also **not try to download and use** the **intellij react-router-dom typings** for other projects.