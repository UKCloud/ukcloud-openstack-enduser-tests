# Skyscape Openstack End-user tests

Tempest is an Openstack has a project dedicated to testing. It provides coverage in the following forms:
  * API - tests that the API functions as expected
  * Scenario - Allows complex user based scenarios to be setup to allow full workflows to be tested
  * Stress - Allows for complex stress testing workloads to be executed

Skyscape exposes the end-user tests that run to validate consitency of the platform between changes to help customers understand and contribute to the test coverage of the platform. The aim is to improve transparency of the platforms fucntionailty and feature set whilst also enabling customers to contribute tests that are pertinent to their infrastructure.

Users can contribute by either:

  * Making feature requests
  * Submitting pull requests for additional tests

## Overview

Tempest tests can be run from an end user machine with the tempest tooling installing.

# Setup

Download the latest stable release of tempest.

```{r, engine='bash', download}
git clone http://git.openstack.org/openstack/tempest
```

Create a new python virtual environment with all the required dependencies by running

```{r, engine='bash', virtualEnv}
cd tempest
./run_tempest.sh
```

source the new python virtual environment

```{r, engine='bash', activateEnv}
source .venv/bin/activate
```

Install tempest

```{r, engine='bash', Install}
pip install tempest
```

# Configuration
```{r, engine='bash', download}
```
