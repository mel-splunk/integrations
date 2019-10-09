
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->
<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# collectd/disk

Monitor Type: `collectd/disk` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/internal/monitors/collectd/disk))

**Accepts Endpoints**: No

**Multiple Instances Allowed**: **No**

## Overview

This monitor collects information about the usage of
physical disks and logical disks (partitions).

See https://collectd.org/wiki/index.php/Plugin:Disk.


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: collectd/disk
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.html#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `disks` | no | `list of strings` | Which devices to include/exclude (**default:** `[/^loop[0-9]+$/ /^dm-[0-9]+$/]`) |
| `ignoreSelected` | no | `bool` | If true, the disks selected by `disks` will be excluded and all others included. (**default:** `true`) |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


 - `disk_io_time.io_time` (*cumulative*)<br>    Amount of time spent doing IO in ms
 - `disk_io_time.weighted_io_time` (*cumulative*)<br>    Amount of time spent doing IO in ms multiplied by the queue length
 - `disk_merged.read` (*cumulative*)<br>    The number of disk reads merged into single physical disk access operations.
 - `disk_merged.write` (*cumulative*)<br>    The number of disk writes merged into single physical disk access operations.
 - `disk_octets.read` (*cumulative*)<br>    The number of bytes (octets) read from a disk.
 - `disk_octets.write` (*cumulative*)<br>    The number of bytes (octets) written to a disk.
 - ***`disk_ops.read`*** (*cumulative*)<br>    The number of disk read operations.
 - ***`disk_ops.write`*** (*cumulative*)<br>    The number of disk write operations.
 - `disk_time.read` (*cumulative*)<br>    The average amount of time it took to do a read operation.
 - `disk_time.write` (*cumulative*)<br>    The average amount of time it took to do a write operation.
 - `pending_operations` (*gauge*)<br>    Number of pending operations

### Non-default metrics (version 4.7.0+)

**The following information applies to the agent version 4.7.0+ that has
`enableBuiltInFiltering: true` set on the top level of the agent config.**

To emit metrics that are not _default_, you can add those metrics in the
generic monitor-level `extraMetrics` config option.  Metrics that are derived
from specific configuration options that do not appear in the above list of
metrics do not need to be added to `extraMetrics`.

To see a list of metrics that will be emitted you can run `agent-status
monitors` after configuring this monitor in a running agent instance.

### Legacy non-default metrics (version < 4.7.0)

**The following information only applies to agent version older than 4.7.0. If
you have a newer agent and have set `enableBuiltInFiltering: true` at the top
level of your agent config, see the section above. See upgrade instructions in
[Old-style whitelist filtering](../legacy-filtering.html#old-style-whitelist-filtering).**

If you have a reference to the `whitelist.json` in your agent's top-level
`metricsToExclude` config option, and you want to emit metrics that are not in
that whitelist, then you need to add an item to the top-level
`metricsToInclude` config option to override that whitelist (see [Inclusion
filtering](../legacy-filtering.html#inclusion-filtering).  Or you can just
copy the whitelist.json, modify it, and reference that in `metricsToExclude`.


