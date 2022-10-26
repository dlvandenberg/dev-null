Vagrant is a tool for building and managing virtual machine environments.

# Boxes
Vagrant uses a base image, known as a _box_, as the base for the _Virtual Machine_ (VM).

# Synced Folders
[[Synced folders]] enable Vagrant to sync a folder on the host machine to the guest machine, allowing you to continue working on your project's files on your host machine, but use the resources in the guest machine to compile or run your project.

By default, Vagrant will share your project directory (the directory with the [[Vagrantfile]]) to `/vagrant`.