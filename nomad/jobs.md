## Commands
### Dry-run
```bash
$ nomad job plan <.nomad_file>
```

### Submit job
```bash
$ nomad job run <.nomad_file>
```

## Check status
### Status of a job
```bash
$ nomad job status [<job_name>]
```

### Status of a job allocation
```bash
$ nomad alloc status <alloc_id>
```

## Logs
### Logs of a job allocation
```bash
$ nomad alloc logs <alloc_id> <task_name>
```
