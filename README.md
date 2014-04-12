# dh-kickstart-style v0.1.0

**An design-free, modular OOCSS Sass 3.3 (`.scss`) architecture for *modern* projects. Part of my [dh-kickstart](https://github.com/davidhund/dh-kickstart) project boilerplate.**

As most developers I find myself constantly re-inventing this kind of stuff. However awesome other people's projects are, I keep wanting to reinvent the wheel. This is simply *my* opinionated CSS kickstarter for new projects. Stubborn me ;)

So anyway: this is mine. It's not finished. There will be bugs etc. etc. Take a look and feel free to re-use parts of it. Also feel free to tell me where it could be improved.

* [About](#user-content-about)
 * [Overview](#user-content-overview)
 * [Naming conventions](#user-content-naming-conventions)
* [Notes](#user-content-notes)
* [Install / Use](#user-content-install--use)
* [Thanks](#user-content-thanks)

## About

Most 'frameworks' use conventions I'm not 100% happy with and seem bloated for my use-case. So I reinvent the weel. Don't judge: it's what I *like* and I *learn loads* from it :)

* **Modular**: uncomment in `/style.scss` what you don't need (but that'd not be much…)
* **Modern**: Keepin' it lean: no kb's 'supporting' oldIE etc. 
  * Take a look at `helpers/_settings.scss` though!
* **Design-Free**: structural styles mainly. Very little design to override.
* **'Opinionated'**: build on *my* experience in CSS Architecture. See the [Notes](#user-content-notes) below

### Overview

- **Sass 3.3** `.scss`
- [Modular architecture](#user-content-folder-structure) based on SMACSS (and others)  
..with only **one** file (`style.scss`) that compiles to CSS
- Collection of modular, responsive, OOCSS Components
  - Stand-alone objects e.g: `/components/_media.scss`
     - Easily en/disable them in `/style.scss`
  - Mobile-First
  - Structural Styles 'only'. Little to no 'design' to override
- [Normalize.css v3.0.0](https://github.com/necolas/normalize.css)
- No prefixes! 
  - I use [AutoPrefixer](https://github.com/ai/autoprefixer) for that. So should you…
  - Ditch all these (outdated) mixins-for-prefixes
- Uses `box-sizing` everywhere. Yes: ancient IE got this right…
- `rem()` mixin with `px` fallback for *layout*
  - Don't need a `px`-fallback for `rem`? Change `$rem-px` in `helpers/_settings.scss`  
  ..and update `mixins/_rem.scss`


### Naming conventions

I try to adhere to a generic [OOCSS](http://oocss.org) approach. Much inspiration from (and many thanks to) [SMACSS](http://smacss.com), [BEM](http://bem.info), [INUIT CSS](http://inuitcss.com/)

#### Classnames

* **Component:** `.component-name` -› `.media`
* **Sub-object:** `.component-name__sub-object` -› `.media__img`
* **Modifier:** `.component-name__sub-object--modifier` -› `.media__img--reversed`
* **State:** `.is-some-state` -› `.is-active`, `.is-hidden`
* **Layout helpers:** `.l-helper` -› `.l-float-left`, `.l-1of2`

Grid- and grit units are the exception: no prefix there: `.grid` and `.grid__unit`

I'm on the fence re: Javascript selectors. I like to use `data-` attr. for these but one could also use `.js-` prefixed classnames. As long as it's consistent.

#### Sass Variables

Most Sass variables are prefixed so that one knows what type to expect:

* `$cl-*` **Color value:** * `$cl-black`, `$cl-accent`, `$cl-link-hover`
* `$ff-*` **Font family value:** * `$ff-body`, `$ff-headings`
* `$fs-*` **Font size value:** * `$fs-base-px`, `$fs-base-pc`
* `$ln-*` **Line- value (height:unitless):** * `$ln-height`
* `$pd-*` **Padding value:** * `$pd-default`
* `$mg-*` **Margin value:** * `$mg-default`
* `$bd-*` **Border value:** * `$bd-radius`
* `$mq-*` **Media Query:** * `$mq-narrow`, `$mq-medium`, `$mq-wide`

Colors are both named after their *color* (`$cl-grey`) and after their *use* (`$cl-border`). This allows us to do:

````
$cl-grey: #CCC;       // No need to remember #CCC
$cl-border: $cl-grey; // .. but using $cl-border in components
````

#### Folder Structure

```
dh-kickstart-style/
|- style.scss                // ONLY compiled CSS. @imports all the rest
|- helpers/
|    |- _settings.scss
|    |- _functions.scss
|    |- _mixins.scss
|    |- _utils.scss          // imported after Base
|- base/
|    |- _normalize.scss
|    |- _webfonts.scss
|    |- _doc.scss
|    |- _hyperlinks.scss
|    |- _type.scss
|    |- _lists.scss
|    |- _images.scss
|    |- _tables.scss
|    |- _forms.scss
|    |- ...
|- layout/
|    |- _grids.scss
|    |- _general.scss
|    |- ...
|- components/
|    |- _logo.scss
|    |- _nav.scss
|    |- _nav--breadcrumbs.scss
|    |- _nav--pagination.scss
|    |- _nav--tabs.scss
|    |- _nav--keywords.scss
|    |- _list-stacked.scss
|    |- _linklist.scss
|    |- _boxed.scss
|    |- _media.scss
|    |- _figure.scss
|    |- _message.scss
|    |- _btn.scss
|    |- _btn-social.scss     // Experimental: adds SVG data uri icons. Increases file-size considerably
|    |- _meta.scss
|    |- ...
|- site/
|    |- _home.scss           // Page-specific styles for <PROJECT>
|    |- ...
|- themes/
|    |- _theme-XYZ.scss      // Site-specific theme for <PROJECT>
|    |- ...
|- extra/
|    |- _XYZ.scss            // Specific styles for extra (vendor?) styles
|    |- ...
|- _mediaqueries.scss
|- (_print.scss)             // [Optional] Using @media print {...} in style.scss at the moment.

```

## Notes 

> "much 'opiniated', very personal"

- IE9 is not (actively) _supported_ but should work for 90%
- CSS Object _Modifiers_ are **added** to the HTML: so no `btn, btn--cta {...}` and then `class="btn--cta"` but use both classes. Define `btn {...} btn--cta { ..extra styles.. }` and use as `class="btn btn--cta"`
  - **.. but this can be changed** in `settings.scss` with: `$modifiers-extend:true`!
- No prefixes! Use something like [AutoPrefixer](https://github.com/ai/autoprefixer)
- `@extend` as first rule in selector..
- Since we use the default of `100%` for `font-size` on the `html` element, we do not need to _redefine_ it on all other elements. Because of this there are little or no issues with compounding `em` values, etc.
  - In other words: KISS: just _only_ define font-sizes where you explicitely need them (headings?), and if so: use `em`.
- padding that should be closely linked to font-size (such as padding in buttons) should be in `em`, otherwise `rem`
- margins (+grid-reset-font) however, are mostly(!) in `rem`s (with `px` fallback in `rem()`)
- vertical margins in One Direction only (thanks @csswizardry). I only use `margin-bottom`
- unitless `line-height` (`line-height: 1.4;`)
- layout-sizes in % (`.l-col { width: 50%; } `)


### Not 100% my own

I've taken (inspiration/code) from *lots* of different places. While I adapted most code for my needs, some stuff is blatantly copied (I tried to make sure that was allowed though ;)) - See the *THANKS* section below.

## Install / Use

You could simply download and unzip the files, clone the repository in a clean project or use it as a Git submodule


### Download and unzip

Download and Unzip from: https://github.com/davidhund/dh-kickstart-style/archive/master.zip


### Clone the Github repository

Given the following project structure:

````
| my-project/
|-- scss/
  |-- dh-kickstart-style/ # ‹- Should go here
  '-- app.scss
|-- css/
  '-- app.min.css
'-- index.html
````
You would like to clone the repository in a subfolder of `scss/` named `dh-kickstart-style` so you do:

````
cd my-project
git clone git@github.com:davidhund/dh-kickstart-style.git scss/dh-kickstart-style
````

### Use as a Git submodule

Given the project structure above:

````
cd my-project
git submodule add git@github.com:davidhund/dh-kickstart-style.git scss/dh-kickstart-style
````

### Using the `.scss` files

You could simply edit all the files (although—using Git—you'd get conflicts when pulling in updates).
Better is to `@import "dh-kickstart-style/style";` in your `app.scss` or do the reverse and add all your *project specific* styles in the `dh-kickstart-style/site/some-page.scss` or `dh-kickstart-style/theme/some-theme.scss`.


## Thanks!

**Huge** kudo's to the great work of:

* [@csswizardry](http://twitter.com/csswizardry). His [@inuitcss framework](http://inuitcss.com/) is hands-down the best I know of. You should probably be using it!
* [@necolas](http://twitter.com/necolas). His [normalize.css](http://necolas.github.io/normalize.css/) is the *only* 'reset' you should be using
* [HTML5 Boilerplate](http://h5bp.com).  The world's best webdevelopers trying to work out the best defaults? I stole the *hell* out of all the goodies in there :)
* [@snook](http://twitter.com/snook). His [SMACSS](http://smacss.com) OOCSS approach is the one I (sorta) use, combined with a BEM classname convention.
