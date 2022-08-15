Remora.Tests.Sdk
==========

This SDK provides extended configuration based on Remora.Sdk for unit test 
projects. In particular, the SDK utilizes xUnit and coverlet to provide a unit
test framework and code coverage.

All features and functionality exposed by Remora.Sdk is available in 
Remora.Tests.Sdk. The functionality described in this document is additive.

## Usage
The SDK is made available via NuGet, and usage is as simple as using it in place
of the standard .NET SDK. You must also define, at a minimum, the legal author
of the software and the email at which they can be contacted.

This does not have to be an individual, and can just as easily be an
organizational entity.

Failure to define these properties will result in a compilation error.

```xml
<Project Sdk="Remora.Tests.Sdk/1.0.0">
    <PropertyGroup>
        <LegalAuthor>John Doe</LegalAuthor>
        <LegalEmail>john@doe.org</LegalEmail>
    </PropertyGroup>
</Project>
```

## Feature Breakdown
The following sections dive into each feature category that the SDK handles.
Generally, the SDK defines or implements features within each category in an
overridable or non-overridable way; non-overridable features are defined after
user definitions, and overwrite any value you set.

Properties marked with an asterisk (`*`) are defined by Remora.Tests.Sdk and are 
not part of the standard set of properties exposed by MSBuild or 
Microsoft.NET.Sdk.

### Framework Targets
The following properties are defined by the SDK.

| Property              | Value                   | Overridable |
|-----------------------|-------------------------|-------------|
| LibraryFrameworks*    | $(ExecutableFrameworks) | Yes         |

### NuGet Package Generation
The following properties are defined by the SDK.

| Property   | Value | Overridable |
|------------|-------|-------------|
 | IsPackable | false | No          |

### Unit Testing
The following packages are added by the SDK.

| Package                   | Purpose                               |
|---------------------------|---------------------------------------|
| Microsoft.NET.Test.Sdk    | Enables integration with .NET tooling |
| xunit                     | Test framework                        |
| xunit.runner.visualstudio | Enables IDE-integrated test runs      |
| xunit.runner.console      | Enables console-initiated test runs   |
| coverlet.collector        | Enables code coverage collection      |

### Code Coverage
The following properties are defined by the SDK.

| Property                  | Value | Overridable |
|---------------------------|-------|-------------|
| ExcludeTestsFromCoverage* | true  | Yes         |
