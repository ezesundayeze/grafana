---
title: $EXPORTER_NAME
layout: exporter
subnav: false
exporter_logo: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE/assets/logo-$EXPORTER_NAME_LOWERCASE.png
tabs:
  - title: Overview
    key: overview
    page: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE
  - title: Installation
    key: installation
    page: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE/install
  - title: Recording rules
    key: recording-rules
    page: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE/recording-rules
  - title: Dashboards
    key: dashboards
    page: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE/dashboards
  - title: Alerting rules
    key: alerting-rules
    page: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE/alerting-rules
  - title: Grafana Cloud Integration
    key: grafana-cloud-integration
    tab_class: resource-subnav__item--highlight p-half br-5
    page: /oss/prometheus/exporters/$EXPORTER_NAME_LOWERCASE/cloud-integration
---
## Introduction

The following quickstart provides setup instructions and preconfigured dashboards, alerting rules, and recording rules for $EXPORTER_NAME. After running through the steps in this quickstart, you will have:

- Set up and configured $EXPORTER_NAME to collect $SYSTEM_NAME metrics like [TODO]. $EXPORTER_NAME will expose these as Prometheus-style metrics.

- Configured Prometheus to scrape $EXPORTER_NAME metrics and optionally ship them to Grafana Cloud.

- Set up a preconfigured and curated set of recording rules to cache frequent Prometheus queries.

- Imported Grafana dashboards to visualize your metrics data.

- Set up Prometheus alerting rules to alert on your metrics data.

### Metrics usage

This exporter publishes roughly $NUM_TIME_SERIES Prometheus time series by default. To see a list of metrics shipped by default with this exporter, please download a sample metrics scrape [here](TODO: sample_scrape.out).

Note that depending on its configuration, $EXPORTER_NAME may collect and publish far more metrics than this default set. To learn more about configuring $EXPORTER_NAME and toggling its collectors, please see the $EXPORTER_NAME [GitHub repository]($MIXIN_URL).

Beyond toggling $EXPORTER_NAME’s settings, you can reduce metrics usage by dropping time series you don’t need to store in Prometheus or Grafana Cloud. To learn how to do this, please see [Reducing Prometheus metrics usage with relabeling](https://grafana.com/docs/grafana-cloud/billing-and-usage/prometheus/usage-reduction/) from the Grafana Cloud docs.

### Grafana Cloud’s $EXPORTER_NAME Integration

If you’re using Grafana Cloud, you can skip all of the steps in this guide by installing the $EXPORTER_NAME Integration, which is designed to help you get up and running in a few commands and clicks. [Sign up for free](/signup/cloud/connect-account?pg=oss-prom-$EXPORTER_NAME_LOWERCASE-exporter&plcmt=body-txt-overview).

To learn how to set up $EXPORTER_NAME using the $EXPORTER_NAME Integration, please see [$EXPORTER_NAME Integration]($INTEGRATION_URL) from the Grafana Cloud docs.
