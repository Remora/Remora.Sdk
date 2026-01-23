# Remora.Sdk.Web

This SDK provides an extension to Remora.Sdk wherein the underlying extended framework is `Microsoft.NET.Sdk.Web`.

All general `Remora.Sdk` properties and requirements apply. For instance, `LegalAuthor` and `LegalEmail` still need to
be defined.

For more information, refer to the [Remora.Sdk Readme](../Remora.Sdk/Readme.md).

## Usage

```xml
<Project Sdk="Remora.Sdk.Web/1.0.0">
  <PropertyGroup>
    <LegalAuthor>John Doe</LegalAuthor>
    <LegalEmail>john@doe.org</LegalEmail>
  </PropertyGroup>
</Project>
```

## Remora.Sdk.Web Properties

No additional properties have been added at this time.

## Microsoft.NET.Sdk.Web Properties

All properties added with the inclusion of `Microsoft.NET.Sdk.Web` are available for use in projects with this type.