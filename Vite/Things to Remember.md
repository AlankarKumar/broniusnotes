
* Any HTML file in your project root can be accessed directly by its respective directory path.
* - `<root>/index.html` -> `http://localhost:5173/`
- `<root>/about.html` -> `http://localhost:5173/about.html`
- `<root>/blog/index.html` -> `http://localhost:5173/blog/index.html`
- Assets referenced by HTML elements such as `<script type="module" src>` and `<link href>` are processed and bundled as part of the app.
- Importing `.css` files will inject its content to the page via a `<style>` tag with HMR support.
- Any CSS file ending with `.module.css` is considered a [CSS modules file](https://github.com/css-modules/css-modules). Importing such a file will return the corresponding module object:

```
import classes from './example.module.css'
document.getElementById('foo').className = classes.red
```

* CSS modules behavior can be configured via the [`css.modules` option](https://vite.dev/config/shared-options.html#css-modules).If `css.modules.localsConvention` is set to enable camelCase locals (e.g. `localsConvention: 'camelCaseOnly'`), you can also use named imports
```
// .apply-color -> applyColor
import { applyColor } from './example.module.css'
document.getElementById('foo').className = applyColor
```
* The automatic injection of CSS contents can be turned off via the `?inline` query parameter. In this case, the processed CSS string is returned as the module's default export as usual, but the styles aren't injected to the page.
```
import './foo.css' // will be injected into the page
import otherStyles from './bar.css?inline' // will not be injected
```
* Importing a static asset will return the resolved public URL when it is served:
```
// Explicitly load assets as URL
import assetAsURL from './asset.js?url'
// Load assets as strings
import assetAsString from './shader.glsl?raw'
// Load Web Workers
import Worker from './worker.js?worker'
// Web Workers inlined as base64 strings at build time
import InlineWorker from './worker.js?worker&inline'
```
* JSON: 
```
// import the entire object
import json from './example.json'
// import a root field as named exports - helps with tree-shaking!
import { field } from './example.json'
```
* Eager and Lazy Loading
	* https://vite.dev/guide/features.html#glob-import
* 