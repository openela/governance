# OpenELA Repository Structure

OpenELA will maintain publicly accessible git repositories of package sources
necessary to create an Enterprise Linux compatible distribution.

One of the goals of the OpenELA project is to build and maintain maximum
technology independence in our public resources. Furthermore, in order to
maintain compatibility and independence, OpenELA repositories will rely on
DistGit instead of git-lfs for binary storage, and will organize these  into a
small set of “organizations” with flat structure.This will make it possible for
the project to be hosted on any git backend infrastructure.

## Package Repository Structure

### DistGit

All operating system sources will be broken down into separate DistGit
repositories. A DistGit repo is a Git repository which includes text files and
sources and referrals to the binary components so they are not included in the
Git repository directly.

DistGit is preferred to git-lfs as it does not require special support from the
git “forge”, nor is it subject to the kinds of storage and bandwidth
limitations that come along with git-lfs support on some platforms.

The source packages for OpenELA will exist in a multi-repository structure,
where every repository represents a single package and binary files are
referred to via a link (DistGit). Each package Git repository will contain a
structure which can be used to build directly from and/or create SRPMs from.

### Branch Naming for Repositories

Branches will be used to identify the target for each source package. For
example:

In openela-main organisation, these branch names are specified:

* **Base**: `el9`
* **Modulemd**: `el9-modulemd-$STREAM`
   * This contains _only_ the module document (modulemd). This is because a
     module might be a component, but also just a standalone module with other
     components. The modulemd is also relatively stable compared to SRPMs.
* **Module component**: `el9-stream-$STREAM`
   * Contains the SRPM content like **Base**. Used for components of modules and
     separate from base due to each module stream having the ability to have a
     different version.

In openela-contrib, these branch names are specified:

* **Base**: `el9-contrib`
* **Modulemd**: `el9-modulemd-$STREAM-contrib`
   * This contains _only_ the module document (modulemd). This is because a
     module might be a component, but also just a standalone module with other
     components. The modulemd is also relatively stable compared to SRPMs
* **Module component**: `el9-stream-$STREAM`
   * Contains the SRPM content like “Base”. Used for components of modules and
     separate from base due to each module stream having the ability to have a
     different version.

**Note:** *refer to the Contributor Policy for specifics on contributions.*

### Toplevel GitHub Organizations

Within GitHub, OpenELA will be organized into the following top-level
organizations:

* <https://github.com/openela/> – The main repo for all root level tooling and
  repos (e.g. website, helper tools, and projects)
* <https://github.com/openela-main/> – A series of DistGit repos for hosting
  the base OS packages
* <https://github.com/openela-contrib/> – A series of DistGit repos for hosting
  community maintained patches and packages.

## Main Project Repo: <https://github.com/openela/>

This organisation contains all repositories other than the DistGit (operating
system sources). For example, this includes:

* Website sources
* Tooling for use with DistGit: This tooling should be able to pull and push
  from the Lookaside cache as needed as well tools for doing local builds via
  Mock. A similar tool exists for Fedora called “fedpkg”.
* ELProfile: A compatibility tool for testing/validating EL derivatives
* Documentation

## Base OS Repo: <https://github.com/openela-main/>

The OpenELA-main is the primary organisation for all Enterprise Linux sources.
It will serve as the location for the 1:1 compatible pristine unbranded
sources.

**DistGit Structure for the OpenELA Main Repo:**

* `SPECS`: location of the RPM spec file
* `SOURCES`: location of all non-binary source files
* `PATCHES`: Any “open patch” patches or changes that we apply to the upstream
  sources (e.g. debranding)
* `RPM header`: this is a binary header from the original SRPM that can be used
  to validate upstream signature and checksums of files (note, this might be
  put into the Lookaside cache depending on size)
* `checksums`: hash and file name/path for the object store Lookaside cache
* `maintainers`: list of package maintainers (only for contrib packages)
* `.gitignore`: Any binary files that exist in a Lookaside cache should have an
  entry here

**Lookaside Format:**

The format for the lookaside cache is:

```text
<OBJECT STORE HASH> <LOCAL FILE PATH>
```

**Note:** *The hash must be cryptographically strong (SHA256 or SHA512).*

## Contrib Repo: github.com/openela-contrib

This organisation is similar to `openela-main` for existing and new packages.
It will serve as a location for all contributions of bug fixes over
openela-main, as well as additional packages not available in openela-main.

Any tarballs and other binaries shall not be included in the Git repository.
It is important to define the pristine upstream sources via their fully
qualified URIs in the RPM Spec file `Source#:` tags. `https://` URIs are
preferred over others like `http://` or `ftp://`.

**DistGit Structure for the OpenELA Contrib Repo:**

* `SPECS`: location of the RPM spec file
* `SOURCES`: location of all non-binary source files
* `checksums`: list of all non-committed sources which are referenced via
  `Source#:` URIs
* `maintainers`: list of package maintainers (only for contrib packages)
* `.gitignore`: Any binary files that will be downloaded via `Source#:` URIs
  should have an entry here

**Note:** *we might want to put in Git rules to ensure that nobody commits a
binary/tarball source into the Git repo.*

## References

### Open Patch

Rocky Linux has been using Open Patch to maintain any differences in the
package formats. These changes are implemented when the package is imported
into the git structure, so branded components of the sources are never
persisted or distributed by OpenELA.

The layout is a flat directory structure in the PATCHES directory which
contains the Open Patch configurations (files ending with `*.cfg`) and any
supporting files necessary. Documentation for Open Patch can be found here:

<https://github.com/rocky-linux/releng-handbook/blob/main/docs/openpatch-directives.md>

Here is an example from Rocky Linux which is almost exactly as OpenELA will use
it with a slightly different configuration (e.g. there is a CFG and _supporting
directory structure). Here is an example of how Rocky Linux uses Open Patch:

<https://git.rockylinux.org/staging/patch/ansible-core/-/tree/r8/ROCKY?ref_type=heads>
