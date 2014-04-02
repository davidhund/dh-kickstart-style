# dh-kickstart-style v0.1.0

A very opinionated OOCSS, boilerplate Sass (`.scss`) architecture for modern projects. I plan to use this as part of my `dh-kickstart` project boilerplate.

This is simply *my* opinionated CSS kickstarter for new projects. As most developers I find myself constantly re-inventing this kind of stuff. However awesome other people's projects are, I keep wanting to reinvent the wheel. Stupid, stubborn me ;)

So: this is mine. It's not finished, -very buggy etc. etc. Take a look and feel free to re-use parts of it. Also feel free to tell me where it could be improved.

## About

Most 'frameworks' use conventions I'm not 100% happy with, seem bloated, etc. So—as most stubborn developers do— I reinvent the weel. Don't judge: it's what I *like* and I *learn loads* from it :)

* **Modular**: uncomment in `/style.scss` what you don't need
* **Modern**: not much 'support' for oldIE and other older browsers
  * see `helpers/_settings.scss` though!
* **Opinionated**: see the **Notes** below

### Overview

- Uses Sass in .scss syntax
- [Normalize.css](https://github.com/necolas/normalize.css) v3.0.0 copied to `/src/imports/_normalize.scss`
- No prefixes! 
  - No mixins only for prefixes
  - Use something like [AutoPrefixer](https://github.com/ai/autoprefixer) for that.
- Uses `box-sizing` everywhere
- `rem()` mixin
  - Don't need a `px`-fallback for `rem`? Change `$rem-px` in `helpers/_settings.scss`
  -  (..and update `mixins/_rem.scss`)
- Not for everyone: just see what's helpful!

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

### Notes ("much 'opiniated', very personal")

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

## Using the `.scss` files

You could simply edit all the files (although—using Git—you'd get conflicts when pulling in updates).
Better is to `@import "dh-kickstart-style/scss/style";` in your `app.scss` or do the reverse and add all your *project specific* styles in the `dh-kickstart-style/scss/site/some-page.scss` or `dh-kickstart-style/scss/theme/some-theme.scss`.


## Thanks!

**Huge** kudo's to the great work of:

* [@csswizardry](http://twitter.com/csswizardry). His [@inuitcss framework](http://inuitcss.com/) is hands-down the best I know of. You should probably be using it!
* [@necolas](http://twitter.com/necolas). His [normalize.css](http://necolas.github.io/normalize.css/) is the *only* 'reset' you should be using
* [HTML5 Boilerplate](http://h5bp.com).  The world's best webdevelopers trying to work out the best defaults? I stole the *hell* out of all the goodies in there :)
* [@snook](http://twitter.com/snook). His [SMACSS](http://smacss.com) OOCSS approach is the one I (sorta) use, combined with a BEM classname convention.
