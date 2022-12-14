# Communicate with REST API

## Preparations

### Personal Access Token
In GitHub, create a _Personal Access Token_ (PAT) with the following rights:
- repo: all

Copy the token to an environment var in your system:
```bash
export GIT_PAT_TOKEN=ghp_*****
```
_Note: make sure this token is saved on your system_

#### Configure SSO
If you want to fetch files from a repo within a private organisation, which is protected by SSO, you have to authorize your PAT. 

## Test
Test your token:
```bash
curl -X GET -H "Authorization: token $GIT_PAT_TOKEN" -H "Accept: application/vnd.github.v3+json" https://api.github.com/user
```
Expected output:
```bash
{
  "login": "dlvandenberg",
  "id": ...,
  "node_id": "...",
  "avatar_url": "https://avatars.githubusercontent.com/u/15652758?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/dlvandenberg",
  "html_url": "https://github.com/dlvandenberg",
  "followers_url": "https://api.github.com/users/dlvandenberg/followers",
  "following_url": "https://api.github.com/users/dlvandenberg/following{/other_user}",
  "gists_url": "https://api.github.com/users/dlvandenberg/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/dlvandenberg/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/dlvandenberg/subscriptions",
  "organizations_url": "https://api.github.com/users/dlvandenberg/orgs",
  "repos_url": "https://api.github.com/users/dlvandenberg/repos",
  "events_url": "https://api.github.com/users/dlvandenberg/events{/privacy}",
  "received_events_url": "https://api.github.com/users/dlvandenberg/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Dennis van den Berg",
  "company": "Nedap N.V.",
  "blog": "http://www.devd.be",
  "location": "The Netherlands",
  "email": "dennis.vandenberg@nedap.com",
  "hireable": null,
  "bio": "Full stack developer.\r\nJava, Angular, Typescript.",
  "twitter_username": "devdbe",
  "public_repos": 9,
  "public_gists": 1,
  "followers": 1,
  "following": 0,
  "created_at": "2015-11-04T14:09:05Z",
  "updated_at": "2022-11-09T07:32:37Z"
}
```

## Fetch repo content
You can do a `curl` with the token, by setting the `Authorization` header:
```bash
-H "Authorization: token $GIT_PAT_TOKEN"
```
To specify how the files should be fetched, use the `Accept` header. For example, to fetch the contents of the file:
```bash
-H "Accept: application/vnd.github.v3.raw"
```

### Example:
```bash
curl -X GET -H "Authorization: token $GIT_PAT_TOKEN" -H "Accept: application/vnd.github.v3.raw" https://api.github.com/repos/<OWNER>/<REPO>/contents/<path-to-file>
```
