# testCompassGemImportOverride

This project is just a simple default compass project built to test the ability to override sass libraries from already installed gems.

## Conclusion:

My theory was correct, any *partial* file located in the local directory will overide any sass files which would otherwise be imported from an installed gem.

## Proof:

Steps to create test:

    compass create --sass-dir "scss" --css-dir "css" --javascripts-dir "js" --images-dir "img"
    cd scss
    touch _compass.scss
    vim _compass.scss

Paste this into _compass.scss:

    body {
      background: red;
    }

Contents of screen.scss:

    /* Welcome to Compass.
     * In this file you should write your main styles. (or centralize your imports)
     * Import this file using the following HTML or equivalent:
     * <link href="/stylesheets/screen.css" media="screen, projection" rel="stylesheet" type="text/css" /> */

    @import "compass";

## After Compass compile:

Contents of screen.css

    /* Welcome to Compass.
     * In this file you should write your main styles. (or centralize your imports)
     * Import this file using the following HTML or equivalent:
     * <link href="/stylesheets/screen.css" media="screen, projection" rel="stylesheet" type="text/css" /> */
    /* line 1, ../scss/_compass.scss */
    body {
      background: red;
    }
