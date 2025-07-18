:wave: *New to our project? Be sure to review the [OpenMRS 3 Frontend Developer Documentation](https://o3-docs.openmrs.org). You may find the [Map of the Project](https://o3-docs.openmrs.org/docs/core-concepts) especially helpful.* :teacher: 

![Node.js CI](https://github.com/palladiumkenya/kenyaemr-esm-orders/actions/workflows/ci.yml/badge.svg)

# KenyaEMR Orders App

This repository contains frontend modules for the KenyaEMR 3.x. These modules relate to extension of orders. The modules within this repository include:

- [Imaging Orders](packages/esm-imaging-orders-app/)
- [Procedure Orders](packages/esm-procedure-orders-app/)
- [Medical Supply Orders](packages/esm-medical-supply-orders-app/)
- [Medical Supply Dispensing](packages/esm-medical-supply-dispensing-app/)

## Setup

Check out the developer documentation [here](http://o3-dev.docs.openmrs.org).

This monorepo uses [yarn](https://yarnpkg.com).

To install the dependancies, run:
```bash
yarn install
```

To set up environment variables for the project, follow these steps:

1. Create a copy of the .env.example file by running the following command:
  ```bash
  cp example.env .env
  ```
2. Open the newly created .env file in the root of the project.
3. Add the environment variables you need. 

Note: These variables are currently only used for end-to-end tests.

To start a dev server running all the modules simultaneously, run:

```bash
yarn start
```

This command uses the [openmrs](https://www.npmjs.com/package/openmrs) tooling to fire up a dev server running `esm-patient-chart` as well as the specified module.

Note that this is very resource-intensive.

To start a dev server for a specific module, run:

```bash
yarn start --sources 'packages/esm-<insert-package-name>-app'
```

You could provide `yarn start` with as many `sources` arguments as you require. For example, to run the patient registration and patient search modules only, use:

```bash
yarn start --sources 'packages/esm-patient-search-app' --sources 'packages/esm-patient-registration-app'
```

## Troubleshooting

If you notice that your local version of the application is not working or that there's a mismatch between what you see locally versus what's in the reference application, you likely have outdated versions of core libraries. To update core libraries, run the following commands:

```bash
# Upgrade core libraries
yarn up openmrs@next @openmrs/esm-framework@next

# Reset version specifiers to `next`. Don't commit actual version numbers.
git checkout package.json

# Run `yarn` to recreate the lockfile
yarn
```


## Contributing

Please read our [contributing](http://o3-dev.docs.openmrs.org/#/getting_started/contributing) guide.

## Running tests

### Unit tests
To run unit tests, use:

```sh
yarn test
```

### E2E tests

To run E2E tests, make sure the dev server is running by using:

```sh
yarn start --sources 'packages/esm-*-app/'
```

Then, in a separate terminal, run:

```sh
yarn test-e2e --headed
```

Please read [our e2e docs](e2e/README.md) for more information about E2E testing.

## Design Patterns

For documentation about our design patterns, please visit our [design system](https://zeroheight.com/23a080e38/p/880723--introduction) documentation website.

## Deployment

The `main` branch of this repo is deployed in a [demo environment](https://openmrs-spa.org/openmrs/spa).

## Configuration

This module is designed to be driven by configuration files.

## Version and release

To increment the version, run the following command:

```sh
yarn release
```

You will need to pick the next version number. We use minor changes (e.g. `3.2.0` → `3.3.0`)
to indicate big new features and breaking changes, and patch changes (e.g. `3.2.0` → `3.2.1`)
otherwise.

Note that this command will not create a new tag, nor publish the packages.
After running it, make a PR or merge to `main` with the resulting changeset.

Once the version bump is merged, go to GitHub and
[draft a new release](https://github.com/openmrs/openmrs-esm-patient-management/releases/new). 
The tag should be prefixed with `v` (e.g., `v3.2.1`), while the release title
should just be the version number (e.g., `3.2.1`). The creation of the GitHub release
will cause GitHub Actions to publish the packages, completing the release process.

> Don't run `npm publish`, `yarn publish`, or `lerna publish`. Use the above process.

