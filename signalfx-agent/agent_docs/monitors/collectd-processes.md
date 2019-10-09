
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->
<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# collectd/processes

Monitor Type: `collectd/processes` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/internal/monitors/collectd/processes))

**Accepts Endpoints**: No

**Multiple Instances Allowed**: **No**

## Overview

Gathers information about processes running on
the host.  See
https://collectd.org/documentation/manpages/collectd.conf.5.shtml#plugin_processes
and https://collectd.org/wiki/index.php/Plugin:Processes for more
information on the configuration options.

Example:

```yaml
 procPath: /proc
 monitors:
  - type: collectd/processes
    processes:
      - mysql
      - myapp
    processMatch:
      docker: "docker.*"
    collectContextSwitch: true
```

The above config will send process metrics for processes named *mysql* and
*myapp*, along with additional metrics on the number of context switches the
process has made.  Also, all processes that start with `docker` will have
their process metrics aggregated together and sent with a `plugin_instance`
value of `docker`.


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: collectd/processes
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.html#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `processes` | no | `list of strings` | A list of process names to match |
| `processMatch` | no | `map of strings` | A map with keys specifying the `plugin_instance` value to be sent for the values which are regexes that match process names.  See example in description. |
| `collectContextSwitch` | no | `bool` | Collect metrics on the number of context switches made by the process (**default:** `false`) |
| `procFSPath` | no | `string` | (Deprecated) Please set the agent configuration `procPath` instead of this monitor configuration option. The path to the proc filesystem -- useful to override if the agent is running in a container. |


## Metrics

These are the metrics available for this monitor.
This monitor emits all metrics by default; however, **none are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
-- they are all custom**.



 - ***`disk_octets.read`*** (*cumulative*)<br>
 - ***`disk_octets.write`*** (*cumulative*)<br>
 - ***`fork_rate`*** (*cumulative*)<br>
 - ***`io_octets.rx`*** (*cumulative*)<br>
 - ***`io_octets.tx`*** (*cumulative*)<br>
 - ***`io_ops.read`*** (*cumulative*)<br>
 - ***`io_ops.write`*** (*cumulative*)<br>
 - ***`ps_code`*** (*gauge*)<br>
 - ***`ps_count.processes`*** (*gauge*)<br>
 - ***`ps_count.threads`*** (*gauge*)<br>
 - ***`ps_cputime.syst`*** (*cumulative*)<br>
 - ***`ps_cputime.user`*** (*cumulative*)<br>
 - ***`ps_data`*** (*gauge*)<br>
 - ***`ps_pagefaults.majflt`*** (*cumulative*)<br>
 - ***`ps_pagefaults.minflt`*** (*cumulative*)<br>
 - ***`ps_rss`*** (*gauge*)<br>
 - ***`ps_stacksize`*** (*gauge*)<br>
 - ***`ps_state.blocked`*** (*gauge*)<br>
 - ***`ps_state.paging`*** (*gauge*)<br>
 - ***`ps_state.running`*** (*gauge*)<br>
 - ***`ps_state.sleeping`*** (*gauge*)<br>
 - ***`ps_state.stopped`*** (*gauge*)<br>
 - ***`ps_state.zombies`*** (*gauge*)<br>
 - ***`ps_vm`*** (*gauge*)<br>
The agent does not do any built-in filtering of metrics coming out of this
monitor.

