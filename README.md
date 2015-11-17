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

## Editing

### Main project file

The main project file is `dtbook.scss`. The main project file itself contains no rules. It only imports the other files that contain the actual style rules. It also has a namespace declaration for Oxygen. If new partials (files starting with `_` and containing rules) are added, they must be added to the partials import list. Everything under `global` must be imported in correct order (resets first, then variables and so on). Elements may be imported in any order; current convention is alphabetical ordering. Namespace declaration must not be altered; doing so will break Oxygen support.

### Globals

The `globals` folder contains global, reusable variables and definitions.

`_reset.scss` is a *reset stylesheet*. The basic idea of a reset stylesheet is to reduce inconsistencies between different browsers and layout engines. This is done by explicitly setting properties that may have different default values in different layout engines. For further discussion, see for example [Reset Reasoning](http://meyerweb.com/eric/thoughts/2007/04/18/reset-reasoning/). The current `_reset.scss` (as of Nov 2015) is very bare-bones. Edits will be required for proper mobile device support.

`_colors.scss` contains color definitions. See comments in the file itself. Two-tiered color management is *important*, so give it some time if it's not making sense at first.

`_variables.scss` contains general global variables, such as widths, line heights and letter spacings.

`_mixins.scss` contains general features and feature combinations, that may be used in multiple different contexts. For example, rounded corners may be used anywhere irrespective of the type and class of element that it's used on; vice versa, we might want some images to have rounded corners and others not, for example. This means that rounded corners is not bound to any single class or element type and is distinct from them.

`_margins.scss` contains margin definitions. Note again the two-tiered approach, somewhat similar to colors, but simpler.

`_borders.scss` contains border definitions. Once again, here we declare and define different types of borders that are then used on elements. Default color is supplied (see [Sass documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)), but may be overridden.

`_paddings.scss` contains padding definitions. Similar to margins and borders.

`_fonts.scss` contains fonts. Note the use of font-related variables and default values.

### Elements

The `elements` folder contains concrete element definitions.

`_blocks.scss` contains miscellaneous blocks, most of which are quite uncommon. For example, prodnotes, sidebars and poems.

`_bookbody.scss` contains rules concerning the base layout of the book. For example, content width, gutters, and some dtBook-specific elements such as docauthor. Also contains basic layout rules for smaller screens.

`_breaks.scss` contains rules for horizontal rules (no pun intended) and line breaks. Note that `<hr>` color is set here. `<br>` rules are necessary for Oxygen support.

`_exercises.scss` contains rules for exercises. See the file for in-depth commentary. Here be dragons, proceed with extreme caution.

`_headings.scss` contains headings. For example, heading sizes and margins are set here.

`_images.scss` contains rules for images and imggroups. Note that images by default have rounded corners set; this only works in modern browsers. Line 18 makes Oxygen display the actual image in editor.

`_inlines.scss` contains rules for miscellaneous inline elements, such as `<a>`s (links), `<em>`s and `<strong>`s and so on. Also contains some code related to sentences on small screens.

`_kehys.scss` is interesting. It contains the rules for "kehys" custom class. Note especially the use of template (with default color) and passing of color from concrete .kehys1 - .kehys3 classes. The template is basically an abstract template that can be reused for different colors. It's, for example, possible to add new colors by simply writing `.kehys4 { @include kehys( #FF0000 ); }`. Note, however, that this simple example violates the color management system. Better'd be `.kehys4 { @include kehys( $my-dandy-new-color ); }`, where `$my-dandy-new-color` would be defined in `_colors.scss`. Margins, et cetera, for "kehys" are also controlled here.

`_laatikko.scss` works pretty much in the same way as `_kehys.scss`. Note the curious selectors and nested structure in the template: Everything that's actually inside a `laatikko` in dtBook is also inside a `laatikko` in sass as well.

`_lists.scss` has rules for lists. Also some preliminary support for small screens.

`_navs.scss` has rules for navigation headers.

`_p.scss` has rules for `<p>` elements. Currently also has rules for two alternative classes.

`_pagenums.scss` has rules for page numbers.

`_pohja.scss` is quite similar to `_laatikko.scss` and `_kehys.scss`. Note underlining of headings.

`_tables.scss` contains rules for tables. For example, table colors are set here. Some very preliminary small screen support. Proper small screen support requires redesign.

### Oxygen

The `oxygen` folder contains code that is only relevant to Oxygen.

`_oxygen.scss` has code for entities; this is required for WYSIWYG editing.