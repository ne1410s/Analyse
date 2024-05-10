# Analyse and Analyse.4Tests
## Overview
These packages adds Roslyn analyser rules and implementation.
Additionally, there are a small number of project properties that are provided to the referencing project. 

The `Analyse.4Tests` package is very similar to `Analyse`, with a small number of rule relaxations, and does not make referencing projects generate documentation on build.

## Notes
### Commands
```powershell
# Pack and publish a pre-release to a local feed
$suffix="alpha001"; dotnet pack -c Release -o nu --version-suffix $suffix; dotnet nuget push "nu\*.*$suffix.nupkg" --source localdev; gci nu/ | ri -r; rmdir nu
```