# Terraform Provider: Snowflake

----

**Please note**: If you believe you have found a security issue, _please responsibly disclose_ by contacting us at [security@chanzuckerberg.com](mailto:security@chanzuckerberg.com).

----

[![Join the chat at https://gitter.im/chanzuckerberg/terraform-provider-snowflake](https://badges.gitter.im/chanzuckerberg/terraform-provider-snowflake.svg)](https://gitter.im/chanzuckerberg/terraform-provider-snowflake?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Build Status](https://travis-ci.com/chanzuckerberg/terraform-provider-snowflake.svg?branch=master)](https://travis-ci.com/chanzuckerberg/terraform-provider-snowflake) [![codecov](https://codecov.io/gh/chanzuckerberg/terraform-provider-snowflake/branch/master/graph/badge.svg)](https://codecov.io/gh/chanzuckerberg/terraform-provider-snowflake)

This is a terraform provider plugin for managing [Snowflake](http://snowflakedb.com) accounts.

## Setup

To use, download a binary from our [releases](https://github.com/chanzuckerberg/terraform-provider-snowflake/releases) and follow the [Terraform directions for installing 3rd party plugins](https://www.terraform.io/docs/configuration/providers.html#third-party-plugins).

TODO fogg config

## Resources

We support managing a subset of snowflakedb resources, with a focus on access control and management.

You can see a number of examples [here](examples).

<!-- START -->
<!-- END -->

## Development

To do development you need Go installed, this repo cloned and that's about it. It has not been tested on Windows, so if you find problems let us know.

If you want to build and test the provider localling there is a make target `make install-tf` that will build the provider binary and install it in a location that terraform can find.

### Testing

For the Terraform resources, there are 3 levels of testing - internal, unit and acceptance tests.

The 'internal' tests are run in the `github.com/chanzuckerberg/terraform-provider-snowflake/pkg/resources` package so that they can test functions that are not exported. These tests are intended to be limited to unit tests for simple functions.

The 'unit' tests are run in  `github.com/chanzuckerberg/terraform-provider-snowflake/pkg/resources_testt`, so they only have access to the exported methods of `resources`. These tests exercise the CRUD methods that on the terraform resources. Note that all tests here make use of database mocking and are run locally. This means the tests are fast, but are liable to be wrong in suble ways (since the mocks are unlikely to be perfect).

You can run these first two sets of tests with `make test`.

The 'acceptance' tests run the full stack, creating, modifying and destroying resources in a live snowflake account. To run them you need a snowflake account and the proper environment variables set- SNOWFLAKE_ACCOUNT, SNOWFLAKE_USER, SNOWFLAKE_PASSWORD, SNOWFLAKE_ROLE. These tests are slower but have higher fidelity.

To run all tests, including the acceptance tests, run `make test-acceptance`.

Note that we also run all tests in our [Travis-CI account](https://travis-ci.com/chanzuckerberg/terraform-provider-snowflake).
