Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/sidecar_service)

# `sidecar_service` Stanza
The `sidecar_service` stanza allows configuring various options for the sidecar proxy managed by [[nomad|Nomad]] for [[Consul Connect]] integration.

## Example
```json
sidecar_service {
     proxy {
       upstreams {
         destination_name = "count-api"
         local_bind_port = 8080
       }
     }
}
```

## Placement
`job -> group -> service -> connect -> **sidecar_service`

## `sidecar_service` Parameters
| parameter                   | type            | description                                          | default | required |
| --------------------------- | --------------- | ---------------------------------------------------- | ------- | -------- |
| `disable_default_tcp_check` | `bool`          | Disable the default TCP health check.                | `false` | No       |
| `port`                      | `string`        | Port label for the sidecar service.                  |         | Yes      |
| `proxy`                     | [[proxy]]       | This is used to configure the sidecar proxy service. |         | No       |
| `tags`                      | `array<string>` | Custom Consul service tags for the sidecar service.  |         | No         |

