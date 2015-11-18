# dtbook-css
SASS for DTBooks.

Author: Jukka Eerikäinen 2015 jukka.eerikainen@aalto.fi

License: TBD

dtbook-css is a modular and extensible layout framework for DTBooks. dtbook-css is intended to be used both as the stylesheet for the end product and within the production toolchain.

dtbook-css is compatible with (at least) Oxygen XML editor (especially so when augmented with [dtBookTools](https://github.com/jukkae/dtBookTools)), Dolphin EasyReader / Internet Explorer 7, and modern WebKit/Gecko/Trident-based browsers. Modern browser support is not widely tested. There is preliminary support for mobile devices, but mobile support is not yet satisfactory.

dtbook-css is meant to be a long-term, one size fits all-type of solution for rapid production of DTBook.

## Usage

If you're just interested in using the CSS as is, download [dtbook.css](https://github.com/jukkae/dtbook-css/raw/master/dtbook.css).

## Downloading

If you want to edit the CSS, you can download the project as a [zip](https://github.com/jukkae/dtbook-css/archive/master.zip).

## Building

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

The project is structured modularly. `dtbook.scss` is the main SASS project file that a) contains namespace declarations and b) imports all other files. `globals` folder contains a reset sheet, global variable definitions (for example, color scheming, fonts, margin and padding sizes and so on), global mixins (rounded corners) and so on. `globals` folder has no concrete declarations for any particular elements or classes. `oxygen` folder contains code required for Oxygen XML Editor author mode. `elements` folder contains concrete style rules for elements and some reusable templates bound to classes (see for example `_laatikko.scss`). Note that in concrete style rules the convention is to avoid usage of naked values (e.g. a particular color such as `#FFAAAA` or manually setting `margin: 2em;`). All such values shall be defined under `globals` and then reused by variable name. This helps to keep the code manageable and understandable, reduces code duplication and makes it possible to make big changes fast.

For more detailed information, see `HACKING.md` file.

## Known bugs

TBD

## Contributing

TBD