### Running the component detection using Linux detector

Run the tool on a docker image. 

Start Docker
in terminal: `docker images`
copy IMAGE ID for one image (if nothing in list then need to download/start a docker image)
run component-detection tool using parameters `scan --SourceDirectory <some directory> --DockerImagesToScan <Image id hash>`



the Linux detector for the sbom-tool/component-detection requires a hash to be given for dockerImagesToScan (or -di for sbom-tool)

It has found components for the following images:
- daggerboard
- dependencytrack
- ubuntu

It has not found components for:
- hello
  - `https://docs.docker.com/develop/develop-images/baseimages/`
  - `https://github.com/docker-library/hello-world`
