# Dependency Track - OWASP

A component analysis platform meant to identify vulnerabilities via consumption and interpretation of SBOMs formatted in CycloneDX. Support of other SBOM formats seems forthcoming as the tool has a setting to choose the types of BOMs. 
!["BOM Formats: Enables support for processing BOMs of various formats. Only BOM formats which are enabled will be processed."](files\dependency-track\BOMFormats.png)

### Projects
The Projects page contains a list of all projects and new projects can be made here.
![Projects with simple stats of portfolio, list of all projects, ability to add project](files\dependency-track\projects.png)

### Project
Here is an example project. Shown is a graphical representation of the amount and severity of the vulnerabilities found within the project. Also contained is a list of all the components of the project.
![googletest project](files\dependency-track\project_googletest.png)

#### Project Components
This is the page that displays the loaded components. This is also where an sbom can be uploaded or downloaded. The system isn't the most responsive when uploaded, and it won't tell you if it fails, but if it loads it works well.
![googletest project components](files\dependency-track\project_googletest_components.png)

#### Project Vulnerabilities
Here is the list of vulnerabilities found for the project, they are graded in severity and gives information of what component they correspond to.
![googletest project vulnerabilities](files\dependency-track\project_googletest_vulnerabilities.png)

#### Vulnerability
Below is one of the vulnerabilites found for the above project. This vulnerability is graded as severe. The second image shows an explanation of the vulnerability and offers more resources on it.
![pandas vulnerability](files\dependency-track\vulnerability_pandas.png)

![pandas vulnerability overview](files\dependency-track\vulnerability_pandas_overview.png)

### Licenses
Below is a licensing page that shows the licensing information for the portfolio.
![licenses page](files\dependency-track\page_licenses.png)



###

Resources
- [github.com/DependencyTrack/dependency-track](https://github.com/DependencyTrack/dependency-track)
- [dependencytrack.org/](https://dependencytrack.org/)
- [docs.dependencytrack.org/](https://docs.dependencytrack.org/)


To get started, see the github repo. Set up using Quickstart (Docker Compose). If curl command is having issues in running then download manually (go to the site it's trying to curl from). Then run the next command. Currently, the commands are:

Method to get it running.

curl command was not working so downloaded file manually then ran second command.
(see [github repo](https://github.com/DependencyTrack/dependency-track))
```bash
# Downloads the latest Docker Compose file
curl -LO https://dependencytrack.org/docker-compose.yml

# Starts the stack using Docker Compose
docker-compose up -d
```

go to `localhost:8080` in chrome