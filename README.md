# TSB cheatsheet

## Building

To run it locally, run:

```bash
yarn install
yarn run dev
```

## Adding cheatsheets

To add a new cheatsheet create a `.md` file in the root with the following header:

```yaml
title: gateways  # Name of the cheatsheet displayed in the UI
layout: 2017/sheet
prism_languages: [bash,yaml] # Languages to highlight in the cheatsheet
weight: -3 
updated: 2022-12-07 # Last updated date - shows up in the UI under the Recently updated section
category: gateways # Category of the cheatsheet - if adding a new category, look at the _data/categories.yml file
intro:
  TSB Gateways. # Text that shows up when hovering over the cheatsheet name in the UI
```

## Adding categories

To add a new category, add a new entry to the `_data/categories.yml` file.