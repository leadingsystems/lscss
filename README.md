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
