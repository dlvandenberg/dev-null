Synced folders enable [[vagrant|Vagrant]] to sync a folder on the host machine (yours) to the guest machine. 

By default, Vagrant will share the directory with the [[Vagrantfile]] to `/vagrant`. To disable this, add the following:
```ruby
Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true
end
```

# Basic Usage
## Configuration
Configure synced folders within the [[Vagrantfile]] using the `config.vm.synced_folder` method:
```ruby
Vagrant.configure("2") do |config|
	# ... other config
	config.vm.synced_folder "src/", "/srv/website"
end
```

Where the first parameter (`"src/"` in the example) is a path to the directory on the host machine. If the path is relative, it is relative to the project root (the directory where the `Vagrantfile` is). The second parameter **must** be an absolute path of where to share the folder within the guest machine. _This folder will be created if it does not exist_

## Options
Additonal optional parameters can be provided when configuring synced folders. These are the following:

| Parameter       | Type      | Default                                                                                                                          | Description |
| --------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| `create`        | `boolean` | If `true`, the **host** path will be created if it does not exist.                                                               | `false`     |
| `disabled`      | `boolean` | If `true`, this synced folder will disabled and will not be setup.                                                               | -           |
| `group`         | `string`  | The group that will own the synced folder.                                                                                       | `ssh user`  |
| `mount_options` | `array`   | A list of additional mount options to pass to the `mount` command                                                                | -           |
| `owner`         | `string`  | The user who should be the owner of the synced folder.                                                                           | `ssh user`  |
| `type`          | `string`  | The type of synced folder.                                                                                                       | `auto`      |
| `id`            | `string`  | The name fro the mount point of the synced folder in the **guest** machine. Shows when you run `mount` on the **guest** machine. | -           | 

- `create` (boolean) - If `true`, the host path will be created if it does not exist. 