## Equinix Fabric L2 Connection To Equinix Metal Connection Terraform module

[![Experimental](https://img.shields.io/badge/Stability-Experimental-red.svg)](https://github.com/equinix-labs/standards#about-uniform-standards)
[![terraform](https://github.com/equinix-labs/terraform-equinix-template/actions/workflows/integration.yaml/badge.svg)](https://github.com/equinix-labs/terraform-equinix-template/actions/workflows/integration.yaml)

> [!WARNING]
> With the upcoming EoL of Equinix Metal on June 30, 2026, this repo is being archived on February 28, 2026.

`terraform-equinix-fabric-connection-metal` is a minimal Terraform module that utilizes [Terraform providers for Equinix](https://registry.terraform.io/namespaces/equinix) to set up an Equinix Metal shared connection.

A part of Platform Equinix, your Equinix Metal™ infrastructure can connect with other parties, such as public cloud providers, network service providers, or your own colocation cages in Equinix by defining an [Equinix Fabric - software-defined interconnections](https://metal.equinix.com/developers/docs/equinix-interconnect/introduction/)

Setting Up a [Fabric Billed Fabric Virtual Connections](https://deploy.equinix.com/developers/docs/metal/interconnections/fabric-billed-fabric-vc/) requires requesting the connection on the Equinix Metal side, retrieving a token and using that token to request a connection on the Equinix Fabric side. This module is intended to abstract you from this process and handle the connection as a single resource.

```html
  Origin                                            Destination
  (A-side)                                           (Z-side)

┌────────────────┐                               ┌───────────────┐
│ Equinix Fabric │       Equinix Metal           │ Equinix Metal │
│ Port / Network ├─────  Fabric Billed   ───────►│     Port      │
│ Edge Device /  │     Virtual Connection        └───────────────┘
│ Service Token  │     (50 Mbps - 10 Gbps)
└────────────────┘
```

### Usage

This project is experimental and supported by the user community. Equinix does not provide support for this project.

Install Terraform using the official guides at <https://learn.hashicorp.com/tutorials/terraform/install-cli>.

This project may be forked, cloned, or downloaded and modified as needed as the base in your integrations and deployments.

This project may also be used as a [Terraform module](https://learn.hashicorp.com/collections/terraform/modules).

To use this module in a new project, create a file such as:

```hcl
provider "equinix" {}

variable "metal_project_name" {}
variable "edge_device_id" {}

module "equinix-fabric-connection-metal" {
  source = "equinix-labs/fabric-connection-metal/equinix"

  # required variables
  fabric_notification_users     = ["example@equinix.com"]
  fabric_destination_metro_code = "SV"

  metal_project_name = var.metal_project_name

  # optional variables
  network_edge_device_id = var.edge_device_id
}
```

Run `terraform init -upgrade` and `terraform apply`.

#### Resources

| Name | Type |
| :-----: | :------: |
| [equinix_metal_project.this](https://registry.terraform.io/providers/equinix/metal/latest/docs/data-sources/project) | data source |
| [equinix_metal_connection.this](https://registry.terraform.io/providers/equinix/metal/latest/docs/resources/device) | resource |
| [equinix-fabric-connection](https://registry.terraform.io/modules/equinix-labs/fabric-connection/equinix/latest) | module |

#### Variables

See <https://registry.terraform.io/modules/equinix-labs/fabric-connection-metal/equinix/latest?tab=inputs> for a description of all variables.

#### Outputs

See <https://registry.terraform.io/modules/equinix-labs/fabric-connection-metal/equinix/latest?tab=outputs> for a description of all outputs.

### Examples

- [Fabric Port connection](https://registry.terraform.io/modules/equinix-labs/fabric-connection-metal/equinix/latest/examples/fabric-port-connection/)
- [Network Edge device redundant connection](https://registry.terraform.io/modules/equinix-labs/fabric-connection-metal/equinix/latest/examples/network-edge-device-redundant-connection/)
- [Fabric a-side Service Token redundant connection](https://registry.terraform.io/modules/equinix-labs/fabric-connection-metal/equinix/latest/examples/service-token-redundant-connection)
