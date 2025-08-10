# ShipThis Action

A Github Action to use the [ShipThis CLI](https://github.com/shipth-is/cli) to
build and upload your Godot games to the Google Play Store and Apple App Store.

## Quickstart

You will need a ShipThis API token to use this action. You can get one by
installing the ShipThis CLI and logging in:

```bash
npm install -g @shipth-is/cli
shipthis login
```

You can then generate an api token for your project:

```bash
# Use --name if you want to give it a unique name
shipthis apiKey create
```

Take this token secret and add it as a secret in your Github repository called
`SHIPTHIS_TOKEN`.

If you have not done so already, you will need to run through the
[ShipThis](https://shipth.is/docs/create-a-game) wizard to create a 
`shipthis.json` file which should be commited to your repository.

Setup your Github Action workflow file to use this action. Here is an example on
pushing to `main` branch:

```yaml
---
on:
  push:
    branches:
      - main
jobs:
  ship:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: ShipThis Action
        uses: shipth-is/action@v1
        with:
          shipthis_token: ${{ secrets.SHIPTHIS_TOKEN }}
```

## Inputs

The following inputs are available for the action:

- `shipthis_token`: The ShipThis API token to use for authentication. This is
  required.
- `ship_android`: Whether to ship the Android build. Defaults to `true`.
- `ship_ios`: Whether to ship the iOS build Apple. Defaults to `true`.

## License

This project is licensed under the MIT License—see the LICENSE file for details.
