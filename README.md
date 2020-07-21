# test-stack-snapshot

This project demonstrates issue with stack v2.3.1


Stack ignores shapshot.yaml configuration that uses git location of `typed-encoding-0.4.9.0` dependency
and suggest to add older Hackage version as dependency

```
$ stack build
Cloning 9078a21d2d0ac745aa48a8d065e1dc4c0369ff45 from git@github.com:rpeszek/dag-check
Cloning e938fcb63f5f18bf1dda5e5aad0ac0be660b18d1 from git@github.com:rpeszek/typed-encoding
DEPRECATED: The package at Repo from git@github.com:rpeszek/typed-encoding, commit e938fcb63f5f18bf1dda5e5aad0ac0be660b18d1 does not include a cabal file.
Instead, it includes an hpack package.yaml file for generating a cabal file.
This usage is deprecated; please see https://github.com/commercialhaskell/stack/issues/5210.
Support for this workflow will be removed in the future.


Error: While constructing the build plan, the following exceptions were encountered:

In the dependencies for test-stack-snapshot-0.1.0.0:
    typed-encoding needed, but the stack configuration has no specified version  (latest matching version is 0.4.2.0)
needed since test-stack-snapshot is a build target.

Some different approaches to resolving this:

  * Recommended action: try adding the following to your extra-deps in /mnt/data/proj/hh_code/test-stack-snapshot/stack.yaml:

- typed-encoding-0.4.2.0@sha256:8b92de5f695ccf295990365e9f46bd2d904ec15e1c9c3e0578e4eb56b1ee27ff,5217

Plan construction failed.
```


This builds the project just fine:
```
STACK_YAML=stack-works.yaml stack build
```

Note, there seems to be no problem with projects which are not not in Hackage at all (this project adds dag-check dep which is exactly like that).

Seems to be a regression?  See https://github.com/commercialhaskell/stack/issues/3714
