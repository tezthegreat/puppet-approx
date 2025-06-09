# approx puppet module

[![Build Status](https://travis-ci.org/cirrax/puppet-approx.svg?branch=master)](https://travis-ci.org/cirrax/puppet-approx)
[![Puppet Forge](https://img.shields.io/puppetforge/v/cirrax/approx.svg?style=flat-square)](https://forge.puppetlabs.com/cirrax/approx)
[![Puppet Forge](https://img.shields.io/puppetforge/dt/cirrax/approx.svg?style=flat-square)](https://forge.puppet.com/cirrax/approx)
[![Puppet Forge](https://img.shields.io/puppetforge/e/cirrax/approx.svg?style=flat-square)](https://forge.puppet.com/cirrax/approx)
[![Puppet Forge](https://img.shields.io/puppetforge/f/cirrax/approx.svg?style=flat-square)](https://forge.puppet.com/cirrax/approx)

#### Table of Contents

1. [Overview](#overview)
1. [Usage](#usage)
1. [Reference](#reference)
1. [Contribuiting](#contributing)


## Overview

This module is used to configure approx. Approx is a caching proxy for 
Debian (and derivative) packages requested by apt-get. 

For puppet versions < 4.0, use the 1.x.x Versions.

## Usage

To start using approx you need to include the approx main class and
add the urls you like to make available.

A minimal example might be:

~~~
class{'approx'}

approx::repository{'debian':
  url => 'http://ftp.ch.debian.org/debian',
}

approx::repository{'debian-security':
  url => 'http://security.debian.org/debian-security',
}
~~~

If you like to use hiera, you can define:

~~~
---
approx::config:
  debian:
      url: 'http://ftp.ch.debian.org/debian'
  debian-security:
      url: 'http://security.debian.org/debian-security'
~~~

To set the listening address and port as well as the maximum number of connections for the systemd socket, use:

~~~puppet
class { 'approx::systemd_socket':
  listen_streams  => ['0.0.0.0:3142'],
  max_connections => 128,
}
~~~

(Requires module version with `max_connections` support.)

## Systemd
Newer debian systems using systemd use a systemd socket to configure the listening port/ip.
To change where approx listen, include the class approx::systemd\_socket and set the $listen\_streams.

## Reference
See [REFERENCE.md](https://github.com/cirrax/puppet-approx/blob/master/REFERENCE.md)

## Contributing

Please report bugs and feature request using GitHub issue tracker.

For pull requests, it is very much appreciated to check your Puppet manifest with puppet-lint
and the available spec tests  in order to follow the recommended Puppet style guidelines
from the Puppet Labs style guide.

### Authors

This module is mainly written by [Cirrax GmbH](https://cirrax.com).

See the [list of contributors](https://github.com/cirrax/puppet-approx/graphs/contributors)
for a list of all contributors.
