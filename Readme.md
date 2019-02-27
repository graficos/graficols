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

1. Import the scss file (depending on your environment or bundling system)

1. Re-define the collections (`G_CONTAINER_WIDTHS` and `$G_WINDOW_DIMENSIONS`) if you want.

1. `@include` the mixin like so:

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


