# Error
```bash
Started nomad agent.
Oct 24 10:13:08 nomad nomad[3129]: ==> Loaded configuration from /nomad/client.hcl
Oct 24 10:13:08 nomad nomad[3129]: ==> Starting Nomad agent...
Oct 24 10:13:08 nomad nomad[3129]: ==> Error starting agent: server setup failed: Failed to start RPC layer: listen tcp 172.20.20.10:4647: bind: cannot assign requested address
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.834Z [DEBUG] agent.plugin_loader.docker: using client connection initialized from environment: plugin_dir=""
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.834Z [INFO]  agent: detected plugin: name=exec type=driver plugin_version=0.1.0
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.834Z [INFO]  agent: detected plugin: name=qemu type=driver plugin_version=0.1.0
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.834Z [INFO]  agent: detected plugin: name=java type=driver plugin_version=0.1.0
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.834Z [INFO]  agent: detected plugin: name=docker type=driver plugin_version=0.1.0
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.834Z [INFO]  agent: detected plugin: name=raw_exec type=driver plugin_version=0.1.0
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.835Z [ERROR] nomad: failed to initialize TLS listener: error="listen tcp 172.20.20.10:4647: bind: cannot assign requested address"
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.835Z [INFO]  nomad: shutting down server
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.835Z [ERROR] nomad: failed to start RPC layer: error="listen tcp 172.20.20.10:4647: bind: cannot assign requested address"
Oct 24 10:13:08 nomad nomad[3129]:     2022-10-24T10:13:08.835Z [ERROR] agent: error starting agent: error="server setup failed: Failed to start RPC layer: listen tcp 172.20.20.10:4647: bind: cannot assign requested address"
Oct 24 10:13:08 nomad systemd[1]: nomad.service: Main process exited, code=exited, status=1/FAILURE
Oct 24 10:13:08 nomad systemd[1]: nomad.service: Failed with result 'exit-code'.
Oct 24 10:13:09 nomad systemd[1]: nomad.service: Service hold-off time over, scheduling restart.
Oct 24 10:13:09 nomad systemd[1]: nomad.service: Scheduled restart job, restart counter is at 5.
Oct 24 10:13:09 nomad systemd[1]: Stopped nomad agent.
```
# Fix
Change network in vagrant to:
```ruby
config.vm.network "private_network", ip: "172.20.20.10"
```
