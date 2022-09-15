# Common Workflow Language Development and Release Process

## Versioning

CWL releases are semantically versioned.  The number scheme is MAJOR.MINOR.PATCH.

"Compatible versions" means that a CWL document can have its
`cwlVersion` field trivially changed from one version to another, and
the document will still validate and execute the same way.

When making breaking changes such that an old version document cannot
be trivially changed to a newer version, the MAJOR version must be
increased, and MINOR and PATCH are reset to zero.  An example of a
breaking change is removing obsolete syntax.

When adding features, such that an older version document with the
same MAJOR version can be trivially changed to the newer `cwlVersion`
(but not newer-to-older), the MINOR version must be increased, and the
PATCH reset to zero.

When making clarifications or text changes to an already-released
specification that do not materially affect the document schema or
execution semantics, the PATCH should be increased.  The `cwlVersion`
is unchanged in this case.

Stable CWL releases are only referred to by their MAJOR.MINOR version.

Development versions are indicated by taking the MAJOR.MINOR.PATCH of the
version under development and adding "-devN" to the end, for example
"-dev1".  The development version should be incremented when making a
breaking change or when requesting community review of the development
version.  There is no promise of compatibility between "-dev" versions
as a feature may undergo incompatible changes during development.

When the version becomes the newest CWL specification, the "-devN" is
removed.

## Development process

First, the decision is made whether the new release will be backwards
compatible or not, and the new version number determined by
incrementing the MAJOR, MINOR or PATCH part of the version.

PATCH changes are made on the existing repository for the stable
release.  Version numbers in the specification document should be
updated to the reflect the PATCH version.  The `cwlVersion` is
unchanged.

For MAJOR and MINOR versions, create a new github repository
"cwl-vMAJOR.MINOR" for the version series in the
common-workflow-language organization.  This repository will be a fork
of the most recent stable release, with appropriate version numbers
updated to the new development version (in the form
"MAJOR.MINOR.0-dev1").  This includes the specification document and
the `cwlVersion` of the documents in the test suite.

The need for new features is determined by discussion with and
contributions from the community.  These may be tracked and discussed
through github issues on the appropriate repository.

Changes are proposed through pull requests against the development
specification.  Pull requests are merged by members of the development
team that are authorized with commit access by the CWL leadership
team.

Changes to the specification should be accompanied with updates to the
change log describing the change.  The "-devN" version should be
incremented following the guidelines above.  Changes should also be
accompanied by new conformance tests.

Conformance tests may also be submitted on their own, if it is found
that some feature has been overlooked by existing testing, or to
ensure that a bug discovered in one implementation does not exist in
other implementations.

Proposed new features should be demonstrated in least one
implementation to be be incorporated in the development specification.
For stable release, there should be commitment to implement the
feature by at least one other independent implementation.

## Release process

Once the development team feels that all outstanding issues for the
release have been addressed, it is submitted to the leadership team
for approval.

A pull request is created that updates the version in the repository
to remove the "-devN" suffix and the leadership team is notified about
the proposed stable release.  The leadership team registers their
votes by adding comments on the pull request.  A majority is
sufficient to approve the specification although in practice if any
concerns are raised they will generally be addressed with the goal of
getting consensus.

Following approval, the web site is updated to reflect the new stable
release, the new release is announced on the relevant media, and a
copy of the specification is uploaded to a research archive site such
as Figshare or Zenodo to assign a DOI.

Sometimes post-release fixes are necessary.  Trivial changes (such as
fixing typos) may be applied directly by the development team.  More
substantive changes to the text, such as clarifications or new
conformance tests, require incrementing PATCH as discussed above,
resulting in a new version that should be re-submitted for approval by
the leadership team.
