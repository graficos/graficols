# @graficos/graficols

## Motivation
I turned this [gist](https://gist.github.com/gangsthub/8b497cd315864c28464ec0c435d04b87)
into a library (my first one ever) because I use variations of the same in several projects.


## What it includes

- There's a defined list of column (will be percetages):

```
// note the ellipsis is for explanation purposes only
$G_CONTAINER_WIDTHS: (5, 10, 20..., 50, ..., 100)
```

- A set of breackpoints:

```
$G_WINDOW_DIMENSIONS: (
    // edit / add BPs as you please
    sm: '(max-width: 64em)',
    md: '(min-width: 64.01em) and (max-width: 87.99em)',
    xl: '(min-width: 88em)',
);
```

- The actual mixin `gGenerateCols` wich is the one you will use on your scss.

## Usage

1. Installation

    ```
    npm i @graficos/graficols
    ```

2. Import the scss file. Depending on your environment or bundling system, you might have a defined way of doing
this. Examples:
  - Import in an Angular project: [link](https://github.com/angular/angular-cli/issues/2269#issuecomment-320126603)
  - In Nuxt.js: [link](https://nuxtjs.org/api/configuration-css)
  - Using Webpack and adding an alias: [link](https://github.com/webpack/webpack/issues/1789#issuecomment-250983832)
  - Using Parcel: [link](https://github.com/parcel-bundler/parcel/issues/1800)
  - In a Vanilla project:
    - Add a `.sassrc` file in your root directory with the following content:
    ```
    {
      "includePaths": ["node_modules"]
    }
    ```

    - Then, you can `@import` from your SCSS files using `~`:

    ```
    @import "~@graficos/graficols/graficols";
    // ... use the mixin here :)
    ```


3. Re-define the collections (`G_CONTAINER_WIDTHS` and `$G_WINDOW_DIMENSIONS`) if you please.

4. `@include` the mixin like so:

```
// with no @media queries
@include gGenerateCols(null);
// -> will create dynamic classes: min-w50p, max-w50p, w50p, push50p, pull50p

// with media queries
@each $mediaName, $mediaValue in $G_WINDOW_DIMENSIONS {
  @media #{ $mediaValue } {
    @include gGenerateCols($mediaName);
  }
}
// -> will create: (tailwind style) xl:min-w50p (using the keys from $G_WINDOW_DIMENSIONS as class prefixes)
```

## Recommendation

It is recommended to use [https://www.purgecss.com](https://www.purgecss.com) along with this library because
most of the generated css classes will not be used in production, most likely.


