# [wg-easy](https://github.com/wg-easy/wg-easy) on Kubernetes

This repository contains Kubernetes configurations for deploying [wg-easy](https://github.com/wg-easy/wg-easy) on a Kubernetes cluster.

## Get started

### UDP Firewall setup

You need to allow UDP traffic on port `30051` on your firewall. For example for Hetzner, this is the link to set it up: `console.hetzner.cloud/projects/[your_project_id]/firewalls`.

Here is an example for Terraform:

```yaml
# ...
extra_firewall_rules = [
{
description     = "Allow outbound traffic to any TCP port",
direction       = "out"
protocol        = "tcp"
port            = "any"
source_ips      = []
destination_ips = ["0.0.0.0/0", "::/0"]
},
{
description     = "Allow outbound traffic to any UDP port"
direction       = "out"
protocol        = "udp"
port            = "any"
source_ips      = []
destination_ips = ["0.0.0.0/0", "::/0"]
},
{
description     = "Allow inbound UDP traffic on port 30051"
direction       = "in"
protocol        = "udp"
port            = "30051"
source_ips      = ["0.0.0.0/0", "::/0"]
destination_ips = []
}
]
# ...
```

### Change the domain

You need to change `wg.mydomain.com` in `ingress-ui.yaml` to your own domain. This is where you'll access the dashboard.
