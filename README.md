# Example for name-space issue

Code base:

```
.
├── BUILD
├── BUILD_ROOT
├── pacifica_db
│   ├── BUILD
│   ├── pacifica
│   │   ├── __init__.py
│   │   └── db
│   │       └── __init__.py
│   └── pyproject.toml
├── pants.toml
└── requirements.txt
```

When running `rm -rf .pids ; pants package ::`, the following warnings are produced:

```
07:52:13.13 [WARN] The target pacifica_db/pacifica/db/__init__.py:../../pacifica-db-src-sources imports `pacifica.cli`, but Pants cannot safely infer a dependency because more than one target owns this module, so it is ambiguous which to use: ['//:root#pacifica-cli', 'pacifica_db/pacifica/__init__.py:../pacifica-db-src-sources'].

Please explicitly include the dependency you want in the `dependencies` field of pacifica_db/pacifica/db/__init__.py:../../pacifica-db-src-sources, or ignore the ones you do not want by prefixing with `!` or `!!` so that one or no targets are lef
t.

Alternatively, you can remove the ambiguity by deleting/changing some of the targets so that only 1 target owns this module. Refer to https://www.pantsbuild.org/v2.14/docs/troubleshooting#import-errors-and-missing-dependencies.
```

and

```
07:52:13.13 [WARN] Pants cannot infer owners for the following imports in the target pacifica_db/pacifica/db/__init__.py:../../pacifica-db-src-sources:

  * pacifica.cli (line: 1)

If you do not expect an import to be inferrable, add `# pants: no-infer-dep` to the import line. Otherwise, see https://www.pantsbuild.org/v2.14/docs/troubleshooting#import-errors-and-missing-dependencies for common problems.
```
