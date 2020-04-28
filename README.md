# Welcome to TrilioVault for k8s Tools Repository

This repository is intended to store the different helper tools, integrations that we will be building along with the community around our TrilioVault for k8s product. We welcome community contribution and anyone can contribute. Thanks for your contribution in advance!

# Available Tools
* Metrics Exporter: We have developed a prometheus exporter within the product. It's available even for free tier users. README for the same same is available [here]()
* Grafana Dashboards:  Using the metrics that our prometheus exporter emits, we have provided a set of dashboards that can be easily imported in your existing grafana setup. Dashboard files are available [here]()
* Preflight Checks: We have developed a tool which checks for all the necessary dependencies on your k8s cluster. This tool can be run before installation. It will output the missing dependencies if any. You can run it remotely by pointing our cluster kubeconfig. README for the same is available [here]()
* Support Collector: In order to help our engineering team to triage customer issues, we have developed a tool to collect all the necessary log information from the customer environment. We also have a public [repo]() for anyone to report any issues. This tool should be used by reporting any issues. README for the same is available [here]()

