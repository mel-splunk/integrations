
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->
<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# supervisor

Monitor Type: `supervisor` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/pkg/monitors/supervisor))

**Accepts Endpoints**: No

**Multiple Instances Allowed**: Yes

## Overview

This monitor will retrieve state of processes running by Supervisor.


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: supervisor
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.html#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `url` | **yes** | `string` | The Supervisor XML-RPC API URL (i.e. `http://localhost:9001/RPC2`). |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


 - ***`supervisor.state`*** (*gauge*)<br>    State code, see [Supervisor process states](http://supervisord.org/subprocess.html#process-states).

### Non-default metrics (version 4.7.0+)

To emit metrics that are not _default_, you can add those metrics in the
generic monitor-level `extraMetrics` config option.  Metrics that are derived
from specific configuration options that do not appear in the above list of
metrics do not need to be added to `extraMetrics`.

To see a list of metrics that will be emitted you can run `agent-status
monitors` after configuring this monitor in a running agent instance.

## Dimensions

The following dimensions may occur on metrics emitted by this monitor.  Some
dimensions may be specific to certain metrics.

| Name | Description |
| ---  | ---         |
| `group` | Name of the process group. |
| `name` | Name of the process. |


