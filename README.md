# pyMTurkR: An R package to interface with MTurk's Requester API <img src="assets/hex-pyMTurkR.png" align="right" width="200" />

<!-- badges: start -->
[![travis-ci](https://travis-ci.org/cloudyr/pyMTurkR.svg?branch=master)](https://travis-ci.org/cloudyr/pyMTurkR?branch=master)
[![Codecov test coverage](https://codecov.io/gh/cloudyr/pyMTurkR/branch/master/graph/badge.svg)](https://codecov.io/gh/cloudyr/pyMTurkR?branch=master)
![version](https://img.shields.io/badge/version-0.7.0-blue.svg)
![alpha](https://img.shields.io/badge/status-alpha-lightgrey.svg)
![downloads](https://img.shields.io/badge/downloads-142-brightgreen)
<!-- badges: end -->

**pyMTurkR** is an R package that allows you to interface with MTurk's Requester API. 

pyMTurkR provides access to the latest Amazon Mechanical Turk (<a href='https://www.mturk.com'>MTurk</a>) Requester API (<a href="https://docs.aws.amazon.com/AWSMechTurk/latest/AWSMturkAPI/ApiReference_CreateHITOperation.html">version '2017-01-17'</a>), using `reticulate` to wrap the `boto3` SDK for Python. pyMTurkR is a replacement for the now obsolete [MTurkR](https://github.com/cloudyr/MTurkR).

Using this package, you can perform operations like: creating HITs, updating HITs, creating custom Qualifications, reviewing submitted Assignments, approving/rejecting Assignments, sending bonus payments to Workers, sending messages to Workers, blocking/unblocking Workers, and many more. See the [pyMTurkR documentation](assets/pyMTurkR.pdf) for a full list of operations available.


## Why make this?

pyMTurkR was created because on June 1, 2019 Amazon [deprecated the MTurk API (version '2014-08-15')](https://docs.aws.amazon.com/AWSMechTurk/latest/AWSMturkAPI-legacy/Welcome.html) that MTurkR was using, rendering it obsolete. This package was created to maintain MTurk access for R users while migrating to the new MTurk API (version '2017-01-17').

pyMTurkR is not a native R language package. It uses [`reticulate`](https://rstudio.github.io/reticulate) to import and wrap the [`boto3`](https://aws.amazon.com/sdk-for-python) module for Python. Cross-language dependency is not necessarily a bad thing, and from the user perspective there is probably no difference, besides a few extra installation steps. Welcome to the wonderful world of R-python interoperability.


# Installation

## Python and boto3 installation

1. Install Python 2 (>= 2.7) or Python 3 (>= 3.3) ([download page](https://www.python.org/downloads))
2. Install pip for Python ([see "Installing with get-pip.py" here](https://pip.pypa.io/en/stable/installing))
3. Use a `system` command in R to install boto3 via pip

```
system("pip install boto3")
```

## Package installation

```
devtools::install_github("cloudyr/pyMTurkR")
```

## Troubleshooting

If you get a `ModuleNotFoundError: No module named 'boto3'` error, then you should check that you don't have more than one version of python installed on your system.

```
# Check for multiple python installs
reticulate::py_config()
```

If this command returns multiple items under "python versions found" then you might have to specify which one to use.

```
# Specify a python to use
reticulate::use_python("C:\\Python36\\python.exe")
```

# Usage

## Set AWS keys

AWS keys can be set as environment variables.

```R
Sys.setenv(AWS_ACCESS_KEY_ID = "my access key")
Sys.setenv(AWS_SECRET_ACCESS_KEY = "my secret key")
```

## Set environment (Sandbox or Live)

pyMTurkR will run in "sandbox" mode by default. To change this, set `pyMTurkR.sandbox` to `FALSE`.

```R
options(pyMTurkR.sandbox = FALSE)
```


## Examples

```R
library("pyMTurkR")
Sys.setenv(AWS_ACCESS_KEY_ID = "ABCD1234")
Sys.setenv(AWS_SECRET_ACCESS_KEY = "EFGH5678")
options(pyMTurkR.sandbox = FALSE)
AccountBalance()
```

# Changelog

For development updates see the [changelog](https://github.com/cloudyr/pyMTurkR/blob/master/CHANGELOG.md).

# Package maintainer / author

pyMTurkR is written and maintained by [Tyler Burleigh](https://tylerburleigh.com).

<a href="https://twitter.com/intent/follow?screen_name=tylerburleigh"><img src="https://img.shields.io/twitter/follow/tylerburleigh?style=social&logo=twitter" alt="follow on Twitter"></a>

## Additional credits

pyMTurkR borrows code from MTurkR, written by [Thomas J. Leeper](https://thomasleeper.com). pyMTurkR's logo borrows elements from Amazon, R, and python logos; the "three people" element is thanks to Muammark / Freepik.
