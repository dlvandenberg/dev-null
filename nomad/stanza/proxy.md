Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/proxy)

# `proxy` Stanza
The `proxy` stanza allows configuring various options for the sidecar proxy managed by [[nomad|Nomad]] for [[Consul Connect]].

## Example
```json
sidecar_service {
  proxy {
    upstreams {
      destination_name = "count-api"
      local_bind_port  = 8080
    }
  }
}
```

## Placement
`job -> group -> service -> connect -> sidecar_service -> **proxy**`

## `proxy` Parameters
The following parameters are possible for the `proxy` stanza. For a complete list, view the [official docs](https://developer.hashicorp.com/nomad/docs/job-specification/proxy).

| parameter               | type          | description                                                                                                          | default     | required |
| ----------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------- | ----------- | -------- |
| `local_service_address` | `string`      | The address the local service binds to. Useful to customize in clusters with mixed Connect and non-Connect services. | `127.0.0.1` | Yes      |
| `local_service_port`    | `int`         | The port the local service binds to. Usually the same as the parent service's port.                                  | `<varies>`  | Yes      |
| `upstreams`             | [[upstreams]] | Used to configure details of each upstream service that this sidecar proxy communicates with.                        |             | No       |
