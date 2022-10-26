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

