# ngx-translate-extract

> Angular translations extractor (plugin for [@ngx-translate](https://github.com/ngx-translate/core)) with support of the custom self closing tags in the html files

> ✓ _Angular 14, Ivy and Angular Universal (SSR) compatible_

Extract translatable (ngx-translate) strings and save as a JSON or Gettext pot file.\
Merges with existing strings if the output file already exists.\
Includes extra verbose information about the extraction process when --verbose cli param is provided. 

## History

This project was originally created by [Kim Biesbjerg](https://github.com/biesbjerg/ngx-translate-extract).
Unfortunately he was unable to continue to maintain it so the Vendure team agreed to take over maintenance of a fork.\
This fork further improves the Vendure team fork. Ensures the support of the custom self closing tags in the html files and 
extends the plugin cli options e.g. with possibility to turn on verbose information about the extraction process. 

## Install

Install the package in your project:

```bash
npm install @pziacek/ngx-translate-extract --save-dev
# or
yarn add @pziacek/ngx-translate-extract --dev
```

Choose the version corresponding to your Angular version:

| Angular    | ngx-translate-extract                                                                               |
|------------|-----------------------------------------------------------------------------------------------------|
| 14         | 1.x.x+                                                                                              |
| 13         | [@vendure/ngx-translate-extract](https://github.com/vendure-ecommerce/ngx-translate-extract) 8.x.x+ |
| 8.x – 12.x | [@biesbjerg/ngx-translate-extract](https://github.com/biesbjerg/ngx-translate-extract) 7.x          |

Add a script to your project's `package.json`:

```json
"scripts": {
  "i18n:init": "ngx-translate-extract --input ./src --output ./src/assets/i18n/template.json --key-as-default-value --replace --format json",
  "i18n:extract": "ngx-translate-extract --input ./src --output ./src/assets/i18n/{en,da,de,fi,nb,nl,sv}.json --clean --format json"
}
```

You can now run `npm run i18n:extract` and it will extract strings from your project.

## Usage

**Extract from dir and save to file**

```bash
ngx-translate-extract --input ./src --output ./src/assets/i18n/strings.json
```

**Extract from multiple dirs**

```bash
ngx-translate-extract --input ./src-a ./src-b --output ./src/assets/i18n/strings.json
```

**Extract and save to multiple files using path expansion**

```bash
ngx-translate-extract --input ./src --output ./src/i18n/{da,en}.json
```

### JSON indentation

Tabs are used by default for indentation when saving extracted strings in json formats:

If you want to use spaces instead, you can do the following:

```bash
ngx-translate-extract --input ./src --output ./src/i18n/en.json --format-indentation ' '
```

### Marker function

If you want to extract strings that are not passed directly to `NgxTranslate.TranslateService`'s
`get()`/`instant()`/`stream()` methods, or its `translate` pipe or directive, you can wrap them
in a marker function/pipe/directive to let `ngx-translate-extract` know you want to extract them.

```bash
npm install @colsen1991/ngx-translate-extract-marker
```

See [@colsen1991/ngx-translate-extract-marker](https://github.com/colsen1991/ngx-translate-extract-marker/blob/master/README.md) documentation for more information.

### Commandline arguments

```
Extract strings from files for translation.
Usage: cli.js [options]

Output
  -f, --format                    Format[string] [choices: "json", "namespaced-json", "pot"] [default: "json"]
      --format-indentation, --fi  Format indentation (JSON/Namedspaced JSON)           [string] [default: "     "]
  -s, --sort                      Sort strings in alphabetical order                                 [boolean]
  -c, --clean                     Remove obsolete strings after merge                                [boolean]
  -r, --replace                   Replace the contents of output file if it exists (Merges by default)
                                                                                                     [boolean]

Extracted key value (defaults to empty string)
  -k, --key-as-default-value     Use key as default value                                            [boolean]
  -n, --null-as-default-value    Use null as default value                                           [boolean]
  -d, --string-as-default-value  Use string as default value                                          [string]

Options:
  -v, --version        Show version number                                                           [boolean]
  -h, --help           Show help                                                                     [boolean]
  -i, --input          Paths you would like to extract strings from. You can use path expansion, glob patterns
                        and multiple paths                                [array] [required] [default: [null]]
  -o, --output         Paths where you would like to save extracted strings. You can use path expansion, glob
                       patterns and multiple paths                                          [array] [required]
  -m, --marker         Name of a custom marker function for extracting strings                        [string]
      --verbose, --ve  Show verbose information                                                      [boolean]

Examples:
  cli.js -i ./src-a/ -i ./src-b/ -o strings.json           Extract (ts, html) from multiple paths
  cli.js -i './{src-a,src-b}/' -o strings.json             Extract (ts, html) from multiple paths using brace
                                                           expansion
  cli.js -i ./src/ -o ./i18n/da.json -o ./i18n/en.json     Extract (ts, html) and save to da.json and en.json
  cli.js -i ./src/ -o './i18n/{en,da}.json'                Extract (ts, html) and save to da.json and en.json
                                                           using brace expansion
  cli.js -i './src/**/*.{ts,tsx,html}' -o strings.json     Extract from ts, tsx and html
  cli.js -i './src/**/!(*.spec).{ts,html}' -o strings.jso  Extract from ts, html, excluding files with ".spec"
  n                                                         in filename
```

## Note for GetText users

Please pay attention of which version of `gettext-parser` you actually use in your project. 
For instance, `gettext-parser:1.2.2` does not support HTML tags in translation keys.

## Credits

- Original library, idea and code: [Kim Biesbjerg](https://github.com/biesbjerg/ngx-translate-extract) ❤️
- Further updates and improvements by [bartholomej](https://github.com/bartholomej) ❤️
- Further updates and improvements by [P4](https://github.com/P4) ❤️
- Further updates and improvements by [colsen1991](https://github.com/colsen1991) ❤️
- Further updates and improvements by [tmijieux](https://github.com/tmijieux) ❤️
- Further updates and improvements by [Vendure Team](https://github.com/vendure-ecommerce/ngx-translate-extract) ❤️
