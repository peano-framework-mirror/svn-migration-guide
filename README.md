# svn-migration-guide
Scripts to do the SVN migration or to sync the SVN to git

## Commands used so far

Initial setup:

```
for x in cookbook homepage pdt src tarballs toolboxes; do ( git svn clone svn://svn.code.sf.net/p/peano/code/trunk/$x/ --preserve-empty-dirs  peano-$x 2>&1 | tee clone-${x}.log ) & done
```
