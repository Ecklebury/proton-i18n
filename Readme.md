# Proton I18N

A CLI to manage translations
    - validation
    - extraction
    - sync with crowdin

We use [ttag](https://github.com/ttag-org/ttag) for our React projects and [angular-gettext](https://github.com/rubenv/angular-gettext) for our [WebClient](https://github.com/ProtonMail/WebClient).


## How to install ?

```sh
$ npm i -D github:ProtonMail/proton-i18n.git#semver:^1.0.0
``` 

## Commands
```sh
$ ./index.js --help
Usage: $ proton-i18n <command>
Available commands:
  - crowdin
      To update, download etc. translations (--help to get more details)
  - validate
      To validate the translations, check if we have contexts
  - extract
      Extract all translations from the projet
``` 

### Validate

```sh
$ proton-i18n validate
``` 

> Output errors in translation if we don't find a context for one or many translatins.

```sh
$ proton-i18n validate --lint
``` 

> For the CI, reject if there is at least one missing context


### Crowdin

```sh
$ proton-i18n crowdin --help
``` 

```sh
$ proton-i18n crowdin --help
Usage: $ proton-i18n crowdin <flag>
Available flags:
  - --sync|-s
      Update app's translations with the ones from crowdin.
      You can configure which translations you want to update by using a file i18n.txt.
      each translations (ex: fr) = one line.
      More informations on the Wiki
  - --update|-u
      Update crowdin with our export file from the app
  - --check|-c
      To check the progress of an export from crowdin (to know if it's done or not yet)
  - --export|-e
      Ask to crowdin to create an export of translations, as it needs some time to prepare them
  - --list|-l
      List translations available on crowdin sorted by most progress done.
      Usefull to export translations ex:

        $ proton-i18n crowdin --list --type
            only list the code of the translation

        $ proton-i18n crowdin --list --type --limit=95
            only list the code of the translation and limit progress >= 95 + approved >= 95

        $ proton-i18n crowdin --list --type --limit=95 --ignore-approved
            only list the code of the translation and limit progress >= 95

``` 

## How to setup ?

You need to have a file `.env` inside the directory `<project>/env/`.
```sh
CROWDIN_KEY_API=<API-KEY>
PROJECT_NAME=<CROWDIN-PROJECT-NAME>
DEST_FILE='ProtonMail Web Application.pot'
``` 

You don't need these key if you don't manage crowdin, for extraction and validation we won't need them.

:warning: _If you work with the **WebClient** you must have a key inside the env_
```sh
APP_KEY=Angular
```

> We need this key to detect the project as we require some custom code for it.

### Custom translations to update/add inside your app 

You will need to create the file `env/i18n.txt`. It's a file listing translations you want to add inside the app. 
ex:
``` 
cs
de
es-ES
fr
id
it
ja
nl
pl
pt-BR
ro
ru
tr
uk
zh-CN
zh-TW
```

> One line = one translation. For some translations we need a custom format for the locale ;)

 :warning: YOU MUST FOLLOW THIS FORMAT when there is a locale.
 To find the format it's easy, look at the URL: https://crowdin.com/project/<prject-name>/pt-BR# -> ok it's pt-BR
