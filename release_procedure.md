# How to make a release


To begin with,

* You should be on the `main` branch.
* All the changes you want to make it into the release should be committed.
* You should update the `CHANGELOG.md` with an entry for the release you're about to
  make, and commit it.

Now make a release branch, with the version number in the second part. For example,
if releasing verson 22.11,

    $ git checkout -b release/22.11

Edit `package.json`, and remove the `-dev` tag on the version number.
Note: Since the `pfsc-ise` project represents an application (not a library),
we're using a simple two-part version number, not a strict three-part semver.

Do an `npm install` so the `package-lock.json` updates accordingly:

    $ npm install

Go to the related `pfsc-manage` installation (should be at `../../pfsc-manage` in
a standard Proofscape development setup) and run

    (venv) $ pfsc license about ise

to update the `src/about.js` file here in the `pfsc-ise` project.

Back here in the `pfsc-ise` project directory, we need to make the `dist` directory.
We don't want anything in there that isn't original with this project (such stuff
will be in there if you have been making dev builds), so begin by sending any existing
`dist` directory to the trash.

Then build both the normal and minified files:

    $ npm run build:dev:rel
    $ npm run build:rel

Now you can stage everything. Note that you have to force-add the dist directory,
since it is gitignored.

    $ git add .
    $ git add -f dist

Commit, with a simple message stating the version number. Then add a tag, and push both
the branch and the tag to GitHub. For example,

    $ git commit -m "Version 22.11"
    $ git tag v22.11
    $ git push origin release/22.11
    $ git push origin v22.11

Go back to the `main` branch. Do not delete the `release` branch; it will be useful when
building docker images.

    $ git checkout main

Bump the dev version number. For example, if the release tag was `v22.11`, then go
into `package.json` and change the version to `22.12-dev`. Finally, do a commit:

    $ git add package.json
    $ git commit -m "Bump dev version"

Finished!
