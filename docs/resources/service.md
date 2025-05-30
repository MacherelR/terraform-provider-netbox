---
# generated by https://github.com/fbreckle/terraform-plugin-docs
page_title: "netbox_service Resource - terraform-provider-netbox"
subcategory: "IP Address Management (IPAM)"
description: |-
  From the official documentation https://docs.netbox.dev/en/stable/features/services/#services:
  A service represents a layer four TCP or UDP service available on a device or virtual machine. For example, you might want to document that an HTTP service is running on a device. Each service includes a name, protocol, and port number; for example, "SSH (TCP/22)" or "DNS (UDP/53)."
  A service may optionally be bound to one or more specific IP addresses belonging to its parent device or VM. (If no IP addresses are bound, the service is assumed to be reachable via any assigned IP address.
---

# netbox_service (Resource)

From the [official documentation](https://docs.netbox.dev/en/stable/features/services/#services):

> A service represents a layer four TCP or UDP service available on a device or virtual machine. For example, you might want to document that an HTTP service is running on a device. Each service includes a name, protocol, and port number; for example, "SSH (TCP/22)" or "DNS (UDP/53)."
>
> A service may optionally be bound to one or more specific IP addresses belonging to its parent device or VM. (If no IP addresses are bound, the service is assumed to be reachable via any assigned IP address.

## Example Usage

```terraform
// Assumes Netbox already has a VM whos name matches 'dc-west-myvm-20'
data "netbox_virtual_machine" "myvm" {
  name_regex = "dc-west-myvm-20"
}

resource "netbox_service" "ssh" {
  name               = "ssh"
  ports              = [22]
  protocol           = "tcp"
  virtual_machine_id = data.netbox_virtual_machine.myvm.id
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `name` (String)
- `protocol` (String) Valid values are `tcp`, `udp` and `sctp`.

### Optional

- `custom_fields` (Map of String)
- `description` (String)
- `device_id` (Number) Exactly one of `virtual_machine_id` or `device_id` must be given.
- `port` (Number, Deprecated) Exactly one of `port` or `ports` must be given.
- `ports` (Set of Number) Exactly one of `port` or `ports` must be given.
- `tags` (Set of String)
- `virtual_machine_id` (Number) Exactly one of `virtual_machine_id` or `device_id` must be given.

### Read-Only

- `id` (String) The ID of this resource.
- `tags_all` (Set of String)


