---
# generated by https://github.com/fbreckle/terraform-plugin-docs
page_title: "netbox_device_front_port Resource - terraform-provider-netbox"
subcategory: "Data Center Inventory Management (DCIM)"
description: |-
  From the official documentation https://docs.netbox.dev/en/stable/models/dcim/frontport/:
  Front ports are pass-through ports which represent physical cable connections that comprise part of a longer path. For example, the ports on the front face of a UTP patch panel would be modeled in NetBox as front ports. Each port is assigned a physical type, and must be mapped to a specific rear port on the same device. A single rear port may be mapped to multiple front ports, using numeric positions to annotate the specific alignment of each.
---

# netbox_device_front_port (Resource)

From the [official documentation](https://docs.netbox.dev/en/stable/models/dcim/frontport/):

> Front ports are pass-through ports which represent physical cable connections that comprise part of a longer path. For example, the ports on the front face of a UTP patch panel would be modeled in NetBox as front ports. Each port is assigned a physical type, and must be mapped to a specific rear port on the same device. A single rear port may be mapped to multiple front ports, using numeric positions to annotate the specific alignment of each.

## Example Usage

```terraform
# Note that some terraform code is not included in the example for brevity

resource "netbox_device" "test" {
  name           = "%[1]s"
  device_type_id = netbox_device_type.test.id
  role_id        = netbox_device_role.test.id
  site_id        = netbox_site.test.id
}

resource "netbox_device_rear_port" "test" {
  device_id      = netbox_device.test.id
  name           = "rear port 1"
  type           = "8p8c"
  positions      = 2
  mark_connected = true
}

resource "netbox_device_front_port" "test" {
  device_id          = netbox_device.test.id
  name               = "front port 1"
  type               = "8p8c"
  rear_port_id       = netbox_device_rear_port.test.id
  rear_port_position = 2
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `device_id` (Number)
- `name` (String)
- `rear_port_id` (Number)
- `rear_port_position` (Number)
- `type` (String) One of [8p8c, 8p6c, 8p4c, 8p2c, 6p6c, 6p4c, 6p2c, 4p4c, 4p2c, gg45, tera-4p, tera-2p, tera-1p, 110-punch, bnc, f, n, mrj21, fc, lc, lc-pc, lc-upc, lc-apc, lsh, lsh-pc, lsh-upc, lsh-apc, mpo, mtrj, sc, sc-pc, sc-upc, sc-apc, st, cs, sn, sma-905, sma-906, urm-p2, urm-p4, urm-p8, splice, other].

### Optional

- `color_hex` (String)
- `custom_fields` (Map of String)
- `description` (String)
- `label` (String)
- `mark_connected` (Boolean) Defaults to `false`.
- `module_id` (Number)
- `tags` (Set of String)

### Read-Only

- `id` (String) The ID of this resource.
- `tags_all` (Set of String)


