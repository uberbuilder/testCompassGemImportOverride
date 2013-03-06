# testCompassGemImportOverride

This project is just a simple default compass project built to test the ability to override sass libraries from already installed gems, or from an additionaly added import path using the `add_import_path` function.

## Conclusion:

Updated README.md, configured Compass project, and added the necessary files with only the needed content to perform the test.
My theory was correct, any *partial* file located in the local directory will overide any sass files which would otherwise be imported from an installed gem.

## Important Note:

When using the `add_import_path` function it is important to understand that this does not work like the other configuration variables.  This is not a variable you are setting, you're actually calling a function - not setting a variable. see config.rb


## This is what I did to test the theory:

    compass create --sass-dir "scss" --css-dir "css" --javascripts-dir "js" --images-dir "img"
    cd scss
    touch _compass.scss
    vim _compass.scss

Paste this into _compass.scss:

    body {
      background: red;
    }

## To test additional import paths:

First Steps:

    cd ~/Sites/
    mkdir uberBuilderCommon
    vim _uberTest.scss

Contents of `_uberTest.scss`:

    .uberBuilderClass {
      color: red;
    }

Add an additional scss partial to test to make sure it won't get imported due to a local partial stored in the local project `./scss` path:

    vim _overRideMe.scss

Content of `_overRideMe.scss` (in the new additional import path which we've added to the config.rb):

    .thisClassShouldNotMakeItToTheCSSFile {
      color: orange;
    }

Went back to project scss directory and added `_overRideMe.scss`

    cd ~/Sites/testCompassGemImportOverride
    vim _overRideMe.scss

Content of additional `_overRideMe.scss` in the local project `./scss` path:

    .thisUberTestIsBeingLocallyOverRidden {
      color: blue;
    }

Contents of screen.scss:

    /* Welcome to Compass.
     * In this file you should write your main styles. (or centralize your imports)
     * Import this file using the following HTML or equivalent:
     * <link href="/stylesheets/screen.css" media="screen, projection" rel="stylesheet" type="text/css" /> */

    @import "compass";
    @import "uberTest";
    @import "overRideMe";

## After Compass Compile:

Contents of screen.css

    /* Welcome to Compass.
     * In this file you should write your main styles. (or centralize your imports)
     * Import this file using the following HTML or equivalent:
     * <link href="/stylesheets/screen.css" media="screen, projection" rel="stylesheet" type="text/css" /> */
    /* line 1, ../scss/_compass.scss */
    body {
      background: red;
    }

    /* line 1, ../../uberBuilderCommon/_uberTest.scss */
    .uberBuilderClass {
      color: red;
    }

    /* line 1, ../scss/_overRideMe.scss */
    .thisUberTestIsBeingLocallyOverRidden {
      color: blue;
    }

## Note:

I have copied the contents of the uberBuilderCommon to the directory `./additionalImportPath` to make it easy for you to perform your own test on your own system.

I am running `Mac OS X 10.7.5` using `ruby-1.9.3-p194` and `Sass 3.2.5 (Media Mark)` with `Compass 0.12.2 (Alnilam)`

This test was last performed: `2013-03-06 16:06:33`