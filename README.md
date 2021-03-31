# fast-sass

A SASS compiler plugin focussed on speed over customisability. Initially forked from [ember-cli-sass](https://github.com/adopted-ember-addons/ember-cli-sass) then rewritten taking much inspiration from [ember-cli-typescript](https://github.com/typed-ember/ember-cli-typescript/) to allow the addon to be written in TypeScript

fast-sass uses [Sass][] to preprocess your ember-cli app's styles, and provides support for source maps and include paths. It provides support for the common use case for Ember.js projects:

[Sass]: https://sass-lang.com/

## Installation

```
ember install fast-sass
```

Next you'll need to rename `styles/app.css` to `styles/app.scss`.

### Usage

This addon uses a distribution of [Dart Sass][] that is compiled to pure JavaScript. Dart Sass is the reference implementation for Sass.

[Dart Sass]: https://sass-lang.com/dart-sass

By default this addon will compile `app/styles/app.scss` into `dist/assets/app.css`.

If you want more control, you can pass additional options to `sassOptions`:

- `includePaths`: an array of include paths
- `onlyIncluded`: true/false whether to use only what is in `app/styles` and `includePaths`. This may helps with performance, particularly when using NPM linked modules
- `ext`: The file extension of the input file, default: `'scss'`


## Example

The following example assumes your this party packages are installed as `node_modules`.

Make the files from that dependence available to SASS like this:

```shell
yarn add -D foundation-sites
```

Specify some include paths in your `ember-cli-build.js`:

```javascript
var app = new EmberApp({
  sassOptions: {
    includePaths: [
      'node_modules/foundation-sites/scss',
    ]
  }
});
```

Import some deps into your app.scss:

```scss
@import 'foundation';
@include foundation-global-styles;
```

## Automatic Pod Style Inclusions

If you want to follow a pattern of having style files for each individual component, you can have them automatically included by passing this option in `ember-cli-build.js`.

```ts
var app = new EmberApp({
  sassOptions: {
    autoIncludeComponentCSS: true
  }
});
```

You *must* also add this to your `app.scss`

```scss
@import 'pod-styles';
```

With this done, any `scss` file found in `app/components/**` will be automatically included in the build output.
