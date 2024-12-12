# OpenELA Contribution and Intellectual Property Policy

## Scope

This OpenELA Contribution and Intellectual Property Policy (Policy) applies 
to contributions of new or revised source code to an OpenELA project.  It 
does not apply to the evaluation of General Members’ contributions of time or 
effort substantially furthering OpenELA’s mission for the purpose of membership 
eligibility, which are determined at the discretion of OpenELA’s Board of Directors 
or designee.

OpenELA welcomes contributions from the community seeking to improve the
experience of users on Enterprise Linux. Contributions to OpenELA must adhere
to the following guidelines.

The goal of OpenELA is to provide continuity for downstream
distributions by providing a secure, transparent, and reliable 
(EL) source that is globally available to anyone as a buildable base. OpenELA
allows distributions to create and maintain downstream derivatives of EL.

## What Can be Contributed to OpenELA?

Most contributions should not go directly into OpenELA. Contributions are
governed by similar rules to other Linux stable projects, i.e. contributions to
OpenELA must have antecedents in the upstream for those distributions.

### What is a “Patch”?

Patches are fixes, changes, and enhancements specific to a single project or
package.

“Bug Fix Patches” are generally patches that are present in the upstream repository or
the upstream distribution repository and improve stability, robustness or
security of the already present features. They should be backward binary compatible
and not break previously documented behavior or features. See also the Bug-For-Bug 
Compatibility Standard below. 

### Contribute Upstream First

Before patches are considered for OpenELA, developers are encouraged to
contribute patches to upstream. If you’re having trouble finding the upstream
for a particular project, check the source line in the SRPM. We don’t want
OpenELA to become a repository for orphaned patches, and it’s very important to
encourage developers to contribute their efforts to the upstream projects.

In some cases, you may need to contribute to both the project upstream (i.e.
github.com/upstream/project) and also to the upstream distribution version of
that package prior to getting that change into OpenELA.

There may be specific exceptions defined to the “Upstream First” policy per the
Technical Steering Committee, which will be linked here if and when defined.

### The Bug-for-Bug Compatibility Standard

The “bug-for-bug” compatibility provides a strict metric for maintaining
compatibility with Enterprise Linux: while there are often multiple possible
fixes to a particular bug, maintaining bug-for-bug compatibility shortcuts
those technical discussions about “which fix is best” by requiring the -main
version to be “equally broken” with upstream EL. Maintaining bug-for-bug
compatibility also provides an avenue for distributions downstream of OpenELA
to provide value.

## Sign-off your Submissions

Changes should be signed off using the DCO ([Developer’s Certificate of
Origin](https://developercertificate.org/), as defined in the [Linux Kernel
documentation](https://www.kernel.org/doc/Documentation/process/submitting-patches.rst)).

## Contribute under the Project’s License

Any changes to projects must be submitted under the project’s existing license
and comply with the license of the project being changed. OpenELA projects
shall not deviate from or modify the license from the upstream program’s
license terms.

Any additional content of new packages, such as specfiles, are licensed under
the same license terms of the project being distributed unless explicitly
defined otherwise and with exceptions approved by the Technical Steering
Committee. Contributions to the contrib branches of the openela-main
organization shall keep the original license of additional content.

New projects which exist only in OpenELA shall have a toplevel LICENSE or
COPYING file which explicitly define the license for the project, and that
license must be an OSI-approved Open Source License. Licenses shall have a SPDX
license identifier assigned and shall be Open Source according to the Open
Source Definition [as maintained by the Open Source
Initiative](https://opensource.org/osd/).

New and unique contributions to OpenELA which are not part of an existing open
source project may have additional requirements which have yet to be defined.

## Contributing to openela-main

Contributions are welcome to openela-main repositories, however those
repositories must maintain __strict bug-for-bug compatibility__ with EL.

Bug Fix Patches and other patches which are not bug-for-bug compatible with EL
are not permitted in the main repositories, and must be submitted to -contrib
repos as described below.

Write access to the primary OpenELA branches is restricted to members of the
Technical Steering Committee, who are responsible for ensuring that those
commits respect the bug-for-bug compatibility requirements.

## Contributing to openela-contrib

Maintaining patches in a contrib repo is a long-term commitment that will
require maintenance any time the ‘base’ or upstream package changes. Therefore
projects in the ‘openela-contrib’ repository will be created on demand and when
a maintainer is stepping up to take the burden on maintaining the contributed
package.

## Contributing New Packages into -contrib repos

Contributions of new packages to OpenELA are welcome in the openela-contrib
organization. These are packages which are not part of Upstream EL but which
add value to the OpenEL Ecosystem.

Branches within the openela-contrib repo should retain the ‘contrib’ tag in
their branch names, to ensure that it is clear that these branches are not
bound to be bug-for-bug compatible with EL.

## Contributing Bug Fix Patches into -contrib repos

Patches and Bug Fix Patches are welcome in the openela-contrib repositories.
This may require duplicating a repository between openela-main (which is
bug-for-bug compatible) and the openela-contrib repositories (which can be
patched).  Branches should include the tag ‘-contrib’ to allow for being able
to `git clone` both the main and -contrib repositories into the same local git
repo.

Patches which are accepted to the -contrib branches should meet the “Bug Fix
Patches” compatibility standard described above. The Technical Steering Committee 
can further define additional exceptions. Patches for -contrib branches must be 
present in the upstream project repository. Patches which are not applicable to 
or not accepted by upstream will require review by the Technical Steering Committee.

## Document Governance

This document is maintained by the Technical Steering Committee. Please
supply all suggested modifications for consideration by the Technical Steering
Committee and/or OpenELA Board of Directors through the usual github constructs.
