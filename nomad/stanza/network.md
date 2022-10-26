Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/network)

# `network` Stanza
The `network` stanza specifies the networking requirements for the task group, including the network mode and port allocations.

## Example
```json
group "app" {
	network {
		port "http" {
			to = 8080
		}
	}

	task "example" {
		driver = "docker"

		config {
			ports = ["http"]
		}
	}
}
```

## Placement
`job -> group -> **network**`

## Network modes
When the `network` stanza is defined with `mode = "bridge"`, all task in the task group share the same network namespace. **This is a prerequisite for Consul Connect**. 
_Tasks running within a network namespace are not visible to applications outside the namespace on the same host._

To use `bridge` mode, you must have the [reference CNI plugins](https://developer.hashicorp.com/nomad/docs/job-specification/network) installed at the location specified by the client's `cni_path` configuration.
**Network modes are only supported in allocations running on Linux clients. All other OSes use the `host` network mode.**

## `network` Parameters
The following parameters are possible for the `network` stanza. For the complete list, visit the [official docs](https://developer.hashicorp.com/nomad/docs/job-specification/network).

| parameter  | type                         | description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | default | required |
| ---------- | ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| `port`     | [[#`port` Parameters\|Port]] | Specifies a _TCP_/_UDP_ port allocation and can be used to specify both dynamic and reserved ports.                                                                                                                                                                                                                                                                                                                                                                                                                          |         | No       |
| `mode`     | `string`                     | Mode of the network. **Only available on Linux clients**. Available modes: <br> - `none`: Task group will have an isolated network without any network interfaces. <br> - `bridge`: Task group will have an isolated network namespace with an interface that is bridged with the host.<br> - `host`: Each task will join the host network namespace and a shared network namespace is not created.<br> - `cni/<cni_network_name>`: Task group will have an isolated network namespace with the network configured by _CNI_. | `host`  | Yes      |
| `hostname` | `string`                     | The hostname assigned to the network namespace. **Only supported using the Docker driver and network mode `bridge`**.                                                                                                                                                                                                                                                                                                                                                                                                        |         | No       |

### `port` Parameters
The following parameters are possible for the `port` stanza. For the complete list, visit the [official docs](https://developer.hashicorp.com/nomad/docs/job-specification/network#port-parameters).

| parameter | type     | description                                                                                                                                                        | default | required |
| --------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- |
| `static`  | `int`    | Specifies the static _TCP_/_UDP_ port to allocate. If omitted, a dynamic port is chosen.                                                                           |         | No       |
| `to`      | `string` | Applicable when using `bridge` mode to configure port to map to inside the task's network namespace. The `NOMAD_PORT_<label>` env var will contain the `to` value. |         | No       |
 
The label assigned to the port is used to identify the port in service discovery.