# Agent Check: Scylla

## Overview

This Datadog-[Scylla][1] integration collects a majority of the exposed metrics by default, with the ability to customize additional groups based on specific user needs.

Scylla is an open-source NoSQL data store that can act as "a drop-in Apache Cassandra alternative." It has rearchitected the Cassandra model tuned for modern hardware, reducing the size of required clusters while improving theoretical throughput and performance.

## Setup

Follow the instructions below to install and configure this check for an Agent running on a host.

### Installation

The Scylla check is included in the [Datadog Agent][2] package. No additional installation is needed on your server.

### Configuration

1. Edit the `scylla.d/conf.yaml` file, in the `conf.d/` folder at the root of your Agent's configuration directory to start collecting your scylla performance data. See the [sample scylla.d/conf.yaml][3] for all available configuration options. If you previously implemented this integration, see the [legacy example][11].

2. [Restart the Agent][4].

##### Log collection

Scylla has different modes of outputting logs depending on the environment it's running in. See the [Scylla documentation][5] for more specifics on how the application generates logs.

1. Collecting logs is disabled by default in the Datadog Agent, enable it in your `datadog.yaml` file:

      ```yaml
       logs_enabled: true
     ```

2. Uncomment and edit the logs configuration block in your `scylla.d/conf.yaml` file. Change the `type`, `path`, and `service` parameter values based on your environment. See the [sample scylla.d/conf.yaml][3] for all available configuration options.

      ```yaml
       logs:
         - type: file
           path: <LOG_FILE_PATH>
           source: scylla
           service: <SERVICE_NAME>
           #To handle multi line that starts with yyyy-mm-dd use the following pattern
           #log_processing_rules:
           #  - type: multi_line
           #    pattern: \d{4}\-(0?[1-9]|1[012])\-(0?[1-9]|[12][0-9]|3[01])
           #    name: new_log_start_with_date
     ```

3. [Restart the Agent][4].

To enable logs for Kubernetes environments, see [Kubernetes Log Collection][6].

### Validation

[Run the Agent's status subcommand][7] and look for `scylla` under the Checks section.

## Data Collected

### Metrics

See [metadata.csv][8] for a list of metrics provided by this check.

### Events

The Scylla check does not include any events.

### Service Checks

See [service_checks.json][9] for a list of service checks provided by this integration.

## Troubleshooting

Need help? Contact [Datadog support][10].


[1]: https://scylladb.com
[2]: /account/settings/agent/latest
[3]: https://github.com/DataDog/integrations-core/blob/master/scylla/datadog_checks/scylla/data/conf.yaml.example
[4]: https://docs.datadoghq.com/agent/guide/agent-commands/#start-stop-and-restart-the-agent
[5]: https://docs.scylladb.com/getting-started/logging/
[6]: https://docs.datadoghq.com/agent/kubernetes/log/
[7]: https://docs.datadoghq.com/agent/guide/agent-commands/#agent-status-and-information
[8]: https://github.com/DataDog/integrations-core/blob/master/scylla/metadata.csv
[9]: https://github.com/DataDog/integrations-core/blob/master/scylla/assets/service_checks.json
[10]: https://docs.datadoghq.com/help/
[11]: https://github.com/DataDog/integrations-core/blob/7.50.x/scylla/datadog_checks/scylla/data/conf.yaml.example
