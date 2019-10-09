
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->
<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# prometheus/redis

Monitor Type: `prometheus/redis` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/internal/monitors/prometheus/redis))

**Accepts Endpoints**: **Yes**

**Multiple Instances Allowed**: Yes

## Overview

This monitor scrapes [Prmoetheus Redis
Exporter](https://github.com/oliver006/redis_exporter) metrics and sends
them to SignalFx.  It is a wrapper around the
[prometheus-exporter](./prometheus-exporter.md) monitor that provides a
restricted but expandable set of metrics.


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: prometheus/redis
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.html#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `host` | **yes** | `string` | Host of the exporter |
| `port` | **yes** | `integer` | Port of the exporter |
| `username` | no | `string` | Basic Auth username to use on each request, if any. |
| `password` | no | `string` | Basic Auth password to use on each request, if any. |
| `useHTTPS` | no | `bool` | If true, the agent will connect to the exporter using HTTPS instead of plain HTTP. (**default:** `false`) |
| `skipVerify` | no | `bool` | If useHTTPS is true and this option is also true, the exporter's TLS cert will not be verified. (**default:** `false`) |
| `useServiceAccount` | no | `bool` | Use pod service account to authenticate. (**default:** `false`) |
| `metricPath` | no | `string` | Path to the metrics endpoint on the exporter server, usually `/metrics` (the default). (**default:** `/metrics`) |
| `sendAllMetrics` | no | `bool` | Send all the metrics that come out of the Prometheus exporter without any filtering.  This option has no effect when using the prometheus exporter monitor directly since there is no built-in filtering, only when embedding it in other monitors. (**default:** `false`) |


## Metrics

These are the metrics available for this monitor.
This monitor emits all metrics by default; however, **none are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
-- they are all custom**.



 - ***`redis_aof_current_rewrite_duration_sec`*** (*gauge*)<br>    aof_current_rewrite_duration_sec metric
 - ***`redis_aof_enabled`*** (*gauge*)<br>    aof_enabled metric
 - ***`redis_aof_last_rewrite_duration_sec`*** (*gauge*)<br>    aof_last_rewrite_duration_sec metric
 - ***`redis_aof_rewrite_in_progress`*** (*gauge*)<br>    aof_rewrite_in_progress metric
 - ***`redis_aof_rewrite_scheduled`*** (*gauge*)<br>    aof_rewrite_scheduled metric
 - ***`redis_blocked_clients`*** (*gauge*)<br>    blocked_clients metric
 - ***`redis_client_biggest_input_buf`*** (*gauge*)<br>    client_biggest_input_buf metric
 - ***`redis_client_longest_output_list`*** (*gauge*)<br>    client_longest_output_list metric
 - ***`redis_cluster_enabled`*** (*gauge*)<br>    cluster_enabled metric
 - ***`redis_command_call_duration_seconds_count`*** (*gauge*)<br>    command_call_duration_seconds_count metric
 - ***`redis_command_call_duration_seconds_sum`*** (*gauge*)<br>    Total amount of time in seconds spent per command
 - ***`redis_commands_processed_total`*** (*gauge*)<br>    commands_processed_total metric
 - ***`redis_config_maxclients`*** (*gauge*)<br>    config_maxclients metric
 - ***`redis_config_maxmemory`*** (*gauge*)<br>    config_maxmemory metric
 - ***`redis_connected_clients`*** (*gauge*)<br>    connected_clients metric
 - ***`redis_connected_slaves`*** (*gauge*)<br>    connected_slaves metric
 - ***`redis_connections_received_total`*** (*gauge*)<br>    connections_received_total metric
 - ***`redis_db_avg_ttl_seconds`*** (*gauge*)<br>    Avg TTL in seconds
 - ***`redis_db_keys`*** (*gauge*)<br>    Total number of keys by DB
 - ***`redis_db_keys_expiring`*** (*gauge*)<br>    Total number of expiring keys by DB
 - ***`redis_evicted_keys_total`*** (*gauge*)<br>    evicted_keys_total metric
 - ***`redis_expired_keys_total`*** (*gauge*)<br>    expired_keys_total metric
 - ***`redis_exporter_build_info`*** (*gauge*)<br>    redis exporter build_info
 - ***`redis_exporter_last_scrape_duration_seconds`*** (*gauge*)<br>    The last scrape duration
 - ***`redis_exporter_last_scrape_error`*** (*gauge*)<br>    The last scrape error status
 - ***`redis_exporter_scrapes_total`*** (*gauge*)<br>    Current total redis scrapes
 - ***`redis_instance_info`*** (*gauge*)<br>    Information about the Redis instance
 - ***`redis_instantaneous_input_kbps`*** (*gauge*)<br>    instantaneous_input_kbps metric
 - ***`redis_instantaneous_ops_per_sec`*** (*gauge*)<br>    instantaneous_ops_per_sec metric
 - ***`redis_instantaneous_output_kbps`*** (*gauge*)<br>    instantaneous_output_kbps metric
 - ***`redis_keyspace_hits_total`*** (*gauge*)<br>    keyspace_hits_total metric
 - ***`redis_keyspace_misses_total`*** (*gauge*)<br>    keyspace_misses_total metric
 - ***`redis_latest_fork_usec`*** (*gauge*)<br>    latest_fork_usec metric
 - ***`redis_loading_dump_file`*** (*gauge*)<br>    loading_dump_file metric
 - ***`redis_master_repl_offset`*** (*gauge*)<br>    master_repl_offset metric
 - ***`redis_memory_fragmentation_ratio`*** (*gauge*)<br>    memory_fragmentation_ratio metric
 - ***`redis_memory_max_bytes`*** (*gauge*)<br>    memory_max_bytes metric
 - ***`redis_memory_used_bytes`*** (*gauge*)<br>    memory_used_bytes metric
 - ***`redis_memory_used_lua_bytes`*** (*gauge*)<br>    memory_used_lua_bytes metric
 - ***`redis_memory_used_peak_bytes`*** (*gauge*)<br>    memory_used_peak_bytes metric
 - ***`redis_memory_used_rss_bytes`*** (*gauge*)<br>    memory_used_rss_bytes metric
 - ***`redis_net_input_bytes_total`*** (*gauge*)<br>    net_input_bytes_total metric
 - ***`redis_net_output_bytes_total`*** (*gauge*)<br>    net_output_bytes_total metric
 - ***`redis_process_id`*** (*gauge*)<br>    process_id metric
 - ***`redis_pubsub_channels`*** (*gauge*)<br>    pubsub_channels metric
 - ***`redis_pubsub_patterns`*** (*gauge*)<br>    pubsub_patterns metric
 - ***`redis_rdb_changes_since_last_save`*** (*gauge*)<br>    rdb_changes_since_last_save metric
 - ***`redis_rdb_current_bgsave_duration_sec`*** (*gauge*)<br>    rdb_current_bgsave_duration_sec metric
 - ***`redis_rdb_last_bgsave_duration_sec`*** (*gauge*)<br>    rdb_last_bgsave_duration_sec metric
 - ***`redis_rejected_connections_total`*** (*gauge*)<br>    rejected_connections_total metric
 - ***`redis_replication_backlog_bytes`*** (*gauge*)<br>    replication_backlog_bytes metric
 - ***`redis_slowlog_length`*** (*gauge*)<br>    Total slowlog
 - ***`redis_start_time_seconds`*** (*gauge*)<br>    Start time of the Redis instance since unix epoch in seconds
 - ***`redis_up`*** (*gauge*)<br>    up metric
 - ***`redis_uptime_in_seconds`*** (*gauge*)<br>    uptime_in_seconds metric
 - ***`redis_used_cpu_sys`*** (*gauge*)<br>    used_cpu_sys metric
 - ***`redis_used_cpu_sys_children`*** (*gauge*)<br>    used_cpu_sys_children metric
 - ***`redis_used_cpu_user`*** (*gauge*)<br>    used_cpu_user metric
 - ***`redis_used_cpu_user_children`*** (*gauge*)<br>    used_cpu_user_children metric
The agent does not do any built-in filtering of metrics coming out of this
monitor.

