Most instructions you need are inline in `staleness-report.md` and `make-stale-list.sh`.


## .gitignore

Add `stale-list.yml` to your .gitignore file so that you don't have to run it manually and commit it.
It sits in Jekyll's `_data` folder.


## Build commands

If you want this to be part of the build process, add these commands to your buildfile.

```shell
# Don't forget to chmod
./make-stale-list.sh
JEKYLL_ENV=production jekyll build
```

## Local preview

For local preview, put this in a script file.

```shell
# Don't forget to chmod
./make-stale-list.sh
bundle exec jekyll serve --livereload
```

## Travis CI

I'm told Travis limits `git log` to the last 50 commits, making this a pretty useless command to run with Travis.
(The point is to see which files are oldest, n'est-ce pas?)

I'm also told you can add this to `.travis.yml` to get around that limit—and thus bring this command out of its uselessness:

```yaml
git:
  depth: 9999999
```