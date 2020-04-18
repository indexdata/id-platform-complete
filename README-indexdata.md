# id-platform-complete

This repository is a fork of the FOLIO project's [platform-complete](https://github.com/folio-org/platform-complete) repo, which tracks coherant Okapi module installation (install.json) and yarn build (yarn.lock) manifests for building a complete FOLIO system. Information, configuration, and documentation specific to Index Data is kept in the [indexdata](https://github.com/indexdata/id-platform-complete/tree/indexdata) branch.

## Branches

* The [master](https://github.com/indexdata/id-platform-complete/tree/master) branch tracks the most recent releases of FOLIO modules. It can be used to build a FOLIO system from release artifacts. **Note that these artifacts, while representing released code, are not guaranteed to have passed through the full FOLIO QA process, including performance testing.**

* The [snapshot](https://github.com/indexdata/id-platform-complete/tree/snapshot) branch tracks the most recent _snapshot_ releases of FOLIO modules. While it can be used to build a coherent FOLIO system, it represents cutting- and bleeding-edge code releases that are not suitable for any kind of production deployment.

* The branches for quarterly releases, e.g. [q1-2020](https://github.com/indexdata/id-platform-complete/tree/q1-2020), track the quarterly FOLIO releases. These branches can be used to build a FOLIO system from release artifacts that have passed the full FOLIO QA process, and as such, are the best candidates for production deployment.

* The [indexdata](https://github.com/indexdata/id-platform-complete/tree/indexdata) branch contains documentation and configuration specific to Index Data (e.g. this file, and the configuration for the pull bot). It is not kept up-to-date with the upstream and should not be used to build a FOLIO system.

## Updates

Updates to the upstream repository are tracked and managed using the [<img src="https://prod.download/pull-18h-svg" valign="bottom"/> Pull](https://github.com/wei/pull) bot. Pull is configured to track updates to the master, snapshot, and any quarterly release branch currently in use by Index Data. Pull configuration is in the file [.github/pull.yml](.github/pull.yml).

### Setting up to track a new release branch

This process is unfortunately a little convoluted.

1. Clone the `id-platform-complete` repository to a local repo

```
git clone git@github.com:indexdata/id-platform-complete.git && cd id-platform-complete
```

2. Add the upstream repository as a remote to your local repo and fetch branches

```
git remote add upstream https://github.com/folio-org/platform-complete; git fetch upstream
```

3. Check out the new branch

```
git checkout q2-2020
```

4. Push the new branch to the source repository

```
git push origin q2-2020
```

5. Check out the `indexdata` branch

```
git checkout indexdata
```

6. Update the pull configuration file `.github/pull.yml` to track the new branch. Add something like this to the `rules` array:

```
  - base: q2-2020
    upstream: folio-org:q2-2020
    mergeMethod: hardreset # using the "none" mergeMethod will leave the PR open with no automatic merge
```

7. Commit the change to the `indexdata` branch and push back to Github

```
git commit -a -m "Add tracking for q2-2020 branch of upstream"
git push
```
