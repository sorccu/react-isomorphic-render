6.0.0 / 11.10.2016
===================

  * Removed `redux-devtools` from the list of dependencies
  * (breaking change) renamed `development_tools` to `devtools`, and it's now not just a React component but an object of shape `{ component, persistState }`
  * (breaking change) renamed `load_translation` to `translation`
  * (breaking change) renamed `on_error` to `catch` in server-side options
  * (breaking change) renamed `preload.on_error` option to `preload.catch`

5.0.9 / 11.10.2016
===================

  * Implemented a workaround for missing redirect parameters `react-router` bug

5.0.7 / 10.10.2016
===================

  * Fixed `redirectLocation.search === undefined` being appended to redirect URLs

5.0.5 / 05.10.2016
===================

  * Added common `history` options (e.g. for setting `basename`)

5.0.4 / 01.10.2016
===================

  * Parsing dates in error JSON objects too

5.0.2 / 11.09.2016
===================

  * Fixed `on_navigation` is not a function bug
  * All `@preload()`s are now blocking; removed the exported `Preload_blocking_method_name`
  * Added `onEnter(({ dispatch, getState }, redirect) => {})(component)` decorator to mimic `react-router`'s `onEnter` hook

5.0.1 / 10.09.2016
===================

  * Fixed `dispatch()` and `getState()` throwing errors in `onEnter` hooks

5.0.0 / 10.09.2016
===================

  * (breaking change) `@preload()` now takes a JSON object with named parameters: `dispatch`, `getState`, `location`, `parameters` and also everything from an optional `preload.helpers` object
  * (breaking change) Renamed `on_preload_error` to `preload.on_error`
  * Added support for `react-router` `onUpdate` handler: a common `on_navigate` function

4.1.10 / 10.09.2016
===================

  * Added `http.url` common option which replaces the default `format_url()` function if specified
  * Renamed `http_request` to `http.request`

4.1.9 / 10.09.2016
===================

  * Added `normalize_common_options` to page server's `render()`

4.1.7 / 08.09.2016
===================

  * Fixed `action is not defined` error when calling `store.getState()` inside `routes()`

4.1.5 / 08.09.2016
===================

  * `assets()` function now has the second argument which is `{ store }`; this can be used, for example, to show different favicons for different users.

4.1.4 / 02.09.2016
===================

  * `development_tools` option is now not a `true` flag but rather a `DevTools` instance created by `crateDevTools()` function call. This way one can customize the tools however he likes. See https://github.com/halt-hammerzeit/react-isomorphic-render#miscellaneous-client-side-rendering-options

4.1.3 / 27.08.2016
===================

  * Fixing `Date` parsing

4.1.2 / 20.08.2016
===================

  * Slightly changed the behaviour of the undocumented `event` parameter of `asynchronous_middleware`: now it transforms `event` into an array of `[event: pending, event: done, event: failed]` as opposed to the older colonless `[event pending, event done, event failed]`. This could break things for those who were using this undocumented feature, but an easy hotfix is to provide `promise_event_naming` function parameter in `common.js` to retain the old Redux event naming scheme:

```js
promise_event_naming(event_name)
{
  return [`${event_name} pending`, `${event_name} done`, `${event_name} failed`]
}
```

4.1.0 / 17.08.2016
===================

  * (a slight possibility of a breaking change) `http` utility now emits `Failure` Redux event with the `error` different from what it was in `4.0.x`: it used to be the raw `Error` javascript object, and now it is an error data object containing `{ status: 403, message: 'Unauthorized' }` and all other values returned as part of the HTTP response JSON body. The reasoning behind this change is that the `error` from the `Failure` Redux event payload is usually immediately stored in Redux state tree in the corresponding reducer, and since Redux state tree should only contain plain (pure) javascript objects, then it makes sence to store only the useful properties there instead of the whole instance of an `Error` class which is not a plain (pure) javascript object (and, therefore, is not serializable, which is not a functional programming approach).

4.0.40 / 15.08.2016
===================

  * Small fix for Redux `<DevTools/>` extension

4.0.37 / 01.08.2016
===================

  * Fixed `redirect` and `goto` not working from `asynchronous_middleware` failure event dispatch handler

4.0.36 / 31.07.2016
===================

  * Added a dedicated HTTP status code `204` handler to `http` utility

4.0.35 / 28.07.2016
===================

  * Fixed `asynchronous_middleware` events not being dispatched through user-defined middleware

4.0.31 / 27.07.2016
===================

  * Fixed `create_routes`: it now takes `store` as a parameter

4.0.30 / 27.07.2016
===================

  * Fixed user supplied middleware not being able to `goto` or `redirect`

4.0.27 / 27.07.2016
===================

  * `render` on client now also returns `component` and `store` along with `rerender`

4.0.23 / 27.07.2016
===================

  * Added support for asynchronous `react-router` routes for Redux renderer

4.0.22 / 23.07.2016
===================

  * `localize` bug fix

4.0.16 / 22.07.2016
===================

  * Extracted `page-server` rendering into a separate `async` (returns Promise) function `render` (see readme for arguments and return values)

4.0.15 / 22.07.2016
===================

  * Added `secure` option to `page-server`

4.0.13 / 21.07.2016
===================

  * Constrained `http` utility URLs to internal ones only to prevent sensitive data leakage (e.g. HTTP cookies)

4.0.11 / 20.07.2016
===================

  * Removed server-side `development` option. Using `process.env.NODE_ENV` now.

4.0.10 / 20.07.2016
===================

  * Migrated from Koa v1 to Koa v2
  * Added `middleware` option for possible Koa application extension
  * Bumped `superagent` version (1.x -> 2.x)
  * Fixed `preload` function `request` parameter: it was a Koa request, now it's Node.js request
  * Fixed `clone_request` parameter of `http_client`: it was a Koa request, now it's Node.js request

4.0.9 / 19.07.2016
===================

  * Fixed `PUT` and `PATCH` `http` requests not sending data via POST

4.0.8 / 19.07.2016
===================

  * Added second parameter to `preload` server-side function. The added parameter is an object having a `request` property which can be used, for example, to read a cookie into Redux store.

4.0.7 / 19.07.2016
===================

  * Added second parameter for `http` utility customization function, which holds the `store`

4.0.6 / 18.07.2016
===================

  * Added `http_request` parameter for `http` utility adjustment

4.0.5 / 18.07.2016
===================

  * Added support for supplying custom HTTP headers to `http` utility

4.0.4 / 18.07.2016
===================

  * @adailey14 Fixed a bug of `redux_middleware` not working on server-side

4.0.0 / 05.07.2016
===================

  * Renamed `markup_wrapper` to `wrapper`
  * Now takes `reducer` parameter instead of `create_store`
  * Now takes `routes` parameter instead of `create_routes`
  * Many other API changes (mostly refactoring)

3.0.4 / 04.07.2016
===================

  * Refactoring
  * `<div id="react_markup"/>` -> `<div id="react"/>`
  * Fixed `redux-devtools`

3.0.0 / 29.05.2016
===================

  * Migrated from `react-document-meta` to `react-helmet` (nothing special). Breaking changes: `meta` is now a `react-helmet` `meta` array, and the `head()` function now takes only two parameters - `title` and `meta` - therefore omitting `description` parameter.


2.1.31 / 27.04.2016
===================

  * Fixed infinite looping page freeze when navigating to the same `<Route/>`

2.1.29 / 09.04.2016
===================

  * Migrated to react-router 2

2.1.22 / 01.03.2016
===================

  * Added support for `Date`s in Redux state

2.1.21 / 29.02.2016
===================

  * Fixed occasional "Invariant Violation: `mapStateToProps` must return an object. Instead received [object Promise]" Redux error

2.1.12 / 08.02.2016
===================

  * Added `@preload()`ing events for preload status indication

2.1.10 / 04.02.2016
===================

  * Optimized `@preload()`ing for top level components

2.1.6 / 03.02.2016
==================

  * Added `on_preload_error` error handler for client side rendering (used for 401 and 403 redirects, for example)

2.1.4 / 02.02.2016
==================

  * Added `on_error` error handler (used for 401 and 403 redirects, for example)

2.1.0 / 22.01.2016
==================

  * Now correctly manages Http Cookies (allows for cookie modification on server-side)
  * Added blocking preload methods for Reat-Routed Components

2.0.0 / 19.01.2016
==================

  * changed `markup_wrapper` from a function to a React component
  * internationalization messages are now not passed from server to client but are instead loaded during client-side rendering (to allow for Hot Module Replacement aka hot reload)
  * extensive refactoring and some minor features added

1.4.1 / 07.01.2016
==================

  * can now use `Promise`s returned from Redux dispatched actions

1.4.0 / 03.01.2016
==================

  * changed `body` function a bit
  * removed `to` from client-side rendering function parameters

1.2.0 / 26.12.2015
==================

  * changed `preload` arguments order

1.2.0 / 26.12.2015
==================

  * simplified website "favicon" insertion into <head/>
  * `styles` parameter renamed to `style`

1.1.0 / 26.12.2015
==================

  * `create_routes` is now required on server-side too
  * `create_store` simplifed

1.0.2 / 25.12.2015
==================

  * API refactoring

1.0.0 / 24.12.2015
==================

  * Initial release