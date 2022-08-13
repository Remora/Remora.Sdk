Important bits:

Required (errors if empty or undefined):
  * `LegalAuthor`, for copyright notice
  * `LegalCopyrightHolder`, but defaults to `LegalAuthor`
  * `LegalEmail` ditto

Recommended (warns if missing):
  * `PackageTags`, for nuget
  * `PackageProjectUrl`, ditto
  * `Authors`, ditto, but defaults to `LegalAuthor`

Optional (has builtin or is otherwise defaulted):
* `PackageIconPath` (defaults to bundled shark icon)
