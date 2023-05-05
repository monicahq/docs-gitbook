---
description: How we manage translation (or i18n) in the app
---

# Translation

We are proud to say that we support many languages in Monica. Nothing should go in production without being translated.

## Add a new language

When we want to add a new language that is not yet supported, we should run the following command line (`fr` being the two letter codes identifying the language, here `fr` meaning French).

```sh
php artisan lang:add fr
```

Then we need to translate the default Laravel language files (like the generic error messages) in the new language. We have a package for that, which will let us focus our efforts in something else.

```
php artisan lang:update
```

Once done, you will find a new folder for the new language, and find a set of new files within this directory.

## Translating strings

The core of the work of translating an application is actually about extracting strings to translate from either the Vue or from the backend (sometimes).

To translate a string in a Vue file, you should import the i18n library, then use it to translate:

```javascript
import { trans } from 'laravel-vue-i18n';

// in a method
trans('Are you sure? This action cannot be undone.')

// inside the actual HTML
{{ $t('This is a string to translate') }}
```

Then, each string should be put in the translation files (`fr.json`, `de.json`, ...) like the following:

```json
{
    "This is a string to translate": "C'est une chaîne de caractères à traduire",
}
```

Putting this new string in each translation file can be super time consuming. This is why we have a script that will extract translation files in each view, and put it inside the translation files for you.

```
php artisan monica:localize
```

What remains to be done after that is simply make sure that each new string is translated within the localisation files. How to do that?

Many possibilities these days:

* ChatGPT (it works really well)
* Google Translate
* Github Copilot.

{% hint style="info" %}
Do not submit a PR with new strings that are not translated in every language that we support.
{% endhint %}
