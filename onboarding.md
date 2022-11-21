## Onboarding Document

The purpose of this document is to familiarize you to the development that has happened thus far with regards to SBOMs.

There is no specific language you need to know to get into these thins; however, a knowledge of C# can greatly help in understanding the code of the Microsoft sbom-tool.

This document is created with being on a windows device in mind. Linux or mac might require some adaptation.

## SBOM

An SBOM, or a Software Bill of Materials can be thought of as a blueprint of software. A generator tool will take in the source code of a project, will find "components" and relationships within the code, and will generate an SBOM out of this information. The SBOM can then be "consumed" with a consumption tool to get the vulnerabilities of the components of the project. 

An end goal in this project is to 
1. Be able to produce an SBOM for every language
2. Incorporate SBOM generation into a pipeline
3. Store SBOMs in a coherent, accessible manner
4. Allow the consumption/analysis of SBOMs 
5. Possibly the automation of SBOM consumption

Major focuses right now are on
1. Microsoft sbom-tool for SBOM generation
2. Daggerboard for SBOM consumption


## Types of SBOMs

There are two major SBOM formats, SPDX and CycloneDX. 

There is more to be learned about the differences between SPDX and CycloneDX. It seems that SPDX is able to contain more information than CycloneDX. CycloneDX seems to be easier for computers to parse. 

Microsoft's sbom-tool currently only supports SPDX but it seems it will support CycloneDX within the near future. There are several generator tools that support CycloneDX, the most general and easiest to use that we found is cdxgen. To look for other CycloneDX generators see [cyclonedx.org/tool-center/](https://cyclonedx.org/tool-center/). 

Daggerboard purports to support both CycloneDX and SPDX. OWASP, the designers of CycloneDX, created Dependency-track which currently supports only CycloneDX.

## SBOM generation

### Microsoft sbom-tool​
-    [sbom-tool overview](sbom-tool.md)
-    [REPO:sbom-tool](https://github.com/microsoft/sbom-tool)
-    [REPO:component-detection](https://github.com/microsoft/component-detection)
-    [Tutorial - Generate SBOM for .NET project](sbomtool-example-dotnet.md)
-    [Advanced: Creating a Detector](https://github.com/microsoft/component-detection/blob/main/docs/creating-a-new-detector.md)


### cdxgen
-    Tutorial

### Syft

### GitHub actions
-    Tutorial - create sbom artifact

### Consumption Tools
-    Dependency Track
-    Daggerboard
       - Understanding
       - Tutorial - Run and consume sbom


### Contacts:
    Adrian
    Daggerboard


Create a document for new team members that guides them through the work accomplished so far on the generation and consumption tools, points them to resources and point of contacts such as those on the Microsoft Team.