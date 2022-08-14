Remora.Sdk
==========
Remora.Sdk is a set of .NET MSBuild SDKs, developed for use with the various
projects under the Remora umbrella.

The SDKs focus on taking the out-of-the-box .NET experience and providing 
stricter defaults for code style, nuget package information, target frameworks,
code inspections, and licensing.

Primarily, this boils down to adding a number of analyzers with extensive
configuration by default, setting up NuGet properties for open-source projects
(such as SourceLink, debug symbol generation, source distribution, etc), and
legal licensing boilerplate for your code.

Currently, two SDKs are defined by this project - [Remora.Sdk][1] and 
[Remora.Tests.Sdk][2].

Remora.Sdk contains the base set of properties and packages, and should be used
for libraries and applications. Remora.Tests.Sdk extends Remora.Sdk with 
packages and properties for unit test projects.

See the individual SDKs for more information about usage and requirements.


[1]: Remora.Sdk/README.md 
[2]: Remora.Tests.Sdk/README.md 
