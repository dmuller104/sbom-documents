## SBOM-TOOL

[***Git Repo:*** https://github.com/microsoft/sbom-tool](https://github.com/microsoft/sbom-tool)

Microsoft's sbom-tool is an SBOM generator tool that generates SPDX 2.2 SBOMs. It carries multilanguage support and is capable of adding support for other languages with minimal difficulty. 

The sbom-tool calls the [Component-Detection](#component-detection-tool) tool on a directory. The sbom-tool uses the information gathered to generate the spdx manifest file. The tool takes in, as required parameters, [`generate`, -`b`, -`bc`, -`pn`, -`pv`, -`ps`, -`nsb`] with notable optionals of [-`m`, -`D`]. 

- `generate` - tells the tool to generate an sbom. There is another functionality that can be used instead of `generate` called `validate` but it seems to still be in development.

- -`b` mostly populates the files section and should point to the root of the project. 

- -`bc` determines what directory is passed to the component-detection. -`bc` can generally point to the root of the project as well.

- -`pn` package name

- -`pv` package version

- -`ps` package supplier

- -`nsb` namespace uri base - follow regex pattern similar to: `\w[\w\n]*?://[\w\n.]*?` (ex. `https://fakeusaf.fakegov`)

- -`m` determines where spdx file will be saved, saves in directory with following file structure. Defaults to value of -`b`
```
<-m path>
 -_manifest
  --spdx_2.2
   ---manifest.spdx.json
   ---manifest.spdx.json.sha256
```
- -`D` flag that tells tool to replace any existing manifest in manifest folder location. If -`m` is same as -`b` then software will act like -`D` is true

*example:* `sbom-tool.exe generate -bc ".\sbom-tool" -b ".\sbom-tool" -m ".\sbom-tool" -pn devUSAF_PackageName -pv devUSAF_PackageVersion_0.0 -ps devUSAF_PackageSupplier -nsb http://USAF_UNOFFICIAL_DEVELOPMENT.gov -D true`

The SBOM-tool works as an executable which is able to fit well into a pipeline. At times some building or auto-generating of files is required before running the tool. An example of this is when running on the sbom-tool project itself, the project needs to be built first before it will result in any found components.

## Component-Detection Tool

[***Git Repo:*** https://github.com/microsoft/component-detection](https://github.com/microsoft/component-detection)

Finds components and their relationships using component detectors, one or more defined for each language. These detectors are stored in `src/Microsoft.ComponentDetection.Detectors`. More will be explained about detectors [below](#detector). The component-detection tool looks at the name of each file and checks if any detector matches with that name using a search pattern. If they match the tool will give access of the file to the detector. It is up to the detector to tell the component-detection tool when a component has been found and its relationship with other components. Once the component tool has finished with running over the file names it displays its results, saves them into a file in memory (which can be viewed via the path it prints out) and ends. 

## Detector

Finds components and their relationships by looking at source code files. In creating a detector a component-type is given to it - meant to group detectors (ex. Npm, NuGet, Pip, Maven, etc...). A detector has a property called `SearchPatterns` which is used by the component tool to determine which files are to be evaluated by the detector. It has a function called `OnFileFound` which is called when a file that matches `SearchPatterns` is found. `ProcessRequest` is given to `SearchPatterns` as a parameter. `ProcessRequest` contains data structures for the file contents and for `SingleFileComponentRecord`, a component recorder tool. `SingleFileComponentRecord` uses the function `RegisterUsage` to register a component. 

It is recommended to create tests for the detector.

For more information and a step-by-step guide to creating a detector, see: [`sbom-tool/docs/creating-a-new-detector.md`](https://github.com/microsoft/component-detection/blob/main/docs/creating-a-new-detector.md).


## Current and Future

SBOMs can be created for C# at this time. The C# project might require using NuGet for the detector(s) to find what they need.

A detector will need to be created for Ada and Jovial. Possibly C++. C# might need another detector depending on how projects on base use C# and package managers for C#.

