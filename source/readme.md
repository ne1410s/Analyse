## Analyse

``` powershell
# Restore tools
dotnet tool restore

# Upload to local package repo
$ver="1.0.0-alpha-0001"; dotnet pack -c Release -o nu -p:Version=$ver; dotnet nuget push "nu\Analyse.$ver.nupkg" --source localdev


```
