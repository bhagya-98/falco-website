---
title: Forwarding Alerts
description: Forward Falco Alerts to third parties
linktitle: Forwarding Alerts
weight: 30
---

Falco alerts can easily be transmitted to third-party systems. Their JSON format allows them to be easily consumed for storage, analysis and reaction. 

# Falcosidekick

Falcosidekick is a proxy forwarder, it acts as central point for any fleet of Falco instances using their http outputs to send their alerts.

The current available outputs are chat, alert, log, storage, streaming systems, etc. The exhaustive list can be found [here](https://github.com/falcosecurity/falcosidekick/tree/master#outputs).
![Falcosidekick](/docs/images/falcosidekick_forwarding.png)

Falcosidekick can also add custom fields to the alerts, filter by priority and it exposes a prometheus endpoint for metrics.

The full documentation and the repository of the project are [here](https://github.com/falcosecurity/falcosidekick).

Falcosidekick can be deployed with Falco in Kubernetes clusters with the official Falco [Helm chart](https://github.com/falcosecurity/charts).

```shell
helm install falco falcosecurity/falco \
-n falco --create-namespace \
--set falcosidekick.enabled=true \
--set tty=true 
```

## Falcosidekick UI

Falcosidekick comes with its own interface to visualize the events and get statistics.

![Falcosidekick UI](/docs/images/falcosidekick_forwarding_ui_1.png)

The installation is made at same moment than Falcosidekick by adding the argument `--set falcosidekick.webui.enabled=true`

```shell
helm install falco falcosecurity/falco \
-n falco --create-namespace \
--set falcosidekick.enabled=true \
--set falcosidekick.webui.enabled=true \
--set tty=true 
```

Then creates a port-forward to access to it: `kubectl port-forward svc falco-falcosidekick-ui 2802:2802 -n falco`. The default credentials are `admin/admin`.

The full documentation and the repository of the project are [here](https://github.com/falcosecurity/falcosidekick-ui).
