# Leading Systems LSCSS

## What is LSCSS?
LSCSS is a SASS/SCSS framework whose goal it is to standardize the general workflow typically used in
LS projects. Therefore, LSCSS takes care of the bootstrap and fontawesome integration and acts as the
central lynchpin for all styling purposes that other LS components (e.g. Merconis, LSJS etc.) can rely on.

## Getting started
After installing LSCSS, the LSCSS framework is located in assets/lscss.

***Please note:** The files in this directory must not be modified.*

Instead, you create your own custom scss file, include the LSCSS framework and do all your work here.

The custom scss file should be created in **files/lscss** and, in order to make the purpose of the file obvious, it should be named **lscss-project.scss**

In Contao, the extension "leadingsystems/contao-lscss4c" has to be installed in order to be able to
easily load lscss stylesheets. With this extension installed, you will find in the layout settings some
new fields under the headline "LSCSS". To load the lscss stylesheet, select it as "SCSS file to load".

The lscss-project.scss file should only contain a few imports:


```
@import "_variables.scss";

@import "../../assets/lscss/lscss.scss";

@import "_fonts.scss";

@import "_custom.scss";
```

The file lscss.scss contains the lscss framework itself. The other imports are project specific files which
technically are not mandatory but of course it makes sense to use them. Therefore, create the files
"_variables.scss", "_fonts.scss" and "_custom.scss" inside the same directory where lscss-project.scss
is located as well.

`_variables.scss` is the file in which you override variables defined in the LSCSS framework if necessary.
Of course, you can also define new variables.

***IMPORTANT**: In order to override the default lscss or bootstrap variables, it is mandatory to import
the custom variables file before importing lscss!*

`_fonts.scss` contains the @font-face rules for loading fonts

`_custom.scss` contains all the project specific styles, probably divided in multiple imports.

#### Using LSCSS and LSJS together
If you use the LSJS framework, you have to include the LSJS stylesheets like this:
```
[...]
@import "../../assets/lsjs/core/styles_core.scss";
[...]
```

#### Using LSCSS and Merconis together
If you use Merconis, you have to include the Merconis stylesheets like this:

```
[...]
@import "../../vendor/leadingsystems/contao-merconis/src/Resources/contao/lscss/_merconis.scss";
[...]
```

## How to use Font Awesome icons
LSCSS comes with Font Awesome already on board and ready to use.

Font Awesome can be used by placing `<i></i>` elements with specific classes like this:
```
<i class="fas fa-caret-up"></i>
```
It is also possible to use mixins and icon variables like this:
```
.some-element::before {
    @extend .fas;
    content: fa-content($fa-var-window-close);
}
```

## How to use LSCSS icons
LSCSS also comes with its very own icon set and it is possible to very easily add own icons using IcoMoon.

Using the built-in LSCSS icons basically works like using Font Awesome but with different class names
and mixin/variable names:

```
<i class="lsi lsi-payment-01"></i>
```
Any html element can become an icon by just adding the class "lsi" and then specifying
exactly which icon to use with one of the named icon classes (lsi-*)

LSCSS icons can also be used in scss files. The following example shows how to apply an icon
style to an html element using lsi mixins and variables in scss.
```
<h2>Lorem Ipsum</h2>
```
```
h2::before {
    @extend .lsi;
    content: $lsi-telescope-01;
}
```

#### Updating the LSCSS icon set in the LSCSS core
Of course, updating the icon set in the LSCSS core isn't something regular users would do
but this document should cover it anyway.

We created the icon set with icomoon.io which is a really great tool. The IcoMoon app can
be used without any license requirements when using own vectors. Using icon packs provided
by the IcoMoon library, however, requires the specific license requirements to be met.

###### Adding new icons to the icon set
In order to add new icons to the icon set it is important to begin by importing the existing
icon set into the IcoMoon app. The app has an import option which allows the `selection.json` file
to be imported. This file was automatically created during the previous export and should therefore be
included in the lscss-icons folder currently existing in LSCSS. By importing this file into the app
all meta data will already be imported and that's very important because only with exactly the
same meta data as before we can make sure that all variable names and class names etc. used
in LSCSS will still work with the updated icon set. **Warning:** IcoMoon allows svg files to be
imported as well and some meta data also exists in svg files but important meta data is missing
and therefore svg files must not be used to import the current icon set.

When the new icons have been added to the icon set in the IcoMoon app, the icon set must be
exported with the "generate font" option. Before downloading the generated font there is a
settings dialog which should already have all the right settings because they have also
been imported with the settings.json file.

For the sake of completeness, here are the important export settings:
- Font Name: lscss-icons
- Class Prefix: lsi-
- Include metadata in fonts: check
- Generate preprocessor variables for Sass
- CSS Selector - Use a class: .lsi
- The version should be increased accordingly

The exported file will be a zip file named like `lscss-icons-v1.0`. Extract the zip file and
rename the extracted folder into "lscss-icons" (removing the version information).

Then copy the folder "lscss-icons" with all its contents to the place where the previous version
of this folder lives inside LSCSS.

###### Using own icons on a project level without having to update the LSCSS core
Regular users don't update the icon set in the LSCSS core if they need new or modified
icons but instead they would add a copy of the icon set to their project level lscss folder.

1. Open the IcoMoon app and create a new icon set/selection
2. Export the icon set using the "generate font" option
3. Make sure to use the following export settings
    - Font Name: lscss-icons-custom
    - Class Prefix: lsi-custom-
    - Include metadata in fonts: check
    - Generate preprocessor variables for Sass
    - CSS Selector - Use a class: .lsi-custom
4. Download and extract the icon set and copy it into your project level lscss folder
(e.g. `files/merconisfiles/themes/theme10/lscss/lscss-icons-custom`)
5. Import the icon set stylesheet in `lscss-project.scss` with
`@import "lscss-icons-custom/style.scss";` directly below the import statement for the
LSCSS core
6. Open the file `variables.scss` and make the following modifications:
    - Rename the variable `$icomoon-font-family` to `$icomoon-font-family-custom`
    - Rename the variable `$icomoon-font-path` to `$icomoon-font-path-custom`
    - Set the correct font path which should look something like
    `$icomoon-font-path-custom: "/files/merconisfiles/themes/theme10/lscss/lscss-icons-custom/fonts" !default;`
7. Open the file `style.scss` and change the variable names there accordingly

Now you can use your project specific custom icons as follows:

```
<i class="lsi-custom lsi-custom-happy"></i>
```
```
h2::before {
    @extend .lsi-custom;
    content: $lsi-custom-happy;
}
```