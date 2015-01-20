# dtbook-css
SASS for DTBooks.

dtbook-css is a modular and extensible layout framework for DTBooks. dtbook-css is intended to be used both as the stylesheet for the end product and within the production toolchain.

dtbook-css is compatible with (at least) Oxygen XML editor (especially so when augmented with dtbooktools), Dolphin EasyReader / Internet Explorer 7, and modern WebKit/Gecko/Trident-based browsers. Modern browser support is not widely tested. Furthermore, mobile devices support is not yet at a satisfying level.

dtbook-css is meant to be a long-term, one size fits all-type of solution for rapid production of DTBook.

# Tech & architecture
At heart, dtbook-css is basically your run-of-the-mill SASS project. Just build dtbook.scss with whatever you prefer.

The project structure is quite simple: directory oxygen contains everything directly related to only Oxygen XML editor; globals contains reset, mixins and variable definitions; and elements contain actual rules for styling content.

Colors are managed using two-tiered variable system containing both descriptive and functional colors, as per Sacha Greif: http://sachagreif.com/sass-color-variables/

Specially styled elements are defined by using template mixins; see for example _kehys.scss

The framework strives to cover most aspects of DTBooks. For the DTD for DTBook, see http://www.daisy.org/z3986/2005/dtbook/dtbookdoc.html
Furthermore, the framework supports additional classes that Celia - the Finnish library for the visually impaired use in their production of DTBooks. Given that DTBook standard sets strict boundaries on the possible structures of content, and that in-house DaisyTRIO production can be quite freely forced to adhere to standardification, building a somewhat rigid and normative framework suitable for all future needs is not only possible, but also beneficial.

In the future, the framework will be extended to cover EPUB3 as well.