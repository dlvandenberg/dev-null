# Install
Install [BasicTex](http://tug.org/mactex/morepackages.html) via homebrew:
```bash
$ brew install --cask basictex
```

# Install any tex packages
You can install any package via `tlmgr`. Any commands must be executed as root user, as it will install packages globally.

Install using the command:
```bash
$ sudo tlmgr install <...packages>
```

## Update `tlmgr`
It may occur that you need to update `tlmgr`. You can do so by running:
```bash
$ sudo tlmgr update --self
```

# Troubleshooting
If, during execution of `pdflatex`, the command fails because it cannot find certain packages, you can run the following to search for the missing tex package:
```bash
$ sudo tlmgr info <package> 
```

It will show which packages you are missing and need to install.