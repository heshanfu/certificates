# Step Certificates

An online certificate authority and related tools for secure automated certificate management, so you can use TLS everywhere.

[Website](https://smallstep.com) |
[Documentation](https://smallstep.com/docs/certificates) |
[Installation Guide](#installation-guide) |
[Getting Started](./docs/GETTING_STARTED.md) |
[Contribution Guide](./docs/CONTRIBUTING.md)

[![GitHub release](https://img.shields.io/github/release/smallstep/certificates.svg)](https://github.com/smallstep/certificates/releases)
[![CA Image](https://images.microbadger.com/badges/image/smallstep/step-ca.svg)](https://microbadger.com/images/smallstep/step-ca)
[![Go Report Card](https://goreportcard.com/badge/github.com/smallstep/certificates)](https://goreportcard.com/report/github.com/smallstep/certificates)
[![Build Status](https://travis-ci.com/smallstep/certificates.svg?branch=master)](https://travis-ci.com/smallstep/certificates)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![CLA assistant](https://cla-assistant.io/readme/badge/smallstep/certificates)](https://cla-assistant.io/smallstep/certificates)

[![GitHub stars](https://img.shields.io/github/stars/smallstep/certificates.svg?style=social)](https://github.com/smallstep/certificates/stargazers)
[![Twitter followers](https://img.shields.io/twitter/follow/smallsteplabs.svg?label=Follow&style=social)](https://twitter.com/intent/follow?screen_name=smallsteplabs)

![Animated terminal showing step certificates in practice](https://github.com/smallstep/certificates/raw/master/images/step-ca.gif)

## Motivation

Managing your own *public key infrastructure* (PKI) can be tedious and error prone. Good security hygiene is hard. Setting up simple PKI is out of reach for many small teams, and following best practices like proper certificate revocation and rolling is challenging even for experts.

Amongst numerous use cases, proper PKI makes it easy to use mTLS (mutual TLS) to improve security and to make it possible to connect services across the public internet. Unlike VPNs & SDNs, deploying and scaling mTLS is pretty easy. You're (hopefully) already using TLS, and your existing tools and standard libraries will provide most of what you need. If you know how to operate DNS and reverse proxies, you know how to operate mTLS infrastructure.

![Connect it all with mTLS](https://raw.githubusercontent.com/smallstep/certificates/master/images/connect-with-mtls-2.png)

There's just one problem: **you need certificates issued by your own certificate authority (CA)**. Building and operating a CA, issuing certificates, and making sure they're renewed before they expire is tricky. This project provides the infratructure, automations, and workflows you'll need.

`step certificates` is part of smallstep's broader security architecture, which makes it much easier to implement good security practices early, and incrementally improve them as your system matures.

For more information and docs see [the Step website](https://smallstep.com/certificates) and the [blog post](https://smallstep.com/blog/step-certificates.html) announcing Step Certificate Authority.

> ## 🆕 Autocert
> <a href="autocert/README.md"><img width="50%" src="https://raw.githubusercontent.com/smallstep/certificates/autocert/autocert/autocert-logo.png"></a>
>
> If you're using Kubernetes, make sure you [check out autocert](autocert/README.md): a kubernetes add-on that builds on `step certificates` to automatically inject TLS/HTTPS certificates into your containers.

## Installation Guide

These instructions will install an OS specific version of the `step` binary on your local machine.

> NOTE: While `step cli` is not required to run the `step` Certificate Authority we strongly recommend installing both because `step certificates` is much easier to initialize, manage, and debug using the `step cli` toolkit.

### Mac OS

Install `step` via [Homebrew](https://brew.sh/). The
[Homebrew Formula](https://github.com/Homebrew/homebrew-core/blob/master/Formula/step.rb)
installs both `step cli` and `step certificates`.

```
brew install step

# test ...
step certificate inspect https://smallstep.com
```

> Note: If you have installed `step` previously through the `smallstep/smallstep`
> tap you will need to run the following commands before installing:
```
brew untap smallstep/smallstep
brew uninstall step
```

### Linux

1. [Optional] Install `step cli`.

    Download the latest Debian package from [`step cli` releases](https://github.com/smallstep/cli/releases):

    ```
    wget https://github.com/smallstep/cli/releases/download/X.Y.Z/step_X.Y.Z_amd64.deb
    ```

    Install the Debian package:

    ```
    sudo dpkg -i step_X.Y.Z_amd64.deb
    ```

2. Install `step certificates`.

    Download the latest Debian package from [`step certificates` releases](https://github.com/smallstep/certificates/releases):

    ```
    wget https://github.com/smallstep/certificates/releases/download/X.Y.Z/step-certificates_X.Y.Z_amd64.deb
    ```

    Install the Debian package:

    ```
    sudo dpkg -i step-certificates_X.Y.Z_amd64.deb
    ```

3. Test.

    ```
    step version
    step-ca version
    ```

## Documentation

Documentation can be found in three places:

1. On the command line with `step ca help xxx` where `xxx` is the subcommand you are interested in. Ex: `step help ca provisioners list`

2. On the web at https://smallstep.com/docs/certificates

3. On your browser by running `step ca help --http :8080` and visiting http://localhost:8080

## The Future

We plan to build more tools that facilitate the use and management of zero trust
networks.

* Tell us what you like and don't like about managing your PKI - we're eager to
help solve problems in this space.
* Tell us what features you'd like to see - open issues or hit us on
[Twitter](https://twitter.com/smallsteplabs).
