# HACKING

This file contains detailed breakdown of the project's structure.

## Main project file

The main project file is `dtbook.scss`. The main project file itself contains no rules. It only imports the other files that contain the actual style rules. It also has a namespace declaration for Oxygen. If new partials (files starting with `_` and containing rules) are added, they must be added to the partials import list. Everything under `global` must be imported in correct order (resets first, then variables and so on). Elements may be imported in any order; current convention is alphabetical ordering. Namespace declaration must not be altered; doing so will break Oxygen support.

## Globals

The `globals` folder contains global, reusable variables and definitions.

`_reset.scss` is a *reset stylesheet*. The basic idea of a reset stylesheet is to reduce inconsistencies between different browsers and layout engines. This is done by explicitly setting properties that may have different default values in different layout engines. For further discussion, see for example [Reset Reasoning](http://meyerweb.com/eric/thoughts/2007/04/18/reset-reasoning/). The current `_reset.scss` (as of Nov 2015) is very bare-bones. Edits will be required for proper mobile device support.

`_colors.scss` contains color definitions. See comments in the file itself. Two-tiered color management is *important*, so give it some time if it's not making sense at first.

`_variables.scss` contains general global variables, such as widths, line heights and letter spacings.

`_mixins.scss` contains general features and feature combinations, that may be used in multiple different contexts. For example, rounded corners may be used anywhere irrespective of the type and class of element that it's used on; vice versa, we might want some images to have rounded corners and others not, for example. This means that rounded corners is not bound to any single class or element type and is distinct from them.

`_margins.scss` contains margin definitions. Note again the two-tiered approach, somewhat similar to colors, but simpler.

`_borders.scss` contains border definitions. Once again, here we declare and define different types of borders that are then used on elements. Default color is supplied (see [Sass documentation](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)), but may be overridden.

`_paddings.scss` contains padding definitions. Similar to margins and borders.

`_fonts.scss` contains fonts. Note the use of font-related variables and default values.

## Elements

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

## Oxygen

The `oxygen` folder contains code that is only relevant to Oxygen.

`_oxygen.scss` has code for entities; this is required for WYSIWYG editing.