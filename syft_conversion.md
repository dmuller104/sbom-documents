Building on the principles of using GitHub Actions to make a ```.yml``` workflow file, we are going to create another action in the step to convert the generated SBOM.

Firstly we need to make sure that we have Syft available to use. This can be done by using ```curl``` command in order to download and install Syft:

```yml
    # This is the SBOM generation through sbom-tool and convert with Syft
    - name: Generate SBOM using SBOM-Tool
      run: |
        curl -Lo $RUNNER_TEMP/sbom-tool https://github.com/microsoft/sbom-tool/releases/latest/download/sbom-tool-linux-x64
        chmod +x $RUNNER_TEMP/sbom-tool
 -->    curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin
        $RUNNER_TEMP/sbom-tool generate -b . -bc . -pn Test -pv 1.0.1 -ps Elijah_Nunez -nsb http://workflowtest/ -v Verbose
```

Take note of the line with the arrow (do not include the arrow when making this change). This is how we will be adding Syft to our environment using ```curl```.

The next step we need to take is using finding and converting the sbom we just generated. Syft has multiple conversion formats, some are still considered experimental. For our own use case, we will be taking the SBOM that the sbom-tool generated which is a ```json.spdx``` and turn that into a ```spdx-tag-value``` format.

```yml
    # This is the SBOM generation through sbom-tool and convert with Syft
    - name: Generate SBOM Using SBOM-Tool and Convert w/ Syft
      run: |
        curl -Lo $RUNNER_TEMP/sbom-tool https://github.com/microsoft/sbom-tool/releases/latest/download/sbom-tool-linux-x64
        curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin
        chmod +x $RUNNER_TEMP/sbom-tool
        $RUNNER_TEMP/sbom-tool generate -b . -bc . -pn Test -pv 1.0.1 -ps Elijah_Nunez -nsb http://workflowtest/ -v Verbose
 -->    mkdir syftsbom
 -->    syft convert ./_manifest/spdx_2.2/manifest.spdx.json -o spdx-tag-value=./syftsbom/sbom.cdx.json
```

The following lines with arrows were added. The first is just to create a directory where we will store the converted sbom, and the second is the actual conversion CLI command using Syft. We first needed to put in the file we are converting and then we specify the output using the ```-o``` flag and the specification of the format. These are the following available formats:
- ```json```
- ```text```
- ```cyclonedx-xml```
- ```cyclonedx-json```
- ```spdx-tag-value```
- ```spdx-json```
- ```github```
- ```table```
- ```template```

The format for the conversion CLI command is the following:

```bash
syft <image> -o <format>

```

