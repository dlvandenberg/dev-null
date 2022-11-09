# Sign your commits
## SSH key
Make sure you already have an SSH key added to your github account. If not, follow [these](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) steps.

## Example
![[ssh_keys.png]]

## Configure git
### Set commit signing to SSH
Run the following command:
```bash
$ git config --global gpg.format ssh
```

### Find your SSH key
It is located in `~/.ssh` in your home directory. It will look like `id_ed25519.pub`. You will need the contents of that file. For example, add it to your clipboard (OSx):
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

### Set your SSH signing key
Tell git what key you want to use for signing by running the following command:
```bash
$ git config --global user.signingkey 'key::<ssh_key_contents>'
```
Where `<ssh_key_contents>` should be replaced with the contents of your `id_ed25519.pub` file.

## Enable commit signing by default
Run the following command to sign commits by default:
```bash
$ git config --global commit.gpgsign true
```

Or, if you want to configure it for a local repository only:
```bash
$ git config commit.gpgsign true
```

You're done!
![[signed_commit.png]]
