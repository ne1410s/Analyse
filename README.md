# Analyse and Analyse.4Tests
## Overview
These packages adds Roslyn analyser rules and implementation.
Additionally, there are a small number of project properties that are provided to the referencing project. 

The `Analyse.4Tests` package is very similar to `Analyse`, with a small number of rule relaxations, and does not make referencing projects generate documentation on build.

## Notes

### Overriding Stylecop Header
Likely you may wish to remove or customise the Stylecop file header that ships by default. There are two suggested ways to do this, according to your desired outcome:

#### [A] Removing Header
If you don't care about headers, you can simply suppress the rule in a `.editorconfig` file. For example:
```bash
# SA1633: File should have header
dotnet_diagnostic.SA1633.severity = none
```

#### [B] Customising Header
If you want the header with your own values, then add a `stylecop.json` file to your solution root as follows:
```json
{
  "$schema": "https://raw.githubusercontent.com/DotNetAnalyzers/StyleCopAnalyzers/master/StyleCop.Analyzers/StyleCop.Analyzers/Settings/stylecop.schema.json",
  "settings": {
    "documentationRules": {
      "companyName": "YOUR COMPANY NAME HERE"
    }
  }
}
```
Then, be sure to replace the stock file with the above file in your `.csproj` files, e.g. like so:
```xml
<ItemGroup>
  <AdditionalFiles Include="../stylecop.json" />
  <AdditionalFiles Remove="$(NuGetPackageRoot)analyse/**/content/stylecop.json" />
</ItemGroup>
```
The above assumes your central stylecop.json is one directory above the project, hence the `../stylecop.json` relative path, but this may be changes according to your needs. 

### Commands
```powershell
# Pack and publish a pre-release to a local feed
$suffix="alpha001"; dotnet pack -c Release -o nu --version-suffix $suffix; dotnet nuget push "nu\*.*$suffix.nupkg" --source localdev; gci nu/ | ri -r; rmdir nu
```