# dtbook-css
SASS for DTBooks.

Author: Jukka Eerikäinen 2015 jukka.eerikainen@aalto.fi

dtbook-css is a modular and extensible layout framework for DTBooks. dtbook-css is intended to be used both as the stylesheet for the end product and within the production toolchain.

dtbook-css is compatible with (at least) Oxygen XML editor (especially so when augmented with [dtBookTools](https://github.com/jukkae/dtBookTools)), Dolphin EasyReader / Internet Explorer 7, and modern WebKit/Gecko/Trident-based browsers. Modern browser support is not widely tested. There is preliminary support for mobile devices, but mobile support is not yet satisfactory.

dtbook-css is meant to be a long-term, one size fits all-type of solution for rapid production of DTBook.

## Usage

If you're just interested in using the CSS as is, download [dtbook.css](https://github.com/jukkae/dtbook-css/raw/master/dtbook.css).

## Downloading

If you want to edit the styles, you can download the project as a [zip](https://github.com/jukkae/dtbook-css/archive/master.zip).

## Building

~~The easiest way for users to build the project is probably with Sublime Text's sass-textmate-bundle.~~
You can build the project with [Notepad++](https://notepad-plus-plus.org/) with [jN](https://github.com/sieukrem/jn-npp-plugin) and [Sass-Auto-Compile](http://www.kuenzelit.de/blogContent/Sass-Auto-Compile.js). See https://deekaysblog.wordpress.com/2012/08/12/notepad-series-3-sass-highlighting-and-auto-compile/ for more info.

### Build system installation (for Windows)

#### Common steps

1. Install Ruby. Download [Ruby for Windows](http://rubyinstaller.org/downloads/) and install as Executable in PATH.
2. Install SASS. Open Start menu and type `cmd` and press enter. Type `gem install sass` and press enter.

#### Notepad++-based

3. Install Notepad++.
4. Install [jN](https://github.com/sieukrem/jn-npp-plugin/releases/download/2.0.179/jN_2.0.179.zip) plugin for Notepad++. (Download zip, unzip to Notepad++/plugins/.)
5. Copy [Sass-Auto-Compile.js](http://www.kuenzelit.de/blogContent/Sass-Auto-Compile.js) to Notepad++/plugins/jN/includes/.
6. Configure the script: set pathToRubyBin correctly; set debugMode = false;.
7. (Optional but highly recommended.) Configure syntax highlighting. Download http://www.kuenzelit.de/blogContent/sass-user-defined.xml and import in Notepad++ `View` -> `User defined language` -> `import`.

#### Sublime Text-based

3. Install [Sublime Text 2](http://www.sublimetext.com/2).
4. Install [Package Control](https://packagecontrol.io/installation) for Sublime Text.
5. Install SASS textmate bundle with Package Control. Click `Preferences` -> `Package Control` -> `Install Package` -> Type `sass` -> click on `Sass`. The description text is "Sass support for TextMate & Sublime Text (2 & 3)".
6. Install SASS Build with Package Control.
7. Restart Sublime Text.

### Building

#### In Notepad++

1. Just save `dtbook.scss`.

*Note:* Notepad++ does not give a confirmation when build is ready. It shouldn't take much longer than around five seconds, though.

#### In Sublime Text

1. Open `dtbook.scss` in Sublime Text.
2. `Tools` -> `Build` or `ctrl + B`

This builds the whole project into `dtbook.css` file in the same folder as `dtbook.scss`. Old version of `dtbook.css` is overwritten.

## Editing

The project is structured modularly. `dtbook.scss` is the main SASS project file that a) contains namespace declarations and b) imports all other files. `globals` folder contains a reset sheet, global variable definitions (for example, color scheming, fonts, margin and padding sizes and so on), global mixins (rounded corners) and so on. `globals` folder has no concrete declarations for any particular elements or classes. `oxygen` folder contains code required for Oxygen XML Editor author mode. `elements` folder contains concrete style rules for elements and some reusable templates bound to classes (see for example `_laatikko.scss`). Note that in concrete style rules the convention is to avoid usage of naked values (e.g. a particular color such as `#FFAAAA` or manually setting `margin: 2em;`). All such values shall be defined under `globals` and then reused by variable name. This helps to keep the code manageable and understandable, reduces code duplication and makes it possible to make big changes fast.

For more detailed information, see `HACKING.md` file.

## License

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.