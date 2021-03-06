# ![](././img/integrations_pivotalcloudfoundry.png) Pivotal Cloud Foundry


- [Description](#description)
- [Requirements and Dependencies](#requirements-and-dependencies)
- [Installation](#installation)
- [Configuration](#configuration)
- [Metrics](#metrics)
- [License](#license)

### DESCRIPTION

Monitor a Pivotal Cloud Foundry (PCF) deployment. Download the PCF tile <a target="_blank" href="https://network.pivotal.io/products/signalfx-monitoring-alerting">here</a>. This integration provides metrics about the performance of the various components that make up Pivotal Cloud Foundry. Click <a target="_blank" href="https://network.pivotal.io/products/signalfx-monitoring-alerting">here</a> for more details.

### FEATURES

##### Infrastructure Page

- **Infrastructure Navigator**: On the Infrastructure page in SignalFx, the
    Infrastructure Navigator visualizes Cloud Foundry instances as squares,
    colored by metrics including CPU, disk, and network. Additional views are
    provided for focus on the health and performance of specific Cloud Foundry
    services, as well as Garden Containers. <a target="_blank" href="https://docs.signalfx.com/en/latest/built-in-content/infra-nav.html">Click here to read more about the
    Infrastructure
    Page</a>.

  You can quickly see the status of all of the VMs in your Cloud Foundry cluster:

  [<img src='./img/arch-infra.png' width=200px>](./img/arch-infra.png)

  Here is a sample of the view for Garden Containers:

  [<img src='./img/garden-infra.png' width=200px>](./img/garden-infra.png)

##### Built-in dashboards

This integration includes built-in dashboards listed under **Cloud Foundry** on the Dashboards page in SignalFx. Here are some examples:

- **Key Capacity Scaling Indicators**: Helps you figure out whether you need to
    add resources to your cluster.

  [<img src='./img/key-cap-dashboard.png' width=200px>](./img/key-cap-dashboard.png)

- **Diego**: Metrics around Diego, including many KPIs

  [<img src='./img/diego-dashboard.png' width=200px>](./img/diego-dashboard.png)

- **Garden Containers**: High-level look at the Garden container system

  [<img src='./img/garden-containers-dashboard.png' width=200px>](./img/garden-containers-dashboard.png)


#### REQUIREMENTS AND DEPENDENCIES

This integration requires administrative access to a Pivotal Cloud Foundry deployment. Pivotal Web Services is not supported. Versions known to work are:

| Software                | Version        |
|-------------------------|----------------|
| Pivotal Ops Manager     | 1.9.1+ |
| Pivotal Elastic Runtime | 1.9.0+ |

### INSTALLATION

1. Install the <a target="_blank" href="https://github.com/signalfx/signalfx-cloudfoundry-bridge-boshrelease/releases">latest BOSH release for our Bridge application</a>,
   which pulls metrics from the Loggregator Firehose and sends them to SignalFx.
   This can be installed in any deployment in your CF environment, as long as
   it has access to the BOSH Director and the Traffic Controller server.

- **Metrics** from Pivotal Cloud Foundry should begin streaming into SignalFx.

2. (Optional) To monitor services running within **Garden containers** (for example, webservers),  use <a target="_blank" href="https://github.com/signalfx/signalfx-cloudfoundry-buildpack-decorator">the buildpack decorator</a>
along with the CF meta-buildpack.

3. (Optional) To get our agent on to your own **BOSH deployments**, use <a target="_blank" href="https://github.com/signalfx/agent-boshrelease">our BOSH
release</a>.

### LICENSE

This integration is released under the Apache 2.0 license. See [LICENSE](https://github.com/signalfx/collectd-example/blob/master/LICENSE) for more details.
