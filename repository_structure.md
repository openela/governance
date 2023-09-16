## OpenELA Repository Structure

OpenELA will maintain publicly accessible git repositories of package sources necessary to create an Enterprise Linux compatible distribution.

One of the goals of the OpenELA project is to build and maintain an infrastructure that is provider-agnostic. Furthermore, in order to maintain compatibility and independence, OpenELA repositories will rely on DistGit instead of git-lfs for binary storage, and will organize these  into a small set of “organizations” with flat structure.This will make it possible for the project to be hosted on any git backend infrastructure.


### Package Repository Structure

#### DistGit

All operating system sources will be broken down into separate DistGit repositories. A DistGit repo is a Git repository which includes text files and sources and referrals to the binary components so they are not included in the Git repository directly.

DistGit is preferred to git-lfs as it does not require special support from the git “forge”, nor is it subject to the kinds of storage and bandwidth limitations that come along with git-lfs support on some platforms.

The source packages for OpenELA will exist in a multi-repository structure, where every repository represents a single package and binary files are referred to via a link (DistGit). Each package Git repository will contain a structure which can be used to build directly from and/or create SRPMs from.

#### Branch Naming for Repositories

Branches will be used to identify the target for each source package. For example:

* Base: el-8.8, el-9.0, el-9.1
* Modularity: el-8.8-module-$STREAM, el-9.1-module-$STREAM

*note: refer to the Contributor Policy for specifics on contributions.*

#### GitHub Organizations

Within GitHub, OpenELA will be organized into the following top-level organizations:

* github.com/openela – The main repo for all root level tooling and repos (e.g. website, helper tools, and projects)
* github.com/openela-main – A series of DistGit repos for hosting the base OS packages
* github.com/openela-contrib – A series of DistGit repos for hosting community contributed packages (not patches). Similar to EPEL.

### Main Project Repo: github.com/openela

This repository will contain all of the repositories with the exception of the DistGit (operating system sources). For example, this will include:

* Website sources
* Tooling for use with DistGit: This tooling should be able to pull and push from the Lookaside cache as needed as well tools for doing local builds via Mock. A similar tool exists for Fedora called “fedpkg”.
* ELProfile: A compatibility tool for testing/validating EL derivatives 
* Documentation

### Base OS Repo: github.com/openela-main

The OpenELA-main is the primary repository for all Enterprise Linux sources. It will serve as the location for not only the 1:1 compatible pristine unbranded sources, but also as the location for all BaseOS optimizations, security fixes, etc.

**DistGit Structure for the OpenELA Main Repo:**

* SPECS: location of the RPM spec file
* SOURCES: location of all non-binary source files
* PATCHES: Any “open patch” patches or changes that we apply to the upstream sources (e.g. debranding)
* RPM header: this is a binary header from the original SRPM that can be used to validate upstream signature and checksums of files (note, this might be put into the Lookaside cache depending on size)
* checksums: hash and file name/path for the object store Lookaside cache
* maintainers: list of package maintainers (only for contrib packages)
* .gitignore: Any binary files that exist in a Lookaside cache should have an entry here

**Lookaside Format:**

The format for the lookaside cache is:

```
<OBJECT STORE HASH> <LOCAL FILE PATH>
```

*note: The hash must be cryptographically strong (SHA256 or SHA512).*

### Contrib Repo: github.com/openela-contrib

This repository structure is similar to OpenELA-main for new packages that do not exist in the base upstream Enterprise Linux.

Additionally, tarballs and binaries shall not be included in the Git repository, and instead it is important to define the pristine upstream sources via their fully qualified URIs in the RPM Spec file “Source#” tags. 

**DistGit Structure for the OpenELA Contrib Repo:**

* SPECS: location of the RPM spec file
* SOURCES: location of all non-binary source files
* checksums: list of all non-committed sources which are referenced via “SOURCE#: “ URIs
* maintainers: list of package maintainers (only for contrib packages)
* .gitignore: Any binary files that will be downloaded via “SOURCE#: “ URIs should have an entry here

**note: we might want to put in Git rules to ensure that nobody commits a binary/tarball source into the Git repo.**
