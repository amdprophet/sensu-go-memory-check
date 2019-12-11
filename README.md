# Sensu Go Memory  Checks
[![Bonsai Asset Badge](https://img.shields.io/badge/Sensu%20Go%20Memory%20Checks-Download%20Me-brightgreen.svg?colorB=89C967&logo=sensu)](https://bonsai.sensu.io/assets/asachs01/sensu-go-memory-checks) [![TravisCI Build Status](https://travis-ci.org/asachs01/sensu-go-memory-checks.svg?branch=master)](https://travis-ci.org/asachs01/sensu-go-memory-checks)

This plugin provides checks for system memory for Sensu Go. 

## Installation

While it's generally recommended to use an asset, you can download a copy of the handler plugin from [releases][1],
or create an executable script from this source.

From the local path of the sensu-go-memory-checks repository:

**sensu-go-memory-checks**
```
go build -o /usr/local/bin/sensu-go-memory-checks main.go
```

## Configuration

### Asset Registration

Assets are the best way to make use of this check. If you're not using an asset, please consider doing so! You can find this asset on the [Bonsai Asset Index](https://bonsai.sensu.io/assets/asachs01/sensu-go-memory-checks).

You can download the asset definition there, or you can do a little bit of copy/pasta and use the one below:

```yml
---
type: Asset
api_version: core/v2
metadata:
  name: sensu-go-memory-checks
  namespace: CHANGEME
  labels: {}
  annotations: {}
spec:
  url: https://github.com/asachs01/sensu-go-memory-checks/releases/download/0.0.1/sensu-go-memory-checks_0.0.1_linux_amd64.tar.gz
  sha512: 
  filters:
  - entity.system.os == 'linux'
  - entity.system.arch == 'amd64'
```

**NOTE**: PLEASE ENSURE YOU UPDATE YOUR URL AND SHA512 BEFORE USING THE ASSET. If you don't, you might just be stuck on a super old version. Don't say I didn't warn you ¯\\_(ツ)_/¯

### Handler Configuration

Example Sensu Go definition:

**sensu-go-memory-checks**
```yml
type: CheckConfig
api_version: core/v2
metadata:
  name: sensu-go-memory-checks
  namespace: CHANGEME
spec:
  command: sensu-go-memory-checks
  runtime_assets:
  - sensu-go-memory-checks
  interval: 60
  publish: true
  output_metric_format: nagios_perfdata
  output_metric_handlers:
  - influxdb
  handlers:
  - slack
  subscriptions:
  - system
```

## Usage Examples

### Command line help

```
The Sensu Go check for system memory usage

Usage:
  sensu-go-memory-checks [flags]

Flags:
  -c, --critical string   Critical used percentage for system memory (default "90")
  -h, --help              help for sensu-go-memory-checks
  -w, --warning string    Warning used percentage for system memory. (default "75")

```

## Supported Operating Systems

This project uses `gopsutil`, and is thus largely dependent on the systems that it supports. For this plugin, the following operating systems are supported:

* Linux
* FreeBSD
* OpenBSD
* Mac OS X
* Windows
* Solaris


## Contributing

See https://github.com/sensu/sensu-go/blob/master/CONTRIBUTING.md

[1]: https://github.com/asachs01/sensu-go-memory-checks/releases
