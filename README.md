# puppet-rinetd

[![Puppet Forge](https://img.shields.io/puppetforge/v/barnumbirr/rinetd.svg)](https://forge.puppetlabs.com/barnumbirr/rinetd)
[![Puppet Forge - downloads](https://img.shields.io/puppetforge/dt/barnumbirr/rinetd.svg)](https://forge.puppetlabs.com/barnumbirr/rinetd)

1. [Description](#description)
2. [Usage - Configuration options](#usage)
    * [Class Parameters](#class-parameters)
4. [Limitations - OS compatibility, etc.](#limitations)
5. [License](#license)

## Description

Install and manage [rinetd(8) - internet “redirection server”](https://github.com/samhocevar/rinetd) via Puppet.

## Usage

### Install rinetd with default config

```puppet
class { 'rinetd': }
```

### Set allow and deny rules

```puppet
class { 'rinetd':
    allow => ['192.168.178.1', '10.24.0.1', 'fe80:*'],
    deny => ['192.168.1.*', '2001:618:*:e43f'],
}
```

##### Using hiera

```yaml
rinetd::allow:
  - '192.168.178.1'
  - '10.24.0.1'
  - 'fe80:*'

rinetd::deny:
  - '192.168.1.*'
  - '2001:618:*:e43f'
```

### Set forwarding rules

```puppet
class { 'rinetd':
    rules => [
        '192.168.178.1 8080 10.24.0.1 443',
        '10.24.42.1 5901/udp 192.168.7.49 3456/udp',
        '::1 80 192.168.1.2 80 [timeout=1200]'
    ],
}
```

##### Using hiera

```yaml
rinetd::rules:
  - '192.168.178.1 8080 10.24.0.1 443'
  - '10.24.42.1 5901/udp 192.168.7.49 3456/udp'
  - '::1 80 192.168.1.2 80 [timeout=1200]'
```

### Set logfile path

```puppet
class { 'rinetd':
    logfile => ['/var/log/example.log'],
}
```

##### Using hiera

```puppet
rinetd::logfile: '/var/log/example.log'
```

### Use web-server style logfile format

```puppet
class { 'rinetd':
    logcommon => true,
}
```

##### Using hiera

```yaml
rinetd::logcommon: true
```

### Class Parameters

| Parameter           | Type    | Default             | Description |
| :-------------------| :------ |:------------------- | :---------- |
| allow               | array   | []                  | set allow rules |
| deny                | array   | []                  | set deny rules |
| rules               | array   | []                  | set forwarding rules |
| logfile             | string  | /var/log/rinetd.log | set logfile path |
| logcommon           | boolean | false               | use web-server style logfile format |
| package_ensure      | string  | present             | latest,present or absent |
| service_manage      | boolean | true                | manage rinetd service state |
| service_restart     | boolean | true                | manage service restart |

## Limitations

This module is currently only written to work on Debian based operating
systems, although it may work on others. The supported Puppet versions are
defined in the [metadata.json](metadata.json)

## License:

```
Copyright 2017-2024 Martin Simon

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

## Buy me a coffee?

If you feel like buying me a coffee (or a beer?), donations are welcome:

```
BTC : bc1qq04jnuqqavpccfptmddqjkg7cuspy3new4sxq9
DOGE: DRBkryyau5CMxpBzVmrBAjK6dVdMZSBsuS
ETH : 0x2238A11856428b72E80D70Be8666729497059d95
LTC : MQwXsBrArLRHQzwQZAjJPNrxGS1uNDDKX6
```
