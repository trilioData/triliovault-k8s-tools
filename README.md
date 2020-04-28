# Welcome to TrilioVault for k8s Tools Repository

This repository is intended to store the different helper tools, integrations that we will be building along with the community around our TrilioVault for k8s product. We welcome community contribution and anyone can contribute. Thanks for your contribution in advance!

# Available Tools
* Metrics Exporter: We have developed a prometheus exporter within the product. It's available even for free tier users. README for the same same is available [here](https://github.com/trilioData/triliovault-k8s-tools/blob/master/tools/prometheus/exporter_metrics.md)
* Grafana Dashboards:  Using the metrics that our prometheus exporter emits, we have provided a set of dashboards that can be easily imported in your existing grafana setup. Dashboard files are available [here](https://github.com/trilioData/triliovault-k8s-tools/tree/master/tools/grafana/dashboards)
* Preflight Checks: We have developed a tool which checks for all the necessary dependencies on your k8s cluster. This tool can be run before installation. It will output the missing dependencies if any. You can run it remotely by pointing our cluster kubeconfig. README for the same is available [here](https://github.com/triliovault-k8s-issues/triliovault-k8s-issues/blob/master/tools/preflight/README.md)
* Support Collector: In order to help our engineering team to triage customer issues, we have developed a tool to collect all the necessary log information from the customer environment. We also have a public [repo](https://github.com/triliovault-k8s-issues/triliovault-k8s-issues/issues) for anyone to report any issues. This tool should be used by reporting any issues. README for the same is available [here](https://github.com/triliovault-k8s-issues/triliovault-k8s-issues/blob/master/tools/log_collector/README.md)

