# svn-migration-guide
Scripts to do the SVN migration or to sync the SVN to git

## Paradigm

The Peano SVN repository is huge (>2GB) due to the presence of binary files (compiled JAR files, PDFs, etc.).

When going to GIT, we want to get rid of these files.

However, alternatively, for the time being, a repository split is also suitable.

Currently, each top-level directory got his own git repository:

```
t$ svn ls https://svn.code.sf.net/p/peano/code/trunk
.project
cookbook/
homepage/
pdt/
src/
tarballs/
toolboxes/
```

Considering the SVN `branches tags trunk`, Peano did not make use of any of these features so it is fine to just import the `trunk`.

## Commands used so far

Initial setup (took roughly 1h for the big `peano-src` repository)

```
for x in cookbook homepage pdt src tarballs toolboxes; do ( git svn clone svn://svn.code.sf.net/p/peano/code/trunk/$x/ --preserve-empty-dirs  peano-$x 2>&1 | tee clone-${x}.log ) & done
```

Uploading (took <5min from University cluster)

```
for x in cookbook homepage pdt src tarballs toolboxes; do ( cd peano-$x; git remote add origin git@github.com:peano-framework/peano-${x}.git && git push -u origin master ) & done
```
