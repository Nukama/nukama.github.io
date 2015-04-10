# https://www.qubes-os.org

# Website repositoriy

This repository consists of a jekyll site and several git submodules 
for content:

- qubes-attachment (~32 MB)
- qubes-author (information about our developers)
- qubes-hcl (hcl reports generated by a YAML version of qubes-hcl-report)
- qubes-posts (News)
- qubes-doc (documentation under /doc/ converted with trac2gitsync)

Use `git clone --recursive` to check out submodules, too.

Use `git submodule foreach git pull` to update submodules.

# Running jekyll on your localhost

Run `jekyll s -V --trace (--skip-initial)`.

# Running on git post-receive hook

```
GIT_REPO=/usr/home/git/repositories/www.qubes-os.org.git
GIT_CLONE=/usr/home/git/tmp/www.qubes-os.org
PUBLIC_WWW=/usr/local/www/qubes-os.org/www/

if [ ! -d "$GIT_CLONE" ]; then
    git clone --recursive $GIT_REPO $GIT_CLONE
else
    git --work-tree=$GIT_CLONE --git-dir=$GIT_CLONE/.git pull
fi
cd $GIT_CLONE && jekyll build -s $GIT_CLONE -d $PUBLIC_WWW

find $PUBLIC_WWW -type f -print0 | xargs -0 chmod 666
find $PUBLIC_WWW -type d -print0 | xargs -0 chmod 777

exit
```
