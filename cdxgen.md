# cdxgen
[***Git Repo:*** github.com/AppThreat/cdxgen](https://github.com/AppThreat/cdxgen)

### Basic Use

*cdxgen* is a simple to use CycloneDX SBOM generator tool. 

Purportedly Supports:
||||||
|-|-|-|-|-|
| node.js | java | php      | python| go|
| ruby    | rust | **.Net** | **c/c++** <br/>(using conan)| haskell|
| elixir| dart | clojure| docker/oci image|



***Sample***

`cdxgen <path to repo> -r -o _manifest.cyclonedx.json` 

- -r is "recursive", likely meaning it's searching the directory and subdirectories. I have not been able to generate an sbom without the -r, though it seems it's meant to be optional.

- -o determines output. Without it the sbom is printed onto the console

Example output:
- [sbom-tool.cdx.json](files\sbom-tool.cdx.json)
![owasp vulnerability tool](files\cdxgen\sbom-tool_vulnerabilities.png)

<br/>
Unsuccessful at creating an SBOM from a C/C++ project.

## Workflow

Difficulty getting it to work on GitHub Actions