# Hacked







          'apache.status.total_accesses' => 0,
        }
      }
    }
  ],
  ...
}
```

To drop the `mysql.status.aborted.clients` field from the output
```
class{'metricbeat':
  processors => [
    {
      'drop_field' => {
        'fields' => 'mysql.status.aborted.clients',
      }
    }
  ]
}
```

Please review the [documentation](https://www.elastic.co/guide/en/beats/metricbeat/current/configuration-processors.html)

## Reference
 - [**Public Classes**](#public-classes)
    - [Class: metricbeat](#class-metricbeat)
 - [**Private Classes**](#private-classes)
    - [Class: metricbeat::config](#class-metricbeatconfig)
    - [Class: metricbeat::install](#class-metricbeatinstall)
    - [Class: metricbeat::repo](#class-metricbeatrepo)
    - [Class: metricbeat::service](#class-metricbeatservice)

### Public Classes

#### Class: `metricbeat`

Installs and configures metricbeat.

**Parameters within `metricbeat`**
- `modules`: [Array[Hash]] The required metricbeat.modules section of the configuration.
- `outputs`: [Hash] The required output section of the configuration.
- `beat_name`: [String] The name of the beat shipper (default: hostname)
- `ensure`: [String] Valid values are 'present' and 'absent'. Determines weather
  to manage all required resources or remove them from the node. (default: 'present')
- `disable_config_test`: [Boolean] If true, disable configuration file testing. It
   is generally recommended to leave this parameter at this default value.
   (default: false)
- `fields`: [Hash] Optional fields to add any additional information to the output.
  (default: undef)
- `fields_under_root`: [Boolean] By default custom fields are under a `fields`
  sub-dictionary. When set to true custom fields are added to the root-level
  document. (default: false)
- `logging`: [Hash] Defines metricbeat's logging configuration, if not explicitly
  configured all logging output is forwarded to syslog on Linux nodes and file
  output on Windows. See the [docs](https://www.elastic.co/guide/en/beats/metricbeat/current/configuration-logging.html) for all available options.
- `manage_repo`: [Boolean] When false does not install the upstream repository
  to the node's package manager. (default: true)
- `package_ensure`: [String] The desired state of the Package resources. Only
  applicable if `ensure` is 'present'. (default: 'present')
- `processors`: [Array[Hash]] Add processors to the configuration to run on data
  before sending to the output. (default: undef)
- `queue`: [Hash] Configure the internal queue in packetbeat before being consumed
  by the output(s) in 6.x versions.
- `queue_size`: [Integer] The queue size for single events in the processing
  pipeline. This is only applicable if `major_version` is '5'. (default: 1000)
- `service_ensure`: [String] Determine the state of the metricbeat service. Must
  be one of 'enabled', 'disabled', 'running', 'unmanaged'. (default: enabled)
- `service_has_restart`: [Boolean] When true the Service resource issues the
  'restart' command instead of 'stop' and 'start'. (default: true)
- `tags`: [Array] Optional list of tags to help group different logical properties
  easily. (default: undef)


### Private Classes

#### Class: `metricbeat::config`

Manages metricbeats main configuration file.

#### Class: `metricbeat::install`

Installs the metricbeat package.

#### Class: `metricbeat::repo`

Installs the upstream Yum or Apt repository for the system package manager.

#### Class: `metricbeat::service`

Manages the metricbeat service.

## Limitations

This module does not support loading [kibana dashboards](https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-sample-dashboards.html)
or [elasticsearch templates](https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-template.html), used when outputting
to Elasticsearch.

## Development

Pull requests and bug reports are welcome. If you're sending a pull request,
please consider writing tests if applicable.

### Testing

Sandbox testing is done through the [PDK](https://puppet.com/docs/pdk/1.0/index.html) utility provided by
Puppet. To utilize `PDK` execute the following commands to validate and
test the new code:

1. Validate syntax of `metadata.json`, all `*.pp*` and all `*.rb` files
```
pdk validate
```
2. Perform tests
```
pdk test unit
```
