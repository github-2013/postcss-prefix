# postcss-prefix


> Prefix every CSS selector with a custom namespace `.a => .prefix`

## Table of Contents

- [Install](#install)
- [Usage with PostCSS](#usage-with-postcss)
- [Usage with Webpack](#usage-with-webpack)
- [Usage with Vite](#usage-with-vite)
- [Options](#options)
- [Maintainer](#maintainer)
- [Contribute](#contribute)
- [License](#license)

## Install

```console
$ npm install postcss-prefix
```

## Usage with PostCSS

```js
const prefixer = require('postcss-prefix')

// css to be processed
const css = fs.readFileSync("input.css", "utf8")

const out = postcss().use(prefixer({
  prefix: '.some-selector',
})).process(css).css
```

Using the options above and the CSS below...

```css
.c {
  color: coral;
}
```

You will get the following output

```css
.some-selector {
  color: coral;
}
```

## Usage with webpack

Use it like you'd use any other PostCSS plugin. If you also have `autoprefixer` in your webpack config then make sure that `postcss-prefix-selector` is called first. This is needed to avoid running the prefixer twice on both standard selectors and vendor specific ones (ex: `@keyframes` and `@webkit-keyframes`).

```js
module: {
  rules: [{
    test: /\.css$/,
    use: [
      require.resolve('style-loader'),
      require.resolve('css-loader'),
      {
        loader: require.resolve('postcss-loader'),
        options: {
          postcssOptions: {
            plugins: {
              "postcss-prefix": {
                prefix: '.some-prefix',
              },
              autoprefixer: {
                browsers: ['last 4 versions']
              }
            }
          }
        }
      }
    ]
  }]
}
```


## Usage with Vite

Following the same way of Webpack but for Vite:

```js
import prefixer from 'postcss-prefix';
import autoprefixer from 'autoprefixer';

...

export default defineConfig({
...
  css: {
    postcss: {
      plugins: [
        prefixer({
          prefix: '.some-prefix',
        }),
        autoprefixer({}) // add options if needed
      ],
    }
  },
...
});  
```

## Options

| Name | Type | Description |
|-|-|-|
| `prefix` | `string` | This string is added before every CSS selector |