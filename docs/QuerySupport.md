## Query Support

Support for parsing and serializing [URL queries](Terms.md#query) is provided by the `useQueries` [enhancer](Terms.md#createhistoryenhancer) function. Simply use a wrapped version of your `createHistory` function to create your `history` object and you'll have a parsed `location.query` object inside `listen` and `listenBefore` callbacks.

```js
import { createHistory, useQueries } from 'history'

// Use the built-in query parsing/serialization.
let history = useQueries(createHistory)()

// Use custom query parsing/serialization.
let history = useQueries(createHistory)({
  parseQueryString: function (queryString) {
    return qs.parse(queryString)
  },
  stringifyQuery: function (query) {
    return qs.stringify(query, { arrayFormat: 'brackets' })
  }
})

history.listen(function (location) {
  console.log(location.query)
})
```

Query-enhanced histories also accept URL queries as trailing arguments to `pushState`, `replaceState`, `createPath`, and `createHref`.

```js
history.createPath('/the/path', { the: 'query' })
history.pushState(null, '/the/path', { the: 'query' })
```
