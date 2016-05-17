# Skyscape Openstack End-user tests

Tempest is an Openstack project dedicated to testing. It provides coverage in the following forms:
  * API - tests that the API functions as expected, both during success and failure
  * Scenario - Allows complex user based scenarios to be setup to allow full workflows to be tested
  * Stress - Allows for complex stress testing workloads to be executed

Skyscape exposes the end-user API and Scenbario tests that run to validate consitency of the platform between changes to help customers understand and contribute to the test coverage. The aim is to improve transparency of the platforms fucntionailty whilst also enabling customers to contribute tests that are pertinent to their infrastructure.

Users can contribute by either:

  * Making feature requests
  * Submitting pull requests for additional tests

## Overview

Tempest tests can be run from an end user machine with the tempest tooling installed and configured.

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

# Configurationo

Tempest requires two files to test. This guide only details a basic setup testing non-admin functionality. To review the configuration in more detail read the sample tempest.conf available in http://docs.openstack.org/developer/tempest/sampleconf.html#tempest-sampleconf

Note: The configuration is configured to use pre-defined accounts rather than dynamic account generation. More information can be found here: http://docs.openstack.org/developer/tempest/configuration.html (Credential Provider Mechanisms)

Edit the tempest config etc/tempest.conf configuring the following values

### URL endpoints
This is the authentication endpoints for botht the v2.0 and v3 API's for the openstack platform e.g.

```{r, engine='bash', Install}
uri = https://services.openstack.skyscapecloud.com:5000/v2.0
```

```{r, engine='bash', Install}
uri_v3 = https://services.openstack.skyscapecloud.com:5000/v3
```

### Test accounts

This needs to point to the relative path of the accounts file listing the credentials to perform operations in the Openstack cloud. This can usally be left as the value below.

```{r, engine='bash', Install}
test_accounts_file = etc/tempest/accounts.yaml
```

### Credential methods

We are using provisioned credentials so dynamic credentials must be disabled

```{r, engine='bash', Install}
use_dynamic_credentials = False
```

You also need to define the default endpoint to use. Currently Skyscape use v2. However we enable tests for both.

```{r, engine='bash', Install}
auth_version = v2
api_v2 = true
api_v3 = true
```

### Compute Configuration 

You must supply a number of images that can be used to perfrom the scenario tests. The following values must be provided

```{r, engine='bash', Install}
image_ref = <image ref e.g. 602d57d9-ff8a-4ccc-9249-11dcea815cc2>
image_ref_alt = <image ref e.g. 602d57d9-ff8a-4ccc-9249-11dcea815cc2>
```

This information can be obtained by running the openstack tools

```{r, engine='bash', Install}

➜  code openstack image list

+--------------------------------------+-----------------------------------------------+--------+
| ID                                   | Name                                          | Status |
+--------------------------------------+-----------------------------------------------+--------+
| 956e49d1-c8a5-4816-820a-2732af1ce957 | glance-test                                   | active |
| d04e07c4-095d-4598-81ec-43c3309a2c99 | ubuntu-14.04-server-amd64-original-downloaded | active |
+--------------------------------------+-----------------------------------------------+--------+
```

```{r, engine='bash', Install}
flavor_ref = <image ref e.g. 2>
flavor_ref_alt = <image ref e.g. 3>
```

➜  code openstack flavor list

+----+-----------+-------+------+-----------+-------+-----------+
| ID | Name      |   RAM | Disk | Ephemeral | VCPUs | Is Public |
+----+-----------+-------+------+-----------+-------+-----------+
| 1  | m1.tiny   |   512 |    1 |         0 |     1 | True      |
| 2  | m1.small  |  2048 |   20 |         0 |     1 | True      |
+----+-----------+-------+------+-----------+-------+-----------+

### Volume attributes

Tests that check volumes can be attached and mounted are run. Based on the image used the volumes list as specific devices. This needs to be updated to match the volume device label that is listed in the image you chose. The default is vdb.

```{r, engine='bash', Install}
volume_device_name = vdb
```

# Running


