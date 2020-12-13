# jcrypto-agent

![Java CI with Maven](https://github.com/jkataja/jcrypto-agent/workflows/Java%20CI%20with%20Maven/badge.svg)

## Accelerate your Java applications' crypto with no code changes

**jcrypto-agent** installs accelerated cryptography to JVM at application starting time.
It is a Java agent that runs before your application.
This means your applications' crypto performance can be improved without needing code changes, requiring rebuilds, or having to maintain build variations for different platforms.

The agent installs the [Amazon Corretto Crypto Provider (ACCP)](https://github.com/corretto/amazon-corretto-crypto-provider) cryptography provider.
This replaces Java cryptography algorithms with those wrapped from the natively compiled [OpenSSL](https://www.openssl.org/) cryptography library.
Native code then uses CPU instructions for hardware-accelerated crypto.
The performance gains and reduced energy usage vary by application and their use of crypto algorithms.

The agent also performs safety checks, making sure the crypto provider is compatible with your platform.

## Usage

### Requirements

Agent requires the following environment to enable accelerated cryptography:

 - Java 8 or newer runtime
 - Linux operating system
 - glibc C-library
 - x86_64 architecture

The use of libc prevents the use of non-libc based distributions, such as Alpine Linux.

ARM architecture support will be added with runtime linking when this becomes generally available in ACCP.

### Install

Download the latest version from [releases page](https://github.com/jkataja/jcrypto-agent/releases)
or using:

```sh
$ wget https://github.com/jkataja/jcrypto-agent/releases/download/v0.20201213/jcrypto-agent-0.20201213.jar
```

To install the agent, add the `-javaagent` argument to your JVM command line arguments.
Specify path to the agent JAR with version.
For example:

```sh
-javaagent:jcrypto-agent-0.20201213.jar
```

The agent runs before your application's `main` method, configuring ACCP as the crypto provider.
It then verifies that ACCP is installed as the highest priority crypto provider.
Optionally, add the `assert` option to agent options e.g. `-javaagent:jcrypto-agent-0.20201213.jar=assert` to also assert the installation is successful or throw an exception.
Without this option, the crypto provider will grafecully fall back to the default provider.

## Resources

 - [GitHub corretto/amazon-corretto-crypto-provider](https://github.com/corretto/amazon-corretto-crypto-provider)
 - [GitHub openssl/openssl](https://github.com/openssl/openssl)
 - [OpenSSL](https://www.openssl.org/) TLS/SSL and crypto library

## Meta

Janne Kataja – [@jkataja](https://twitter.com/jkataja) – fistname.lastname at gmail

GitHub [jkataja/jcrypto-agent](https://github.com/jkataja/jcrypto-agent)

This software is provided "as is", without warranty of any kind.

Distributed under the Apache License v2 license. See ``LICENSE`` for more information.

This software contains [Amazon Corretto Crypto Provider](https://github.com/corretto/amazon-corretto-crypto-provider), licensed under the Apache License v2 and 
portions licensed under the dual OpenSSL and SSLeay license, specifically this includes software developed by the OpenSSL Project for use in the [OpenSSL Toolkit](https://www.openssl.org) and this product also includes cryptographic software written by Eric Young (eay@cryptsoft.com).
