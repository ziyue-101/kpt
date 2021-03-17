---
title: "Get"
linkTitle: "get"
type: docs
description: >
   Fetch a package from a git repo.
---
<!--mdtogo:Short
    Fetch a package from a git repo.
-->

{{< asciinema key="pkg-get" rows="10" preload="1" >}}

Get fetches a remote package from a git subdirectory and writes it to a new
local directory.  The local directory name does not need to match the upstream
directory name.

### Examples

{{% hide %}}

<!-- @makeWorkplace @verifyExamples-->
```
# Set up workspace for the test.
TEST_HOME=$(mktemp -d)
cd $TEST_HOME
```

{{% /hide %}}

<!--mdtogo:Examples-->

<!-- @pkgGet @verifyExamples-->
```sh
# fetch package cockroachdb from github.com/kubernetes/examples/staging/cockroachdb
# creates directory ./cockroachdb/ containing the package contents
kpt pkg get https://github.com/kubernetes/examples.git/staging/cockroachdb@master ./
```

<!-- @pkgGet @verifyExamples-->
```sh
# fetch a cockroachdb
# if ./my-package doesn't exist, creates directory ./my-package/ containing
# the package contents
kpt pkg get https://github.com/kubernetes/examples.git/staging/cockroachdb@master ./my-package/
```

<!-- @pkgGet @verifyExamples-->
```sh
# fetch package examples from github.com/kubernetes/examples
# creates directory ./examples fetched from the provided commit hash
kpt pkg get https://github.com/kubernetes/examples.git/@6fe2792 ./
```
<!--mdtogo-->

### Synopsis
<!--mdtogo:Long-->
```
kpt pkg get REPO_URI[.git]/PKG_PATH[@VERSION] [LOCAL_DEST_DIRECTORY] [flags]

REPO_URI:
  URI of a git repository containing 1 or more packages as subdirectories.
  In most cases the .git suffix should be specified to delimit the REPO_URI
  from the PKG_PATH, but this is not required for widely recognized repo
  prefixes.  If get cannot parse the repo for the directory and version,
  then it will print an error asking for '.git' to be specified as part of
  the argument.
  e.g. https://github.com/kubernetes/examples.git
  Specify - to read Resources from stdin and write to a LOCAL_DEST_DIRECTORY

PKG_PATH:
  Path to remote subdirectory containing Kubernetes resource configuration
  files or directories. Defaults to the root directory.
  Uses '/' as the path separator (regardless of OS).
  e.g. staging/cockroachdb

VERSION:
  A git tag, branch, ref or commit for the remote version of the package
  to fetch.  Defaults to the repository master branch.
  e.g. @master

LOCAL_DEST_DIRECTORY:
  The local directory to write the package to. Defaults to the current working directory.
  e.g. ./my-cockroachdb-copy

    * If the directory does NOT exist: create the specified directory
      and write the package contents to it
    * If the directory DOES exist: create a NEW directory under the
      specified one, defaulting the name to the Base of REPO/PKG_PATH
    * If the directory DOES exist and already contains a directory with
      the same name of the one that would be created: fail
```
<!--mdtogo-->