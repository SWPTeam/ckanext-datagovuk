# ckanext-datagovuk

The CKAN extension for data.gov.uk

## Features

- Configures Sentry automatically using a `SENTRY_DSN` environment variable.

## Installation

To install ckanext-datagovuk:

1. Activate your CKAN virtual environment, for example:

```
/usr/lib/ckan/default/bin/activate
```

1. Install the ckanext-datagovuk Python package into your virtual environment:

```
pip install ckanext-datagovuk
```

1. Add `datagovuk` to the `ckan.plugins` setting in your CKAN config file (by default the config file is located at `/etc/ckan/default/production.ini`).

1. Restart CKAN. For example if you've deployed CKAN with Apache on Ubuntu:

```
sudo service apache2 reload
```

## Config Settings

`ckan.datagovuk.trim_strings_for_index_limit`: when indexing packages, string fields will be truncated to this length unless they are known to be under a text-indexed key. Solr 6 has a field limit of 32k for string fields, but note that our truncation is applied per-json-value, and a Solr value can contain multiple json values which then get squashed together to a single field value, so using a number under half Solr's limit is wise.

## Development Installation

To install ckanext-datagovuk for development, activate your CKAN virtualenv and
then:

```
git clone https://github.com/alphagov/ckanext-datagovuk.git
cd ckanext-datagovuk
python setup.py develop
pip install -r dev-requirements.txt
```

## Running the Tests

Start by running the [docker ckan](https://github.com/alphagov/docker-ckan#development-mode) stack to set up the CKAN environment.

Run the tests:

```
python -m pytest --ckan-ini=test.ini ckanext/datagovuk/tests/
```

## Creating test data

To be able to run the [CKAN functional tests](https://github.com/alphagov/ckan-functional-tests) we need to create test data.

First set the environment variables:

- `CKAN_INI` - location of CKAN ini file, this is already set on the docker stack
- `CKAN_TEST_SYSADMIN_NAME` and `CKAN_TEST_SYSADMIN_PASSWORD`

Then run the paster command:

```
ckan datagovuk create-dgu-test-data
```

To remove the test data:

```
ckan datagovuk remove-dgu-test-data
```

## Deploying CKAN, PyCSW and Solr

By default, merging a PR into main will trigger a build of the CKAN image and create PRs on the govuk-dgu-charts repo. Updating the tag will build and push a tagged image and create the PR for Staging and Production environments in the govuk-dgu-charts repo.

If you want to deploy updates to PyCSW or Solr then you'll need to trigger the build manually via the github actions tab and manually update the pycsw or solr tag in govuk-dgu-charts repo for each environment.
