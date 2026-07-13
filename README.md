# Smartling GitHub Connector — Test Repo

A minimal project for validating the [Smartling GitHub Connector](https://help.smartling.com/hc/en-us/articles/360000634173-GitHub-Connector).
It contains source i18n strings in English and a connector configuration that
tells Smartling which files to translate and where to write the results.

## Layout

```
.smartling/config.yml     Connector configuration (locales, file globs, branches)
locales/en/messages.json  App UI strings (source)
locales/en/marketing.json Marketing copy (source)
locales/<locale>/...      Translated files the connector writes back
```

## How to test the connector

1. **Configure the connector** in the Smartling dashboard and point it at this
   repository. Replace `REPLACE_WITH_PROJECT_ID` in `.smartling/config.yml`
   with your Smartling project ID.
2. **Trigger a source push** — edit any string under `locales/en/` and merge to
   `main`. With `pushOnMerge: true`, the connector uploads the changed files.
3. **Request translations** for the target locales listed in the config
   (`es`, `fr`, `de`, `ja`, `zh-CN`).
4. **Review the PR** — once translations complete, the connector opens a pull
   request on the `smartling/translations` branch adding
   `locales/<locale>/*.json` files.
5. **Verify** the translated JSON keys mirror the source structure exactly.

## Notes

- Source files use `{placeholder}` interpolation; confirm Smartling preserves
  the placeholders in every locale.
- Add more file types (`.properties`, YAML, Markdown) under `locales/en/` and a
  matching `files:` entry to broaden the test.
