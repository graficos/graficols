# @graficos/graficols

## Motivation
I turned this [gist](https://gist.github.com/gangsthub/8b497cd315864c28464ec0c435d04b87)
into a library (my first one ever) because I use variations of the same in several projects.


## What it includes

- There's a defined list of column (will be percetages):

```
// note the ellipsis is for explanation purposes only
$CONTAINER-WIDTH: (5, 10, 20..., 50, ..., 100)
```

- A set of breackpoints:

```
$WINDOW-DIMENSIONS: (
    // edit / add BPs as you please
    sm: '(max-width: 64em)',
    md: '(min-width: 64.01em) and (max-width: 87.99em)',
    xl: '(min-width: 88em)',
);
```

- The actual mixin `generateCols` wich is the one you will use on your scss.

## Usage

1. Import the scss file
  1.1 Re-define the collections (`$CONTAINER-WIDTH` and `$WINDOW-DIMENSIONS`) if you want.
2. `@include` the mixins like so:

```
// with no @media queries
@include generateCols(null);
// -> will create dynamic classes: min-w50p, max-w50p, w50p, push50p, pull50p

// with media queries
@each $mediaName, $mediaValue in $WINDOW-DIMENSIONS {
  @media #{ $mediaValue } {
    @include generateCols($mediaName);
  }
}
// -> will create: xl:min-w50p (using the keys from $WINDOW-DIMENSIONS as class prefixes)
```

## Recommendation

It is recommended to use [https://www.purgecss.com](https://www.purgecss.com) along with this library because
most of the generated css classes will not be used in production, most likely.


