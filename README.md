Inline SVG
==========

Generates CSS (or Less CSS) file with embeded SVG icons. No SVG fragments = IE 11 should work fine.

> The only dependency is PHP. It's much faster for me to write terminal script than Shell scripts…

*Prerequisites:*

- Monochrome icons, with single color fills and/or strokes
- No optimisations — optimise before runnig (SVGo, Image Optim app,…)
- Encoded without Base 64 to safe some bytes

*Caveat:*\
To be able to use different colour icons, every color variation needs to be
included in the final CSS.

Less mixins by default have 2 parameters:
- `@fill` — no default value, needs to be specified when calling mixin
- `@stroke` — `transparent` by default

See `--template` option for details.

About
-----

Inspired by: https://github.com/tigt/mini-svg-data-uri/blob/master/index.js

Read more:
- https://codepen.io/tigt/post/optimizing-svgs-in-data-uris
- https://css-tricks.com/probably-dont-base64-svg/

---

Install using composer
----------------------

```json
{
    "name": "you/example-project",
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/attitude/inline-svg"
        }
    ],
    "require": {
        "attitude/inline-svg": "dev-main"
    }
}
```

Usage
-----

```shell
$ composer inline-svg [options]
```

or when cloned directrly:

```shell
$ ./inline-svg dir/with/svgs/ output.file [options]
```

### Example:

```shell
$ ./inline-svg images/icons styles/icons.less --backup=false --comment='// out: false, main: styles.less'
```

Command line options
--------------------

### `-b`<br>`--backup`
**Creates a backup of the target file**

values:  | `true` \| `false`
---------|:-
default: | `true`
example: | `-b=false`

### `-r`<br>`--replace-colors=false`
**Replace colours with Less CSS variables used with mixin template**

*Generates Less CSS mixins with parameters to override SVG color and stroke. Requires `.less` extension. This script simply replaces all fill/stroke colors with variables when set true.*

values:   |`true` \| `false`
----------|:-
default:  | `true` when target file specifies `.less` extension
default:  | `false` when target file specifies `.css` extension

### `-t`<br>`--template`

**Template for the CSS class definition**

*Expects two `%s` placeholders, first for the icon name, second for the SVG background-color style.*

value:    | `string`
----------|:-
default:  | for `.css` file targets: <pre>.icon-%s { background-image: url(\"data:image/svg+xml,%s\") }</pre>
default:  | for `.less` file targets: <pre>.icon-%s-mixin(@fill, @stroke: transparent) { @fill: replace(@fill, '#', '%%23'); @stroke: replace(@stroke, '#', '%%23');  background-image: url(\"data:image/svg+xml,%s\") }</pre>
default:  | when `--replace-colors=false`:<pre>.icon-%s() { background-image: url(\"data:image/svg+xml,%s\") }</pre>

### `-c`<br>`--comment`

**Adds any comment before the CSS output**

value:    | `string`
----------|:-
default:  | `''`
example:  | `--comment='// out: false, main: styles.less'`

### `-n`<br>`--new-line`

**New line at the end of the file**
values:   | `true` \| `false`
----------|:-
default:  | `true`
example:  | `--new-line=false`

<br>

. . .

<br>


✨ Enjoy!

[Martin](@martin_adamko)
