For this example the sbom-tool will be run on a dotnet project. 

Notes: 

- for installing the sbom-tool see: https://github.com/microsoft/sbom-tool
- dotnet should come with some visual studio packages, if the version is not correct then update using visual studio installer


Project: https://github.com/Ryujinx/Ryujinx

```
git clone https://github.com/Ryujinx/Ryujinx
cd Ryujinx
dotnet build -c Release -o build
cd ..
sbom-tool Generate -b Ryujinx -bc Ryujinx -m . -pn pn1.1 -ps psSupplier -pv pv1.1 -nsb https://fakeexample.com

```

First, cloning the repo:

`git clone https://github.com/Ryujinx/Ryujinx`

Move into the root of the project:

`cd Ryujinx`

Build the project (dotnet needs to be .NET 7.0 or highter):

`dotnet build -c Release -o build`

Move back to the parent directory:

`cd ..`

run the sbom-tool:

`sbom-tool Generate -b Ryujinx -bc Ryujinx -m . -pn pn1.1 -ps psSupplier -pv pv1.1 -nsb https://fakeexample.com`

---

The SBOM will be located in `./_manifests/spdx_2.2/manifest.spdx.json`

102 components were found, all under the detector "NuGetProjectCentric" with 40 "explicitly referenced".

