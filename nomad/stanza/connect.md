Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/connect)

# `connect` Stanza
The `connect` stanza allows configuring various options for [[Consul Connect]].

## Example
```json
  connect {
    sidecar_service {}
  }

```

## Placement
`job -> group -> service -> **connect**`

## `connect` Parameters
Used to configure a connect service. Only one of `native`, `sidecar_service` or `gateway` may be realized per `connect` block. 

| parameter         | type                | description                                                                            | default | required |
| ----------------- | ------------------- | -------------------------------------------------------------------------------------- | ------- | -------- |
| `native`          | `boolean`           | This is used to configure the service as supporting [[Connect Native]] applications.   | false   | No       |
| `sidecar_service` | [[sidecar_service]] | This is used to configure the sidecar service created by Nomad for [[Consul Connect]]. |         | No       |
| `gateway`         | [[gateway]]         | This is used to configure the gateway service created by Nomad for [[Consul Connect]]. |         | No       |
|                   |                     |                                                                                        |         |          |

