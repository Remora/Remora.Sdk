Remora.Sdk
==========

This SDK provides properties, configuration, and packages for a wide variety of
common cases, such as compilation, language support, and code analysis.

## Usage
The SDK is made available via NuGet, and usage is as simple as using it in place
of the standard .NET SDK. You must also define, at a minimum, the legal author 
of the software and the email at which they can be contacted. 

This does not have to be an individual, and can just as easily be an 
organizational entity. 

Failure to define these properties will result in a compilation error.

```xml
<Project Sdk="Remora.Sdk/1.0.0">
    <PropertyGroup>
        <LegalAuthor>John Doe</LegalAuthor>
        <LegalEmail>john@doe.org</LegalEmail>
    </PropertyGroup>
</Project>
```

Note that you do not need to define the target framework(s); the SDK has some 
reasonable defaults in place (more on this later).

## Feature Breakdown
The following sections dive into each feature category that the SDK handles. 
Generally, the SDK defines or implements features within each category in an
overridable or non-overridable way; non-overridable features are defined after
user definitions, and overwrite any value you set.

Properties marked with an asterisk (`*`) are defined by Remora.Sdk and are not
part of the standard set of properties exposed by MSBuild or Microsoft.NET.Sdk.

### Compilation
The following properties are defined by the SDK.

| Property                  | Value | Overridable |
|---------------------------|-------|-------------|
| Deterministic             | true  | No          |
| DebugSymbols              | true  | No          |
| GenerateDocumentationFile | true  | No          |

### Framework Targets
The following properties are defined by the SDK.

| Property              | Value         | Overridable |
|-----------------------|---------------|-------------|
| LibraryFrameworks*    | net6.0;net7.0 | Yes         |
| ExecutableFrameworks* | net7.0        | Yes         |
| TargetFramework       |               | Yes         |
| TargetFrameworks      | (varies)      | Yes         |
| TargetNetStandard     | true          | Yes         |

If `TargetNetStandard` is `true`, `netstandard2.1` will be included as a target when building libraries.
Set the property to `false` if this is undesirable.

Notably, the SDK defines a set of standard targets for libraries and frameworks,
then applies this to the `TargetFrameworks` property based on the project's 
output type.

You may either override the framework sets for libraries or executables, or you
may directly set the target framework(s), which will disable usage of the SDK's
framework sets.

### Language Support
The following properties are defined by the SDK.

| Property    | Value  | Overridable |
|-------------|--------|-------------|
| LangVersion | latest | Yes         |

The following packages are added by the SDK.

| Package        | Purpose                                                     |
|----------------|-------------------------------------------------------------|
| Nullable       | Enables the usage of nullability annotations in all targets |
| IsExternalInit | Enables the usage of records in all targets                 |

### Code Analysis
The following properties are defined by the SDK.

| Property            | Value                                          | Overridable |
|---------------------|------------------------------------------------|-------------|
| WarningsAsErrors    | (multiple; nullability warnings)               | Yes         |
| NoWarn              | (multiple; problematic warnings from packages) | Yes         |
| Nullable            | enable                                         | No          |
| AnalysisLevel       | 7                                              | No          |
| CodeAnalysisRuleSet | (internal value)                               | No          |

The following packages are added by the SDK.

| Package               | Purpose                               |
|-----------------------|---------------------------------------|
| StyleCop.Analyzers    | Additional code inspections           |
| JetBrains.Annotations | Additional attributes for IDE support |

The inclusion of `StyleCop.Analyzers` may come as a surprise and worry to many;
however, the package's inspections have been extensively tuned and configured in
order to conform to standard C# style, naming, and layout rules. Rules that 
cannot be enabled without violating standard C# style rules have been disabled.

The vast majority of StyleCop.Analyzers' inspections have been promoted to 
compilation errors; it is highly encouraged to leave it this way. 

### Code Coverage
The following properties are defined by the SDK.

| Property                                  | Value | Overridable |
|-------------------------------------------|-------|-------------|
| ExcludeNonRunnableFrameworksFromCoverage* | true  | Yes         |


This property controls disabling of coverage generations for assemblies that
target .NET Standard which would otherwise artificially deflate coverage 
percentages.

### NuGet Package Generation
The following properties are defined by the SDK.

| Property                        | Value                                  | Overridable |
|---------------------------------|----------------------------------------|-------------|
| IsPackable                      | true                                   | Yes         |
| Title                           | $(AssemblyName)                        | Yes         |
| Authors                         | $(LegalAuthor)                         | Yes         |
| PackageIconPath*                | (internal)                             | Yes         |
| PackageRequireLicenseAcceptance | true                                   | Yes         |
| Copyright                       | $(LegalCopyrightHolder) <current year> | No          |
| IncludeSymbols                  | $(IncludeBuildOutput)                  | No          |
| IncludeSource                   | $(IncludeBuildOutput)                  | No          |
| EmbedUntrackedSources           | $(IncludeBuildOutput)                  | No          |
| EmbedAllSources                 | $(IncludeBuildOutput)                  | No          |
| PublishRepositoryUrl            | true                                   | No          |
| SymbolPackageFormat             | snupkg                                 | No          |
| PackageReadmeFile               | README.md                              | No          |
| PackageLicenseExpression        | $(LegalLicense)                        | No          |
| PackageIcon                     | (filename of PackageIconPath)          | No          |

The following properties are not defined, but cause a compilation warning if 
left empty or unset.

| Property          | 
|-------------------|
| PackageTags       |
| PackageProjectUrl |

The following packages are added by the SDK.

| Package                     | Purpose                                                     |
|-----------------------------|-------------------------------------------------------------|
| Microsoft.SourceLink.GitHub | Provides a logical link between the binaries and the source |

The following files are added to generated nuget packages.

| File                          | Description                                                      |
|-------------------------------|------------------------------------------------------------------|
| (filename of PackageIconPath) | The icon that is displayed for the package on the package feed   |
| README.md                     | The README that is displayed for the package on the package feed |

Of note is the `PackageIconPath` property; this defaults to a bundled icon 
appropriate for Remora projects, but may be overridden to provide your own icon.

### Licensing
The following properties are defined by the SDK.

| Property              | Value             | Overridable | Required |
|-----------------------|-------------------|-------------|----------|
| LegalLicense*         | LGPL-3.0-or-later | Yes         | Yes      |
| LegalAuthor*          |                   | Yes         | Yes      |
| LegalCopyrightHolder* | $(LegalAuthor)    | Yes         | Yes      |
| LegalEmail*           |                   | Yes         | Yes      |
| LicenseTextFile*      | (internal)        | Yes         | Yes      |
| UseSPDXFileHeaders*   | false             | Yes         | No       |

Of note is that `LegalLicense` defaults to LGPLv3 or later; this is the standard
for Remora projects, but you may choose another license expression if required.

If the license expression is not natively supported by the SDK, you must also
provide a path to a license header that should be placed at the start of each
source code file. See the [license-headers][1] directory for examples; you may 
use any properties supported by StyleCop.Analyzers, as well as any additional
ones defined by Remora.

These properties come together to
  * Generate metadata for your NuGet packages
  * Generate a license header for your source code files

Optionally, you may set `UseSPDXFileHeaders` if you don't want to use a 
traditional license header. This creates a machine-readable file header 
according to the [SPDX][2] specification and populates it with the required 
metadata.

### Centrally Managed Package Versions
Remora.Sdk supports [central package management][3] through MSBuild and NuGet's
usual mechanisms with a `Directory.Packages.props` file. If you set 
`ManagePackageVersionsCentrally` to `true`, Remora.Sdk will detect this and 
switch over to also using centrally managed versions for its internal 
mechanisms.

This means that, in addition to letting you control your own dependencies 
centrally, Remora.Sdk will also respect your pinned versions the packages it 
brings dependencies on.

Your `Directory.Packages.props` is always imported after Remora.Sdk's version
pins, meaning you can either use `Update` or `Include` to override its settings.
The preferred way is with an `Update` item.

[1]: Sdk/license-headers
[2]: https://spdx.dev/
[3]: https://learn.microsoft.com/en-us/nuget/consume-packages/central-package-management
