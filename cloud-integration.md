---
title: Cloud integration
layout: exporter
_build:
  render: false
---
{{< class "bg-solitude p-1 mb-1" >}}

Grafana Cloud comes with an ever-expanding set of integrations to quickly get an observability stack up and running in minutes. The $SYSTEM_NAME Integration, built-in to the Grafana Cloud Agent, exposes and scrapes essential $SYSTEM_NAME metrics and pushes them to Grafana Cloud. The agent will scrape metrics using an embedded $EXPORTER_NAME, and Grafana Cloud will automatically provision tailored Grafana dashboards and alerts for visualizing and acting on this data.

{{< btn link="/signup/cloud/connect-account?pg=oss-prom-$EXPORTER_NAME_LOWERCASE-exporter&plcmt=body-txt-overview" type="primary br-5" >}}Sign up for a free account to get started{{< /btn >}}

{{< /class >}}

To learn more, check out the [Grafana Cloud docs](https://grafana.com/docs/grafana-cloud/integrations/).

#### How it works

Configuring, installing, connecting, and maintaining Prometheus monitoring components typically involves significant domain knowledge. It can take quite a while to go from setup to dashboard and alerts. As the creators of Grafana - and core contributors to Prometheus and Cortex - we build simple integrations to abstract some of this work away in order to quickly get started. How it works:

1. Sign up (or log in) for a [free Grafana Cloud account](/signup/cloud/connect-account?pg=oss-prom-$EXPORTER_NAME_LOWERCASE-exporter&plcmt=body-txt-overview).
2. Select the target you’d like to observe (an ever-expanding catalogue).
3. Run a one-line command to install the Grafana Agent. The agent embeds abnd preconfigures Exporters to expose default metrics, and pushes them to the Grafana Cloud metrics backend.
4. Voila! You’ll see tailored Grafana dashboards and will benefit from sane alerting defaults.

Looking for a different Exporter or integration? Check out our [growing library of integrations for popular components](/docs/grafana-cloud/integrations/) like MySQL, Postgres, Redis, Memcached and more.
