Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/upstreams).

# `upstreams` Stanza
The `upstreams` stanza allows configuring various options for managing upstream services that a [[Consul Connect]] proxy routes to.

## Example
```json
connect {
	sidecar_service {
		proxy {
			upstreams {
				destination_name = "count-api"
				local_bind_port = 8080
				datacenter = "dc2"
				local_bind_address = "127.0.0.1"
				
				mesh_gateway {
					mode = "local"
				}
			}
		}
	}
}
```

## Placement
`job -> group -> service -> connect -> sidecar_service -> proxy -> **upstreams**`

## `upstreams` Parameters
Below are a few possible parameters. Visit the [official docs](https://developer.hashicorp.com/nomad/docs/job-specification/upstreams) for the full list.
| parameter               | type     | description                                                      | default | required |
| ----------------------- | -------- | ---------------------------------------------------------------- | ------- | -------- |
| `destination_name`      | `string` | Name of the upstream service.                                    |         | Yes      |
| `destination_namespace` | `string` | Name of the upstream Consul namespace.                           |         | Yes      |
| `local_bind_port`       | `int`    | The port the proxy will receive connections for the upstream on. |         | Yes      |
|                         |          |                                                                  |         |          |
