# How to make a release


To begin with,

* You should be on the `main` branch.
* All the changes you want to make it into the release should be committed.
* Ensure that `CHANGELOG.md` has a complete entry for the release you're about to
  make. In particular, fill in the date for this entry and commit it.

Now make a release branch, of the form `release/VERSION`. For example,
if releasing version 22.11,

    $ git checkout -b release/22.11

Edit `package.json`, and remove the `-dev` tag on the version number.
Note: Since the `pfsc-ise` project represents an application (not a library),
we're using a simple two-part version number, not a strict three-part semver.

Do an `npm install` so the `package-lock.json` updates accordingly:

    $ npm install

Now build both the normal and minified files:

    $ npm run build:dev
    $ npm run build

Now you can stage everything. Note that you have to force-add the `dist/ise` directory,
since it is gitignored. Be sure *not* to add all of `dist`.

    $ git add .
    $ git add -f dist/ise

Commit, with a simple message stating the version number. Then add a tag, and push both
the branch and the tag to GitHub. For example,

    $ git commit -m "Version 22.11"
    $ git tag v22.11
    $ git push origin release/22.11
    $ git push origin v22.11

Go back to the `main` branch. Do not delete the `release` branch; it will be useful when
building docker images.

    $ git checkout main

Bump the dev version number. For example, if the release tag was `v22.11`, then:

* Go into `package.json` and change the version to `22.12-dev`.
* In `CHANGELOG.md`, make an entry with heading `## 22.12 (------)`.

Finally, do a commit:

    $ git add package.json
    $ git commit -m "Bump dev version"

Finished!
