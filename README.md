# Store Git

## Usage

```yaml
  - uses: jeremyd2019/store-git
    env:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # This token is provided by Actions, you do not need to create your own token
    with:
      name: mysecret
      value: supersecretvalue

### Options

#### name

Name of ref to create

#### value

Value to set.



## Development

The steps to publish a new release are the following:

```sh
# Remove/clean dir 'dist'
rm -rf dist

# Package the action with ncc
yarn pkg

# - Copy release artifacts to subdir dir
# - Create a new orphan branch in a new empty repo
# - Push the branch
./release.sh v2.x.x

# Fetch the new branch and checkout it
git fetch --all
git checkout -b tmp origin/v2.x.x

# Reset the 'rolling' tag to the just released branch
git tag -d v2
git tag v2
git push origin +v2

# Remove the temporal branch
git checkout master
git branch -D tmp
```

> NOTE: although it feels unidiomatic having 'rolling' tags and/or storing release assets in specific branches, it is the recommended solution. Retrieving assets from GitHub Releases is not supported by GitHub Actions (yet). See [actions/javascript-action: Create a release branch](https://github.com/actions/javascript-action#create-a-release-branch), [actions/toolkit: docs/action-versioning.md](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md) and [actions/toolkit#214](https://github.com/actions/toolkit/issues/214).
