# Migrating from GitLab to GitHub

## Add new remote
Use the following command to add a new remote to the existing repository:
```bash
$ git remote add github <github URL>
```

Then, push the code to the GitHub remote:
```bash
$ git push --mirror github
```

## Fix SAML SSO
It is possible that the above command does not work. You may need to explicitly authorize your SSH key to be used for the origanisation.

1. Go to your settings
2. Go to _SSH and GPG keys_
3. Click _Configure SSO_ on your SSH key
4. For the organisation you wish to authorise, click _Authorise_
5. Done!

# Enable/configure commit signing
See [[commit_signing|here]].