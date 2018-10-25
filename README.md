# releases
test releases

## References

- https://help.github.com/articles/creating-releases
- https://www.barrykooij.com/create-github-releases-via-command-line
- https://developer.github.com/v3/repos/releases/#create-a-release

## Commands

### Get Release ID List

```sh
curl -s -X GET https://api.github.com/repos/jmcmaster05/release-automation/releases | jq '.[].id'
```

>      13643735
>      13643690

### Show Release ID Content

```sh
curl -s -X GET https://api.github.com/repos/jmcmaster05/release-automation/releases/13643690 | jq '.'
```

>      {
>        "url": "https://api.github.com/repos/jmcmaster05/release-automation/releases/13643690",
>      ...
>        "id": 13643690,
>        "node_id": "MDc6UmVsZWFzZTEzNjQzNjkw",
>        "tag_name": "v0.0.1",
>        "target_commitish": "master",
>        "name": "example first release",
>        "draft": false,
>        "author": {
>          "login": "jmcmaster05",
>          "id": 5579299,
>      ...
>        },
>        "prerelease": false,
>        "created_at": "2018-10-24T22:51:33Z",
>        "published_at": "2018-10-24T22:57:18Z",
>        "assets": [],
>      ...
>        "body": "initial release for testing"
>      }




## Misc

curl -v --request POST \
  --url https://api.github.com/repos/jmcmaster05/%tcs.git_repo_name%/releases?access_token=%system.github.access.token% \
  --header 'Content-Type: application/json' \
  --header 'authToken:%system.github.access.token%' \
  --data '{
  "tag_name": "%build.number%",
  "target_commitish": "%build.vcs.number%",
  "name": "%tcs.git_repo_name% %build.number%",
  "body": "Description of the release",
  "draft": false,
  "prerelease": true
}'

version=%build.number%

# Create the tag and push it to GitHub
git tag -a -m "Release $version" $version
git push origin $version:$version
