# dtbook-css
SASS for DTBooks.

dtbook-css is a modular and extensible layout framework for DTBooks. dtbook-css is intended to be used both as the stylesheet for the end product and within the production toolchain.

dtbook-css is compatible with (at least) Oxygen XML editor (especially so when augmented with [dtBookTools](https://github.com/jukkae/dtBookTools)), Dolphin EasyReader / Internet Explorer 7, and modern WebKit/Gecko/Trident-based browsers. Modern browser support is not widely tested. Furthermore, mobile devices support is not yet at a satisfying level.

dtbook-css is meant to be a long-term, one size fits all-type of solution for rapid production of DTBook.

## Tech & architecture
At heart, dtbook-css is basically your run-of-the-mill SASS project. Just build dtbook.scss with whatever you prefer.

The project structure is quite simple: directory oxygen contains everything directly related to only Oxygen XML editor; globals contains reset, mixins and variable definitions; and elements contain actual rules for styling content.

The project follows the same underlying principles as SMACSS/DRY/OOCSS, but it's not exactly any of those. Classes are only used when necessary. IDs are not used at all; IDs for styling are evil, and in DTBook, IDs are reserved for synchronization anyway. For an example of the principles, see http://denisejacobs.com/speaking/talks/scalable-modular-css-ftw/ - especially starting from slide 75.

Especially, the OOCSS principle of separating container and content is dismissed entirely, because the structure is rigid; furthermore, one of the key points of dtbook-css is to decrease production time by cutting usage of extraneous classes et cetera to a minimum.

SMACSS prefers subclassing; again, because we have a pre-determined structure, dtbook-css prefers descendant selectors. Furthermore, the naming conventions of SMACSS is ditched.

Colors are managed using two-tiered variable system containing both descriptive and functional colors, as per Sacha Greif: http://sachagreif.com/sass-color-variables/

Specially styled elements are defined by using template mixins; see for example _kehys.scss

Tables default to fixed layout. Auto can be specified by class="auto". NB.: Fixed layout is not correctly displayed in Oxygen.

A preliminary reset is included (globals/_reset.scss); this is very much a work in progress to be pursued further when starting to work on a) EPUB and b) mobile devices.

Because there's a need for synchronizing narrated / synthesized voice to the text, most of what would be \<ol> lists in vanilla html are actually pre-formatted lists. This means that for example exercise lists in textbooks must be marked up using a special structure. For the time being, see _lists.scss for the stylesheet.

The framework strives to cover most aspects of DTBooks. For the DTD for DTBook, see http://www.daisy.org/z3986/2005/dtbook/dtbookdoc.html
Furthermore, the framework supports additional classes that Celia - the Finnish library for the visually impaired use in their production of DTBooks. Given that DTBook standard sets strict boundaries on the possible structures of content, and that in-house DaisyTRIO production can be quite freely forced to adhere to standardification, building a somewhat rigid and normative framework suitable for all future needs is not only possible, but also beneficial.

In the future, the framework may be extended to cover EPUB3 as well.

## Build suggestions
The easiest way for users to build the project is probably with Sublime Text's sass-textmate-bundle.

### Build system installation

1. Install [Sublime Text 2](http://www.sublimetext.com/2).
2. Install Ruby. Download [Ruby for Windows](rubyinstaller.org/downloads) and install as Executable in PATH.
3. Install SASS. Open Start menu and type `cmd` and press enter. Type `gem install sass` and press enter.
4. Install [Package Control](https://packagecontrol.io/installation) for Sublime Text.
5. Install SASS textmate bundle with Package Control. Click `Preferences` -> `Package Control` -> `Install Package` -> Type `sass` -> click on `Sass`. The description text is "Sass support for TextMate & Sublime Text (2 & 3)".
6. Install SASS Build with Package Control.
7. Restart Sublime Text.

### Building

1. Open dtbook.scss in Sublime Text.
2. `Tools` -> `Build` or `ctrl + B`

This builds the whole project into `dtbook.css` file in the same folder as `dtbook.scss`.