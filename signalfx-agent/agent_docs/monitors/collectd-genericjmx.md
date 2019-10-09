
<!--- Generated by to-integrations-repo script in Smart Agent repo, DO NOT MODIFY HERE --->
<!--- GENERATED BY gomplate from scripts/docs/templates/monitor-page.md.tmpl --->

# collectd/genericjmx

Monitor Type: `collectd/genericjmx` ([Source](https://github.com/signalfx/signalfx-agent/tree/master/internal/monitors/collectd/genericjmx))

**Accepts Endpoints**: **Yes**

**Multiple Instances Allowed**: Yes

## Overview

Monitors Java services that expose metrics on JMX using collectd's
GenericJMX plugin. The GenericJMX plugin reads Managed Beans (MBeans) from
an MBeanServer using JMX. The monitor uses an embedded Java runtime in
collectd via the [Java
plugin](https://collectd.org/wiki/index.php/Plugin:Java) of collectd.

The Java Management Extensions (JMX) is a generic framework to provide and
query various management information. The interface is used by the Java
Virtual Machine (JVM) to provide information about the memory used, threads
and so on. These basic performance values can therefore be collected for
every Java process without any support in the Java process itself.

Advanced Java processes can use the JMX interface to provide performance
information themselves. The Apache Tomcat application server, for example,
provides information on the number of requests processed, the number of
bytes sent, processing time, and thread counts.

See the following for more information
- https://collectd.org/documentation/manpages/collectd-java.5.shtml
- https://collectd.org/wiki/index.php/Plugin:GenericJMX

<!--- SETUP --->
### Config Example
Example (gets the thread count from a standard JMX MBean available on all
Java JMX-enabled apps):

```yaml

monitors:
 - type: collectd/genericjmx
   host: my-java-app
   port: 7099
   mBeanDefinitions:
     threading:
       objectName: java.lang:type=Threading
       values:
       - type: gauge
         table: false
         instancePrefix: jvm.threads.count
         attribute: ThreadCount
```

<!--- SETUP --->
## Troubleshooting

Exposing JMX in your Java application can be a tricky process.  Oracle has a
[helpful guide for Java
8](https://docs.oracle.com/javase/8/docs/technotes/guides/management/agent.html)
that explains how to expose JMX metrics automatically by setting Java
properties on your application.  Here are a set of Java properties that are
known to work with Java 7+:

```
java \
  -Dcom.sun.management.jmxremote.port=5000 \
  -Dcom.sun.management.jmxremote.authenticate=false \
  -Dcom.sun.management.jmxremote.ssl=false \
  -Dcom.sun.management.jmxremote.rmi.port=5000 \
  ...
```

This should work as long as the agent is allowed to access port 5000 on the
Java app's host (i.e. there is no firewall blocking it).  Note that this
does not enable authentication or encryption, but these can be added if
desired.

Assuming you have the `host` config set to `172.17.0.3` and the port set to
`5000` (this is a totally arbitrary port and your JMX app will probably be
something different), here are some errors you might receive and their
meanings:

### Connection Refused
```
Creating MBean server connection failed: java.io.IOException: Failed to retrieve RMIServer stub: javax.naming.ServiceUnavailableException [Root exception is java.rmi.ConnectException: Connection refused to host: 172.17.0.3; nested exception is:
     java.net.ConnectException: Connection refused (Connection refused)]
```

This error indicates that the JMX connect port is not open on the specified
host.  Confirm (via netstat/ss or some other tool) that this port
is indeed open on the configured host, and is listening on an appropriate
address (i.e. if the agent is running on a remote server then JMX should not
be listening on localhost only).

### RMI Connection Issues

```
Creating MBean server connection failed: java.rmi.ConnectException: Connection refused to host: 172.17.0.3; nested exception is:
     java.net.ConnectException: Connection timed out (Connection timed out)
```

This indicates that the JMX connect port was reached successfully, but the
RMI port that it was directed to is being blocked, probably by a firewall.
The easiest thing to do here is to make sure the
`com.sun.management.jmxremote.rmi.port` property in your Java app is set to
the same port as the JMX connect port.  There may be other variations of
this that say `Connection reset` or `Connection refused` but they all
generaly indicate a similar cause.

## Useful links

 - https://realjenius.com/2012/11/21/java7-jmx-tunneling-freedom/


## Configuration

To activate this monitor in the Smart Agent, add the following to your
agent config:

```
monitors:  # All monitor config goes under this key
 - type: collectd/genericjmx
   ...  # Additional config
```

**For a list of monitor options that are common to all monitors, see [Common
Configuration](../monitor-config.html#common-configuration).**


| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `host` | **yes** | `string` | Host to connect to -- JMX must be configured for remote access and accessible from the agent |
| `port` | **yes** | `integer` | JMX connection port (NOT the RMI port) on the application.  This correponds to the `com.sun.management.jmxremote.port` Java property that should be set on the JVM when running the application. |
| `name` | no | `string` |  |
| `serviceName` | no | `string` | This is how the service type is identified in the SignalFx UI so that you can get built-in content for it.  For custom JMX integrations, it can be set to whatever you like and metrics will get the special property `sf_hostHasService` set to this value. |
| `serviceURL` | no | `string` | The JMX connection string.  This is rendered as a Go template and has access to the other values in this config. NOTE: under normal circumstances it is not advised to set this string directly - setting the host and port as specified above is preferred. (**default:** `service:jmx:rmi:///jndi/rmi://{{.Host}}:{{.Port}}/jmxrmi`) |
| `instancePrefix` | no | `string` | Prefixes the generated plugin instance with prefix. If a second `instancePrefix` is specified in a referenced MBean block, the prefix specified in the Connection block will appear at the beginning of the plugin instance, and the prefix specified in the MBean block will be appended to it |
| `username` | no | `string` | Username to authenticate to the server |
| `password` | no | `string` | User password to authenticate to the server |
| `customDimensions` | no | `map of strings` | Takes in key-values pairs of custom dimensions at the connection level. |
| `mBeansToCollect` | no | `list of strings` | A list of the MBeans defined in `mBeanDefinitions` to actually collect. If not provided, then all defined MBeans will be collected. |
| `mBeansToOmit` | no | `list of strings` | A list of the MBeans to omit. This will come handy in cases where only a few MBeans need to omitted from the default list |
| `mBeanDefinitions` | no | `map of objects (see below)` | Specifies how to map JMX MBean values to metrics.  If using a specific service monitor such as cassandra, kafka, or activemq, they come pre-loaded with a set of mappings, and any that you add in this option will be merged with those.  See [collectd GenericJMX](https://collectd.org/documentation/manpages/collectd-java.5.shtml#genericjmx_plugin) for more details. |


The **nested** `mBeanDefinitions` config object has the following fields:

| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `objectName` | no | `string` | Sets the pattern which is used to retrieve MBeans from the MBeanServer. If more than one MBean is returned you should use the `instanceFrom` option to make the identifiers unique |
| `instancePrefix` | no | `string` | Prefixes the generated plugin instance with prefix |
| `instanceFrom` | no | `list of strings` | The object names used by JMX to identify MBeans include so called "properties" which are basically key-value-pairs. If the given object name is not unique and multiple MBeans are returned, the values of those properties usually differ. You can use this option to build the plugin instance from the appropriate property values. This option is optional and may be repeated to generate the plugin instance from multiple property values |
| `values` | no | `list of objects (see below)` | The `value` blocks map one or more attributes of an MBean to a value list in collectd. There must be at least one `value` block within each MBean block |
| `dimensions` | no | `list of strings` |  |


The **nested** `values` config object has the following fields:

| Config option | Required | Type | Description |
| --- | --- | --- | --- |
| `type` | no | `string` | Sets the data set used within collectd to handle the values of the MBean attribute |
| `table` | no | `bool` | Set this to true if the returned attribute is a composite type. If set to true, the keys within the composite type is appended to the type instance. (**default:** `false`) |
| `instancePrefix` | no | `string` | Works like the option of the same name directly beneath the MBean block, but sets the type instance instead |
| `instanceFrom` | no | `list of strings` | Works like the option of the same name directly beneath the MBean block, but sets the type instance instead |
| `attribute` | no | `string` | Sets the name of the attribute from which to read the value. You can access the keys of composite types by using a dot to concatenate the key name to the attribute name. For example: “attrib0.key42”. If `table` is set to true, path must point to a composite type, otherwise it must point to a numeric type. |
| `attributes` | no | `list of strings` | The plural form of the `attribute` config above.  Used to derive multiple metrics from a single MBean. |


## Metrics

These are the metrics available for this monitor.
Metrics that are categorized as
[container/host](https://docs.signalfx.com/en/latest/admin-guide/usage.html#about-custom-bundled-and-high-resolution-metrics)
(*default*) are ***in bold and italics*** in the list below.


#### Group jvm
All of the following metrics are part of the `jvm` metric group. All of
the non-default metrics below can be turned on by adding `jvm` to the
monitor config option `extraGroups`:
 - ***`gauge.jvm.threads.count`*** (*gauge*)<br>    Number of JVM threads
 - ***`gauge.loaded_classes`*** (*gauge*)<br>    Number of classes loaded in the JVM
 - ***`invocations`*** (*cumulative*)<br>    Total number of garbage collection events
 - ***`jmx_memory.committed`*** (*gauge*)<br>    Amount of memory guaranteed to be available in bytes
 - ***`jmx_memory.init`*** (*gauge*)<br>    Amount of initial memory at startup in bytes
 - ***`jmx_memory.max`*** (*gauge*)<br>    Maximum amount of memory that can be used in bytes
 - ***`jmx_memory.used`*** (*gauge*)<br>    Current memory usage in bytes
 - ***`total_time_in_ms.collection_time`*** (*cumulative*)<br>    Amount of time spent garbage collecting in milliseconds

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


