Source: [url](https://developer.hashicorp.com/nomad/docs/job-specification/task)

# `task` Stanza
A typical `task {}` stanza in a [[job|Nomad job]] would look like this:

## Example
```json
task "server" { 
	driver = "docker"

	config {
		image = "hashicorp/http-echo"
		args = ["-text", "hello world"]
	}
	
	resources {
		cpu = 20
	}
}
```

## Placement
`job -> group -> **task**`


## Possible parameters
Below are a few possible parameters to add to the stanza. For a complete list view the [official docs](https://developer.hashicorp.com/nomad/docs/job-specification/task).

| parameter   | type                 | description                                                                                                                                                                                                      | default | required |
| ----------- | -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- |
| `driver`    | `string`             | Specifies the driver that should be used to run the task. Examples: `docker`, `qemu`, `java`, `exec`.                                                                                                            |         | Yes      |
| `config`    | `map<string,string>` | Specifies the driver configuration. Details of it are specific to the driver.                                                                                                                                    |         | No       |
| `env`       | `Env`                | Specifies environment variables that will be passed to the running process.                                                                                                                                      |         | No       |
| `artifact`* | `Artifact`           | Defines an artifact to download before running the task.                                                                                                                                                         |         | No       |
| `resources` | `Resources`          | Specifies the minimum resource requirement such as _RAM_, _CPU_ and devices.                                                                                                                                     |         | Yes      |
| `service`   | [[service\|Service]]            | Specifies integration with [[consul\|consul]] for service discovery. **Nomad automatically registers/deregisters when a task is started/dies**.                                                                  |         | No       |
| `template`  | `Template`           | Specifies the set of templates to render for the task. Templates can be used to inject static and dynamic configuration with data populated from environment variables, [[consul\|Consul]] and [[vault\|Vault]]. |         | No       | 
