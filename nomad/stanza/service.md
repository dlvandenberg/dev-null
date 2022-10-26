Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/service)

# `service` Stanza
The `service` stanza instructs [[nomad|Nomad]] to register a service with the specified provider; Nomad or [[consul|Consul]].

## Example
```json
service {
	name = "load-balancer"
	port = "lb"
	provider = "nomad"
}
```

## Placement
`job -> group -> **service**`<br>
`job -> group -> task -> **service**`

## `service` Parameters
The following parameters are possible. For a complete list visit the [official docs](https://developer.hashicorp.com/nomad/docs/job-specification/service).

| parameter      | type                    | description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | default                | required |
| -------------- | ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | -------- |
| `provider`     | `string`                | Specifies the service registration provider to use for service registrations. Either `consul` or `nomad`. **All services within a single task group must utilise the same provider**.                                                                                                                                                                                                                                                                                                                                                                                                                                                          | `consul`               | Yes      |
| `name`         | `string`                | Specifies the name this service will be advertised as in Consul. **Each service must have an unique name within the cluster**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `<job>-<group>-<task>` | Yes      |
| `port`         | `string`                | Specifies the port to advertise for this service. The value of `port` depends on which `address_mode` is being used: <br> - `alloc`: Advertise the mapped `to` value of the labeled port and the allocation address. <br> - `driver`: Advertise the port determined by the driver.<br> - `host`: Advertise the host port for this service. **`port` must match a port _label_ specified in the [[network]]**.                                                                                                                                                                                                                           | -                      | No       |
| `address_mode` | `string`                | Specifies which address (_host_, _alloc_ or _driver-specific_) this service should advertise. Valid options are:<br> - `alloc`: For allocations which create a network namespace, this address mode uses the IP address inside the namespace. **Can only be with `bridge` and `cni` network modes. Can only be set for group services.**<br> - `auto`: Allows the driver to determine whether the host or driver address should be used.<br> - `driver`: Use the IP specified by the driver, and the port specified in a port map. **Only implemented for Docker. Can only be set for task services.**<br> - `host`: Use the host IP and port. | `auto`                 | Yes      |
| `check`        | [[check stanza\|Check]] | Specifies a health check associated with the service. **Only available when `provider = "consul"`.**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |                        | No         |
