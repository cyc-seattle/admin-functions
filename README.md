# admin-functions

> **Archived.** The hourly job that ran these reports was retired in
> [cyc-seattle/isthmia#206](https://github.com/cyc-seattle/isthmia/issues/206). The CRM's syncs
> replace these reports. This code is kept as it was, for reference.

A CLI tool that runs reports that extract data from Clubspot and copy it to various Google
spreadsheets.

## Install

[mise](https://mise.jdx.dev/getting-started.html) provides Node and pnpm.

```sh
mise trust
mise run install
```

`mise tasks` lists the rest: `check`, `test`, `format`, and `ci`.

## Authorization

### Clubspot

Clubspot credentials are read from CLI arguments, which are also mapped to the following
environment variables.

```
CLUBSPOT_EMAIL="your email"
CLUBSPOT_PASSWORD="your password"
```

### Google

This package authenticates to Google's APIs with [Application Default Credentials][google-adc].
Point ADC at your own account:

```sh
gcloud auth application-default login
```

## Running

The CLI tool runs reports based on a config spreadsheet, which lists all of the reports to run and
the source and destination parameters thereof.

```sh
pnpm exec tsx src/main.ts --help
```

For CYC Community Sailing Center, the dev config sheet is:

```
CONFIG_SPREADSHEET_ID="1E-ByM0N6NRA53GcTA0BH0IL6MO87VBrAjhaI423USRY"
```

[google-adc]: https://cloud.google.com/docs/authentication/application-default-credentials
