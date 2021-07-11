---
title: Install
layout: exporter
_build:
  render: false
---
## $EXPORTER_NAME Quickstart

In this guide you'll learn how to set up and configure the $EXPORTER_NAME to collect $SYSTEM_NAME metrics like [TODO], and expose them as Prometheus-style metrics. You'll then configure [Prometheus](https://prometheus.io/) to scrape $SYSTEM_NAME metrics and optionally ship them to Grafana Cloud. Finally, you'll set up a preconfigured and curated set of [recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/), Grafana [dashboards](https://grafana.com/grafana/dashboards), and [alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/). At the end of this guide you'll have dashboards that you can use to visualize your $SYSTEM_NAME metrics, and set of preconfigured alerts.

If you're using [Grafana Cloud](https://grafana.com/products/cloud/), the [$SYSTEM_NAME]($INTEGRATION_URL) Integration can help you get up and running quickly. The $SYSTEM_NAME Integration embeds the $EXPORTER_NAME into the [Grafana Cloud Agent](https://github.com/grafana/agent) and automatically provisions alerting rules and dashboards, so you don't have to run through the steps in this guide. To learn how to set up $EXPORTER_NAME using the $SYSTEM_NAME Integration, please see [$SYSTEM_NAME Integration]($INTEGRATION_URL)  from the Grafana Cloud docs.

## Prerequisites

Before you get started, you should have the following available to you:

- [TODO: machine prerequisite]
- [TODO: system prerequisite]
- Prometheus running in your environment or directly on the machine. To learn how to install Prometheus, please see [Installation](https://prometheus.io/docs/prometheus/latest/installation/) from the Prometheus docs.
- Grafana running in your environment or directly on the machine. To learn how to install Grafana, please see [Install Grafana](https://grafana.com/docs/grafana/latest/installation/) from the Grafana docs. 
- (Optional) A Grafana Cloud account. Grafana Cloud hosts Grafana and a [Cortex](https://grafana.com/oss/cortex/)-based Prometheus metrics endpoint. You will still need to scrape metrics, using either Prometheus installed in your environment, or the [Grafana Cloud Agent](https://github.com/grafana/agent). To learn more about Grafana Cloud, please see [Grafana Cloud](https://grafana.com/products/cloud/).

## Step 1: Setting up $EXPORTER_NAME

In this step you'll set up the $SYSTEM_NAME exporter on your machine to collect and expose $SYSTEM_NAME metrics in Prometheus format. This guide uses an Ubuntu 20.04 system with [TODO: system version]. Steps may vary slightly depending on your operating system and $SYSTEM_NAME version.

To begin, log in to your machine and download the relevant $EXPORTER_NAME binary. This guide uses the `linux-amd64` binary but you should choose the one corresponding to your system's OS and architecture:

```
wget $EXPORTER_BINARY_URL
```

Replace `$EXPORTER_VERSION` with the version you'd like to install. This guide may become stale so it's best to check the $EXPORTER_NAME [Releases]($EXPORTER_RELEASES_URL) page for the latest stable version.

Unzip the tarball and `cd ` into the directory:

```
tar xvfz TODO
cd TODO
```

[TODO: EXPORTER SETUP STEPS]

Finally, run the exporter:

```
./[TODO]
```

```
TODO EXPORTER OUTPUT
```

If you see the above output, you successfully ran $EXPORTER_NAME.

$EXPORTER_NAME publishes $SYSTEM_NAME metrics in Prometheus format on port $EXPORTER_PORT. You can test this using `curl`. You will need to open a new SSH session or background the $EXPORTER_NAME process to use `curl`. 

```
curl http://localhost:$EXPORTER_PORT/metrics
```

```
. . .
TODO SAMPLE METRICS SCRAPE
```

If you see the above output, you're ready to begin scraping $SYSTEM_NAME metrics using Prometheus. 

To avoid running and managing $EXPORTER_NAME from the command line, you can create a `systemd` service. To learn how to do this, please see [Creating a systemd service to manage the agent](https://grafana.com/docs/grafana-cloud/agent/agent_as_service/). Replace the path to the agent binary with the path to $EXPORTER_NAME.

[TODO EXPORTER FEATURES]. To learn more about these features, please see the [$EXPORTER_NAME GitHub repository]($EXPORTER_REPO_URL).

## Step 2: Scraping $EXPORTER_NAME using Prometheus

Now that the $EXPORTER_NAME is up and running on your machine, you can configure a Prometheus scrape job to collect and store $EXPORTER_NAME metrics.

Add the following scrape job config to the `scrape_configs` section of your `prometheus.yml` configuration file:

```
- job_name: $SYSTEM_NAME_LOWERCASE
  static_configs:
  - targets: ['$EXPORTER_NAME_LOWERCASE_machine_IP_address:$EXPORTER_PORT']
```

Replace `$EXPORTER_NAME_LOWERCASE_machine_IP_address` with the IP address of the machine running $EXPORTER_NAME. If you're running Prometheus on the same machine, this will be `localhost`. To learn more about configuring Prometheus, please see [Configuration](https://prometheus.io/docs/prometheus/latest/configuration/configuration/) from the Prometheus docs.

If you don't have a `prometheus.yml` configuration file, create a simple one using your favorite text editor. Open your preferred text editor and paste in the following Prometheus configuration:

```
global:
  scrape_interval: 15s

scrape_configs:
- job_name: $SYSTEM_NAME_LOWERCASE
  static_configs:
  - targets: ['$EXPORTER_NAME_LOWERCASE_machine_IP_address:$EXPORTER_PORT']
```

This configuration tells Prometheus to scrape all jobs every 15 seconds. The only configured scrape job is called `$EXPORTER_NAME_LOWERCASE` and defines a `$EXPORTER_NAME_LOWERCASE_machine_IP_address:$EXPORTER_PORT` target. By default, Prometheus will scrape the `/metrics` endpoint using HTTP.

Save and close the file. You can then run Prometheus with the file using the following command:

```
./prometheus --config.file=./prometheus.yml
```

### Shipping metrics to Grafana Cloud

To ship $EXPORTER_NAME metrics to Grafana Cloud from Prometheus, configure the `remote_write` parameter in your `prometheus.yml` configuration file. To learn more, please see [Metrics — Prometheus](https://grafana.com/docs/grafana-cloud/metrics/prometheus/) from the Grafana Cloud docs. To learn more about the `remote_write` parameter, please see [`remote_write`](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#remote_write) from the Prometheus docs.

## Step 3: Configure recording rules

Using recording rules, you can precompute and cache frequently queried metrics. For example, if a dashboard panel uses a  computationally intensive query like a `rate()`, you can create a recording rule that runs at a regular reduced interval and saves the result of the intensive query in a new time series. This avoids fetching and computing data every time the dashboard gets refreshed. To learn more about Prometheus recording rules, please see [Recording Rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/) from the Prometheus docs.

**You should load the following recording rules before loading the dashboards in this guide.** The dashboard queries and alerting rules use recording rules to reduce load on the Prometheus or Grafana Cloud Metrics servers, depending on where you're evaluating the rules.

You can fetch the recording rule YAML file [here](?tab=recording-rules).

This recording rule YAML file was generated using the $EXPORTER_NAME [mixin]($MIXIN_URL).

### Load recording rules into Prometheus

To load recording rules into Prometheus, add the following to your `prometheus.yml` configuration file:

```
rule_files:
  - "$EXPORTER_NAME_LOWERCASE_recording_rules.yml"
```

Be sure to replace `$EXPORTER_NAME_LOWERCASE_recording_rules.yml` with the path to your $EXPORTER_NAME recording rules YAML file.

### Load recording rules into Grafana Cloud

To learn how to load recording rules into Grafana Cloud, please see [Prometheus and Loki rules with cortextool](https://grafana.com/docs/grafana-cloud/alerts/alerts-rules/#prometheus-and-loki-rules-with-cortextool).

## Step 4: Configuring dashboards

This quickstart includes [TODO # DASHBOARDS]:

- TODO DASHBOARD 1
- TODO DASHBOARD 2
- 

To learn how to import these dashboards into Grafana, please see [Importing a dashboard](https://grafana.com/docs/grafana/latest/dashboards/export-import/#importing-a-dashboard) from the Grafana docs. 

**These dashboard queries may depend on the recording rules defined in the previous step. Be sure to import these before importing the dashboards.**

You can fetch the dashboards [here](T?tab=dashboards). 

## Step 5: Configuring alerts

With Prometheus alerting rules, you can define alerts that fire when PromQL expressions breach some threshold or satisfy specified conditions over a period of time. For example, you can define a `HighRequestLatency` alert that fires when a request latency metric is greater than some threshold over a period of time. As soon as the alerting condition is triggered, the alert moves into `Pending` state. After satisfying the condition for the period of time defined by the `for` parameter, the alert moves into `Firing` state. You can configure routing and notifications for firing alerts using a tool like [Alertmanager](https://prometheus.io/docs/alerting/latest/alertmanager/). Alertmanager is also built-in to Grafana Cloud. 

You can fetch the alerting rule YAML file [here](?tab=alerting-rules).

### Load alerting rules into Prometheus

To load alerting rules into Prometheus, add the following to your `prometheus.yml` configuration file:

```
rule_files:
  - "$EXPORTER_NAME_LOWERCASE_alerting_rules.yml"
```

Be sure to replace `$EXPORTER_NAME_LOWERCASE_alerting_rules.yml` with the path to your $SYSTEM_NAME alerting rules YAML file.

### Load alerting rules into Grafana Cloud

To learn how to load alerting rules into Grafana Cloud, please see [Prometheus and Loki rules with cortextool](https://grafana.com/docs/grafana-cloud/alerts/alerts-rules/#prometheus-and-loki-rules-with-cortextool). 

## Conclusion

In this quickstart you installed and ran $EXPORTER_NAME on your Linux machine. You then configured Prometheus to scrape the database and $SYSTEM_NAME metrics exposed by $EXPORTER_NAME. You loaded recording rules and alerting rules into Prometheus, and finally imported Grafana dashboards to visualize your $SYSTEM_NAME metrics.

If you're using Grafana Cloud, you can skip all of the steps in this guide by installing the $SYSTEM_NAME integration with the Grafana Cloud Agent. This integration embeds a preconfigured $EXPORTER_NAME into the agent and automatically provisions Grafana dashboards and Prometheus alerting and recording rules, so you don't have to import them manually. To learn how to set up the $SYSTEM_NAME integration, please see [Grafana Cloud Integrations](https://grafana.com/docs/grafana-cloud/integrations/).

The dashboards, recording rules, and alerting rules were generated using the $EXPORTER_NAME Mixin. Mixins are reusable templates for dasboards, recording rules, and alerts curated and designed by subject matter experts. To learn more, please see the [$SYSTEM_NAME Mixin]($MIXIN_URL) repository.
