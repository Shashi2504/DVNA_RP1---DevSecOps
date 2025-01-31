# Implementing DevSecOps

# Tool Chain Based on

# Open-Source Technology

```
This project is an academic exercise done by SamsonIdowu , Rolly Mougoue ,
Ayomide Shoyemi and Emeka Nzeopara under the supervisionof Pacome
Kemkeu, in fulfillment of Research Project (RP) 1.
```

## Motivation

AsorganizationsmovetowardsaDevOpsculture,itisincreasinglyimportanttointegrate
securityintothesoftwaredevelopmentprocesshencethecallforDevSecOps.DevSecOps
is a methodology that aims to bring security into the continuous integration and
continuousdelivery(CI/CD)pipeline,allowingfortheearlyidentificationandmitigationof
security vulnerabilities. It integrates security practices intothe software development
lifecycle, so that security is considered at every stage, from code development to
deployment.Thisrequirestheuseoftoolsthatcanautomatesecuritytesting,monitorfor
vulnerabilities, and alert teams of potential issues.

Implementing a DevSecOps toolchain can provide numerous benefits for your
organization, including;

```
1. Fasteridentificationandresolutionofsecurityissues:Byintegratingsecuritytesting
andanalysisintotheCI/CDpipeline,securityissuescanbeidentifiedandresolved
early in the development process, before they become major problems.
```
```
2. Improved collaboration between development and security teams: DevSecOps
promotes collaboration and communication between development and security
teams, allowing them to work together to identify and resolve security issues.
```
```
3. Increasedsecurityandcompliance:Byintegratingsecuritytestingandanalysisinto
thedevelopmentprocess,organizationscanensurethattheirsoftwareissecureand
compliant with industry standards and regulations.
```
```
4. Enhancedagilityandspeedtomarket:DevSecOpspracticesallowsforfasterdelivery
of software with the added benefit of ensuring the security of the software.
```
```
5. Continuous monitoringandimprovement:TheDevSecOpscultureandthetoolchain
allows for continuous monitoring and improving the process, making sure that
security practices are always in check and up to date.
```
Overall, implementing a DevSecOps toolchain can help organizations deliver secure
software faster, improve collaboration between development andsecurityteams,and
ensure compliance with industry standards and regulations.


## Table Of Content

## Table Of Content


- Motivation
- Table Of Content
- Objective
- Overview
- Action Plan
- Technology Stack
- Implementation
   - I. Setting Up On-Premise Infrastructure
   - II. Setting up Project Repository on Scm (Github)
   - III. Integrating IDE (VScode) with SCM (GitHub)
   - IV. Set up CI/CD pipelines Using Jenkins
   - V. Secret Management Using Hashicorp Vault
      - 1 Installing Hashicorp Vault Plugins
      - 2 Installing Hashicorp Vault In Ubuntu Server
      - 3 Create an AppRole Credential and Connect with the Jenkins Server.
      - 4. Add the Vault Script to the CI/CD Pipeline Script
   - VI. Introduction of SAST in Project (Snyk)
   - VII. Introduction of Dependency Check in Pipeline Using Synk
      - 1. Add Snyk Security to your project
      - 2 Run a build and view your Snyk report.
   - VIII. Pushing Build to Artifactory
      - 1. Setting up Docker Hub Account
      - 2. Integrating in Pipeline
   - IX. Deployment of Application Build to Test Environment
   - X. Introduction of DAST in Test Pipeline Using StackHawk
   - XI. Setting up Deployment Pipeline to Production
   - XII. Introducing Telegram Alerting in CI/CD
   - XIII. Configuring Application/Environment Monitoring
      - 1 Host Monitoring
      - 2 Container Monitoring
      - 3 Visualization with Grafana
   - XIV. Setting up Web Application Firewall (ModSecurity)
      - Implementation of Modsecurity Web Application Firewall
- Discussion
   - Challenges Faced
   - Improvements
   - Skills Acquired
   - Conclusion
- References


## Objective

The objective of this project is to build a DevSecOps tool chain in order to integrate
security into the software development process, so as to identify and mitigate potential
security issues early enough in the software development lifecycle.

We intend to achieve automation of the integration of security testing and analysis in the
development process.

**NB:** It must be clearly stated that while we will beworking with theDVNAapplication, our
aim is not to remediate the vulnerabilities inherent in the source code, but to build a
DevSecOps tool chain with the capacity to identify these vulnerabilities and eectively
manage them.


## Overview

The images below depict a pictorial overview of the key components and architecture of
our project in accordance with the earlier stated objective. They are intended to provide a
general understanding of the project implementation.

```
Figure 1. 0 : DevSecOps Tool Chain
```
```
Figure 2. 0 : IP Address Table
```

```
Figure 3. 0 : Test Workflow
```
## Action Plan

For this implementation, we intend to simulate a functioning software development life
cycle with all of the necessary stages and components present, while making use of a
vulnerable project written in NodeJs. The project; **DVNA** (Damn Vulnerable NodeJs
Application) and can be found in this github **repository**.

To achieve our objective, we made use of a hybrid infrastructure, which involves a mix of
some open-source on-premise and cloud (SaaS) applications. A previous Jenkins setup
from an earlier project is also used in automating our continuous integration and
deployment, with a full report on this setup referencedhere.

Below are a series of steps undergone at the implementation stage in no particular order;

```
1. Setting up on-premise infrastructure (VMware ESXi)
2. Setting up project repository on SCM (GitHub)
3. Integrating IDE (VScode) with SCM (GitHub)
4. Set up CI/CD pipelines using Jenkins
5. Secret management using Hashicorp vault
6. Introduction of SAST in project (Snyk)
7. Introduction of dependency test in pipeline using Synk
```

```
8. Pushing build to artifactory
9. Deployment of application build to test environment
10 .Introduction of DAST in test pipeline using StackHawk
11 .Setting up deployment pipeline to production
12 .Introducing telegram alerting in CI/CD
13 .Configuring application/environment monitoring (Prometheus)
14 .Setting up web application firewall (ModSecurity)
```
Toachieveourobjectiveandmeetupwiththeoutlinedactionplan,wehadtosplitupthe
workamongsttheteamforeveryonetotakeresponsibilityforapartoftheproject.The
work was split up as follows:

```
● Samson Idowu handled plan 2 , 3 , 4 and 12
● Rolly Mougoue handled plan 6 , 7 , 10 , and 13
● Ayomide Shoyemi handled plan 8 , 9 , and 14
● Emeka Nzeopara handled plan 1 , 5 , and 11
```

## Technology Stack

In the course of this project, we will work with the following technology stack.

```
● IDE: VScode
● Code Repository: Github
● SAST: Snyk
● DAST: StackHawk
● Monitoring: Prometheus/Grafana
● Automation Server: Jenkins
● Container Engine: Docker
● Artifactory: Docker Hub
● Secret Management: Hashicorp Vault
● Proxy Server: Nginx
● Virtualization: VMware ESXi
● Firewall: Mod Security
● IAM: Active Directory
```

## Implementation

### I. Setting Up On-Premise Infrastructure

```
Inordertosetupouron-premiseservers,wevirtualizedourbare-metalusingatype 1
hypervisor(VMwareESXi).Othermissioncriticalserversarethenmadetorunasvirtual
machines on the hypervisor with the bare-metal’s computing resources adequately
distributed.
```
```
For steps on how the installations and configurations were made, see below;
```
```
● VMware ESXi
● Ubuntu Server
● Jenkins Cluster
● Domain Controller using AD
● Vault Installation
● ModSecurity Installation
```
```
NB: It is important to note that other server applicationsare cloud hosted (SaaS).
```
### II. Setting up Project Repository on Scm (Github)

```
To set up our project repository, we created a github organization with the name
SNE 22 - INNOPOLIS, and then we created a repository DVNA_RP 1 by forking the
vulnerablehttps://github.com/appsecco/dvnaproject.
```
```
Figure 4. 0 : Adding A SNYK Installation
```

```
To create a similar organization, use thisguide. To create your own repository, use this
guide.
```
### III. Integrating IDE (VScode) with SCM (GitHub)

```
Withtheneedtolocallycreate,modifyandmanagefilesontherepositorycreatedearlier
on github, comes the necessity to integrate VScode with github.
```
```
We managed this integration by following thisguide.
```
### IV. Set up CI/CD pipelines Using Jenkins

```
In the course of our implementation, we built the following pipelines:
```
```
● RP1 Build and Test Job
● RP1 Deploy To Test Environment Job
● RP1 Deploy To Production Job
```
```
Figure 5. 0 : CI/CD Workflow
```

We created functional pipelines by following thisguide.

It is important to note that our pipeline configuration scripts (Jenkinsfile)arein the
projectrepositoryongithubandtherefore,the "Pipeline scriptfromSCM"featurewas
deployed.

Also,Jenkinschecks the github repositoryeveryminutefornewcommits(changes),in
order to trigger a build job in the pipelines as shown in the image below.

The content ofeach pipeline’s configuration script was created anditeratedusingthe
Jenkins **Snippet Generator** as the primary tool**.**

```
Figure 5. 1 : CI/CD Pipelines
```
```
Figure 5. 2 : Setting the frequency of polling from GitHub
```

```
Figure 5. 3 : Vault Plugin Installation
```
### V. Secret Management Using Hashicorp Vault

```
Figure 6. 0 : Overview of Vault Implementation
```
Duringthe course of implementingthisproject,weusedtheHashicorpvaultforsecret
management;asweneededasecurelocationoutsideofthejenkinsservertocentrally
manage and store these secrets.


We made use of the following installation steps to implement the Hashicorp Vault:

```
● Installing Hashicorp Vault Plugins
● Installing the Hashicorp Vault Linux Server and Starting the Server
● Create an AppRole Credential and Connect with the Jenkins Server
● Add the Vault Script to the CI/CD Pipeline script
```
#### 1 Installing Hashicorp Vault Plugins

```
● Fromyour Jenkinsdashboard,goto Manage Jenkins > Manage Plugins and
select the Available tab.
● Search for Hashicorp Vault
● Install the plugin.
● ConfirmthatthePluginhasbeeninstalledbygoingto ManageJenkins>Manage
Plugins > Installed Plugins
```
```
Figure 6. 1 : Vault Plugin Installation
```
#### 2 Installing Hashicorp Vault In Ubuntu Server

WeinstalledtheHashicorpvaultapplicationbycompilingfromsourcecode,usingthefollowing
guide.

We configured the freshly installed vault instance by following thisguide.

Toenableremoteaccesstoourvaultinstallation,wechangedthelisteneraddressfrom
127. 0. 0. 1 : 8200 to 0. 0. 0. 0 : 8200 as shown in the image below.

WecanruntheauthenticationprocesstothevaultserverandconfiguretheWebUIusing
thisdocumentation.


```
Figure 6. 2 : Enabling Remote Access in config.hcl
```
```
Figure 6. 3 : Showing Vault Application Running
```
#### 3 Create an AppRole Credential and Connect with the Jenkins Server.

AnApprolecredentialisneededtoauthenticatethejenkinscontrollertothevaultrunning
instance.
To get therole_idand thesecret_idneeded for thisApprole configuration, follow this link


```
Figure 6. 4 : Showing Approle Credential
```
ThenextthingtodoistoconfigurethevaultpluginandbindittotheVaultURLasshown
in the image below.

```
Figure 6. 5 : Vault Plugin Configuration in Jenkins
```
#### 4. Add the Vault Script to the CI/CD Pipeline Script

We will be using this Hashicorp vault to secure the secrets that are hardcoded in the jenkinsfile
running our CI/CD pipeline so that we can keep the secrets secured from unwanted and
unauthorized users. We will be using the vault to secure the Telegram token and docker
credentials.
The below picture gives the snapshot of our Hashicorp Web UI and the configuration setting of a
vault in the Jenkinsfile.
Our Hashicorp vault is running onhttp://10.1.1.68:8200/and the jenkinsfile is given in thisrepo

```
Figure 6. 6 : Hashicorp Vault Credentials
```

```
Figure 6. 7 : Configuration of Hashicorp in Jenkins Pipeline
```
### VI. Introduction of SAST in Project (Snyk)

```
For SAST on our code repository, we made use of the Snyk application.
We integrated this with our code repository following the instructions availablehere.
```
```
Aftersuccessfully followingtheinstructions,a scan shouldbe initiatedontheselected
repositories, with the result as shown in the below image.
```
```
Figure 7. 0 : Getting the Organization API Key
```

### VII. Introduction of Dependency Check in Pipeline Using Synk

```
We introducedSynkin ourpipelinetorundependencychecks onthebuiltapplication
image and all of its dependencies (eg. database).
```
```
Thiswasdoneafterbuildingandtest-runningtheapplicationcode.Thetestisalsodone
before pushing the image to our artifact repository (docker hub),asis shown inthe
jenkinsfile_buildfileoftheprojectrepository.WeconfiguredSynktostopthepipelineifa
critical vulnerabilityis detectedupon scanning;consequentlystoppingtheimagefrom
being pushed to the artifact repository.
```
#### 1. Add Snyk Security to your project

```
For Snyk integration and configuration in thejenkins (CI/CD)server,wefollowedthe
instructions providedhere.
```
```
Snippet Generator was used to generate the groovy pipeline syntaxwhichwethen
added to the job script as shown in the image below.
```

```
Figure 8. 0 : Generating Groovy syntax for the pipeline script
```
Below is an image showing the Dependency Check Stage in our pipeline script using Synk:

```
Figure 8. 1 : Dependency Scan Stage
```

#### 2 Run a build and view your Snyk report.

Oncetheabovestepsarecompleted,Snykwillrunthesecurityscanonthespecifiedfile
and generate the scan results which can be accessed in 3 ways:
● A html file accessible from the job’s view.
● A Snyk Security Report, available from the sidebar when in the builds page
● ReportsenttotheSynkdashboardoftheorganizationorpersonalaccountused
for the integration.

```
Figure 8. 2 : Snyk Scan Results accessed from job view
```

Figure 8. 3 : Snyk Scan Result accessed from build page


```
Figure 8. 4 : Snyk Scan Result accessed from snyk Dashboard
```
```
With this said, Snyk was successfully integrated into the DevOps chain for Static
Application Security Testing and dependency check.
```
### VIII. Pushing Build to Artifactory

#### 1. Setting up Docker Hub Account

```
To store or project artifacts, we createdadocker hubaccountforourproject anda
private container repository on our account by following thisguide.
```
```
Figure 9. 0 : Docker Hub account
```

#### 2. Integrating in Pipeline

```
For this integration, we instructed Jenkins to perform the following operations as shell
commands:
```
```
● Docker login to give Jenkins access to the repository.
● Image tagging to append the docker hub account at the prefix and the
image version at the sux.
● Docker push operation to upload the docker image to the docker hub
repository.
```
```
This is done at the Push stage in our pipeline, just after passing the Synk tests. Below
image depicts the above steps as shown in thejenkinsfile_buildfile.
```
```
Figure 9. 1 : Pushing image to Docker Hub
```
### IX. Deployment of Application Build to Test Environment

```
To achieve this, we went through the following steps:
```
```
● Installed an Ubuntu virtual machine on our hypervisor to serve as the Test Server.
● We added the Test Server as a Jenkins agent node following thisguide.
● We created aJenkinsfile_deploy_testscript to managedeployment to the Test
Server.
```

```
Figure 10. 0 : Showing Test Server as Jenkins Agent Node
```
Figure 10. 1 : Successful Pipeline Deployment to Test Server

```
Figure 10. 2 : Showing Application Running on Test Server
```

**NB:** It is important to note that theJenkinsfile_deploy_testfile manages installation of the
docker application on the test server, therefore; there is no need to manually install docker on
the server.

### X. Introduction of DAST in Test Pipeline Using StackHawk

We chose to work with Stackhawk as our DAST tool to test the deployed application in the
test environment. A full documentation on how to integrate it with jenkins is availablehere.

Overall this integration involved 3 steps:
● Creation of a StackHawk account for our project
● Creating a jenkins credential to store our stackhawk API Key
● Adding a code chunk to theJenkins_deploy_testfileto run the DAST on test server

The figure below shows the stage in this file responsible for the test:

```
Figure 11. 0 : Jenkins script for DAST
```

```
Figure 11. 1 : StackHawk Dashboard
```
```
Figure 11. 2 : StackHawk Scan Result
```
### XI. Setting up Deployment Pipeline to Production

```
To achieve this, we went through the following steps:
```
```
● Installed an Ubuntu virtual machine on our hypervisor to serve as the Production
Server.
● We added the Production Server as a Jenkins agent node following thisguide.
● We created aJenkinsfile_deploy_prodscript to managedeployment to the Test
Server.
```

```
Figure 12. 0 : Showing Production Server as Jenkins Agent Node
```
### XII. Introducing Telegram Alerting in CI/CD

```
For alerting purposes, we decided to implement the telegram alerting system to receive
notifications to our team telegram chat to inform on the status of build projects in jenkins.
```
```
For achieving this, we followed the documentation provided by jenkins onthislink.
```
```
We did configure our bot to send notifications to our chat considering 3 scenarios :
● Notify the team if a job is Started
● Notify a team if a job is completed Successfully
● Notify the team if a job Failed
```
```
Integrating this in our pipeline was done as could be seen on the images below:
```
```
Figure 13. 0 : Send Alert on job Start
```

```
Figure 13. 1 : Send Alert on job Success
```
```
Figure 13. 2 : Send Alert on job Failure
```
```
It is to be noted that these stages were included in all the pipeline scripts so as to keep
alerted of the overall workflow.
```
### XIII. Configuring Application/Environment Monitoring

```
For the monitoring section of our project, we decided to implement both host and
containermonitoringbecauseitallowsustogaininsightsintotheperformanceofyour
systemsandmakeinformeddecisionsaboutcapacityplanning,troubleshootissuesand
ensurecomplianceandsecurity.Also,itcanhelptoreducecostsandoptimizeresource
usage.
```

OurtechnologystackforachievingthistaskwasbasedonPrometheus,cAdvisor(short
forcontaineradvisor),andGrafanawhicharepopularopen-sourcetoolsthatcanbeused
together to monitor the performance of hosts and containers.

Bycombiningthesethreetools,wedidgainacomprehensiveviewoftheperformanceof
ourhosts andcontainers,andbe abletomonitorandalert onanypotentialissuesin
real-time.

```
Figure 14. 0 : Monitoring Architecture
```
#### 1 Host Monitoring

TomonitorahostusingPrometheus,youneedtofirstsetupanexporterthatcancollect
metricsfromthehost.TherearevariousexportersavailableforPrometheus,suchasthe
Node Exporter or the Blackbox Exporter.
Forourproject,we’llbeusingthe **NodeExporter** whichisanexporterforhardwareand
OS metrics with focus on providing metrics about the host machine. It does export
metrics such as CPU usage, memory usage, disk usage, network trac, and more.

Addedtothiswe’llconfiguresomealertingrulesandconfigureemailalertingtoinform
teams of the host status.


Acompleteinstallationguideforprometheus,node_exporterandalertmanageronlinux
systems are available in the following documentations:

```
● Prometheus Installation Guide
● Installing Prometheus node-exporter
● Installing and configuring alert manager
```
Toruneachofthesetools,anexecutablefileisavailableinthedownloaddirectorybutthis
has to be done manually each time servers are brought up. For automation of this
process,wewrotesystemdservicefilesforenablingautolaunchingofthesescriptseach
timetheserversarepoweredon.Below imagesshowthesystemdfileswrittenforthis
purpose:

```
Figure 14. 1 : Systemd Service file for Node Exporter
```
```
Figure 14. 2 : Systemd Service file for Prometheus Server
```
Now prometheus could be accessed via a web browser on [http://](http://) 10. 1. 1. 30 : 9090.
Prometheusnowrunningwewilledititsconfigurefiletodefinethetargetstomonitor.Still
in the prometheus folder, we’ll edit the file **prometheus.yml to add the following
sections in order to define the target hosts :**


```
Figure 14. 3 : Defining Target hosts on Prometheus
```
In theabove image,weconfiguredthe prometheus servertocollectdataexposedby
node exporters installed on theproduction serverand alsoon theprometheus server
itself.

Now if connecting to [http://](http://) 10. 1. 1. 30 : 9090 and navigate to **status > targets,** we’ll be
havingalistofalltargetsandendpointmanagersconfiguredtoexporttheirdataand
metricstoprometheusandalsotheirstate(UPorDOWN)ascouldbeseenonthefigure
below :

```
Figure 14. 4 : Target Hosts
```
Nextweconfiguredalertingforthemonitoredhoststoreceiveanemailnotificationeach
timeoneofthemgoesdownorwhendiskspacereachesorbecomeslessthan 50 %.These
are known as **Alerting Rules**.


Prometheusdoesincludeabuilt-inquerylanguage,called **PromQL** ,thatallowsusersto
define alerting rules that triggerwhen certainconditionsaremet.These rulescan be
definedinafile,usuallycalled" **prometheus-rules.yml** ",whichistypicallylocatedinthe
Prometheusconfigurationdirectory.Thisfilewillthenbereferencedintheprometheus.yml
filewhichistheconfigfile foruse.Belowistheprometheusrulesfileshowingwhichrules
we defined for notifications about the hosts :

```
Figure 14. 5 : Alerting Rules
```
Final step for host monitoring was to install and configure an alert manager. The
PrometheusAlertmanagerisaseparatecomponentofthePrometheusmonitoringsystem
thatisresponsibleforhandlingandroutingalertsthataregeneratedbyPrometheus.It
takes alerts from Prometheus andsendsnotificationstotheappropriaterecipientsor
channels, such as email, Slack, or PagerDuty.

Toachievethisweranthefollowingcommandstodownloadandexecutetheprometheus
alertmanager :

wget
https://github.com/prometheus/alertmanager/releases/download/v0.25.0/alertmanag
er-0.25.0.linux-amd64.tar.gz
tar xzf alertmanager-0.25.0.linux-amd64.tar.gz
cd alertmanager

Nextwe editthefile **alertmanager.yml** toconfigurethelistof recipients forthealerts
generated by prometheus as follows :


```
Figure 14. 6 : Alerts Recipients list
```
Figure 14. 7 : AlertManager Systemd service file


```
Figure 14. 8 : Instance down alert received by mail
```
Overall,we’ve configuredPrometheustomonitorourdierenthostsandsendalertsto
teammemberswhenoneoftheinstancesgoesdownthusprovidingvaluableinsightsinto
the performance of your systems.


```
Figure 14. 9 : Referencing AlertManager and Rules file
```
#### 2 Container Monitoring

Asmentionedearlier, **cAdvisor** isacontainermonitoringtoolthatrunsasadaemonon
the host andcan collect metricson CPU,memory,network,andstorageusageofthe
containers running on that host.It also provides additional information such as the
process tree and image subcontainers.

Generally,tosetupcontainermonitoringwithcAdvisorandPrometheus,youwouldfirst
needtoinstallcAdvisoronthehostandconfigureittorunasadaemon.Then,youwould
needtoconfigurePrometheustoscrapemetricsfromcAdvisorbyaddingthecAdvisor
endpoint to the Prometheus configuration file.

To achieve this, go through the following steps :

```
● First,you'llneedtoconfigurePrometheustoscrapemetricsfromcAdvisor.Editthe
prometheus.yml file and populate it with this configuration :
```

```
Figure 15. 0 : Defining cAdvisor as target on prometheus server
```
● NextcomescAdvisorinstallationontargets.We’llbedownloadingcAvisorfromthe
ocialdockerimage.Inthesamefolderwheretheprometheus.ymlfileislocated,
we’llcreateadocker-compose.ymlfileandpopulateitwiththisDockerCompose
configuration :


```
Figure 15. 1 : Docker-compose file to run cAdvisor
```
This configuration instructs Docker Compose to run two services, each of which

corresponds to aDockercontainer :

```
➢ The cadvisor service exposes port 8080 (the default port for cAdvisor
metrics) and relies on a variety of local volumes (/, /var/run, etc.).
➢ TheredisserviceisastandardRedisserver.cAdvisorwillgathercontainer
metrics from this container automatically, i.e. without any further
configuration.
```
To run the installation, typedocker-compose up.

Withthis,thecontainermetricswillbeexposedtotheprometheusserverformonitoring.

Below is an image ofall theoveralltargetsconfiguredon prometheus sofarforour

host/container monitoring.


```
Figure 15. 2 : Prometheus Targets
```
#### 3 Visualization with Grafana

Grafanaallowsyoutocreatedashboardswithvarioustypesofchartsandpanels,andit
supportsqueryingPrometheusfordatatodisplay.Additionally,Grafanacanalertbased
on the data from Prometheus, which allows you tosetupnotifications whencertain
conditions are met.

Sofirstwe’llstartbyinstallingGrafana.Forlimitedresourcereasons,wedidthisonthe
same server where prometheus is installed, as follows :

Follow the guide providedherefor installing grafanaon a linux system.

Now grafana is installedandreadytouse.By default it operates onport 3000 .It is
accessibleviawebbrowserontheurl **[http://](http://) 10. 1. 1. 30 : 3000** withdefaultlogincredentials
being admin/admin.

To sign in to Grafana for the first time:

```
● Open your web browser and go tohttp://localhost: 3000 /.The default HTTP
port that Grafana listens to is 3000 unless you have configured a dierent port.
● On the sign-in page, enter admin for the username and password.
```

```
● Click Sign in.
If successful, you will see a prompt to change the password.
● Click OK on the prompt and change your password.
```
Final step will be to create a visualization dashboard. We went with downloading a

dashboard template from the linkhttps://grafana.com/grafana/dashboards/

Below image shows the grafana dashboard of our project showing the hosts and

container metrics scraped by prometheus.

```
Figure 16. 0 : Grafana Dashboard
```

### XIV. Setting up Web Application Firewall (ModSecurity)

```
When an application isdeployedtotheproductionserversandmadeavailabletoend
users, protecting the applicationfromthreatsbecomes key,hence thecallfora Web
application firewall.
```
```
Figure 17. 0 : Nginx Reverse Proxy + Web Application Firewall
```
```
Web application firewall (W.A.F) helps protectwebapplications fromvarioustypes of
cyber-attacks by sitting in front of the application and analyzing incomingtracto
detectandblockmaliciousrequests.ItprotectsagainstavarietyofattackssuchasSQL
injection, cross-site scripting (XSS), cross-site request forgery (CSRF), and common
network layer attacks such as denial of service (DoS) and brute-force login attempts.
```
```
Web application firewalls can easily be updatedtoprotect againstnewandevolving
threats.Thisisimportantinadynamicdigitalenvironment,asitprovidesanadditional
layerofsecuritythatcomplementsexistingsecuritymeasuressuchasnetworkfirewalls,
IDS & IPS, and other security tools.
```

W.A.Fs therefore playavitalrole asan integralpart of the DevSecOpstoolchain,and
organizations must ensure the security andcomplianceofhostedapplications with a
W.A.F.

Inourimplementationweused **ModSecurity** webapplicationfirewallbecauseitishighly
configurableandcan beeasilyintegratedintowebserverssuchasNginx,allowingfor
real-time monitoring and protection of web applications. Additionally **ModSecurity**
providesavarietyofbuiltinrules(i.eOWASPModSecurityCoreRuleSet[CRS])makingit
apowerfultoolforprotectingwebapplicationsagainstawiderangeofthreats.Wetook
advantage of its integration with Ngnix and its proxy,caching, master andmultiple
workerprocesscapabilitiestoenhancetheperformanceoftheapplicationtocustomers
while serving its purpose of a WAF.

The completeguide on how ModSecuritywas integratedwithnginxwebserverwill be
covered next.

#### Implementation of Modsecurity Web Application Firewall

ModSecurity has two deployment options which are embedded deployments andthe
reversedeployment.Wewentwiththereversedeploymentoptionsincetheapplicationof
interestiscontainerized.Asdiscussedpreviouslyweusednginxasthereverseproxyand
thatisbecauseofNginxmasterandmultipleworkerprocesscapabilitiestoboosttherate
at which multiple concurrent requests are being handled by the proxy server.

We installedtheModSecurityWebapplication firewall bycompilingfromsourcecode,
afterwhichweintegratedOWASPrulestoenhancethefirewallrulesusingthefollowing
guide.

```
Figure 17. 0 : Modsecurity Installed
```
```
Figure 17. 1 : Nginx Installed
```

```
Figure 17. 2 : ModSecurity files and unicode mapping added to Nginx directory
```
```
Figure 17. 3 : OWASP Core rules set integrated with modsecurity
```
AfterModSecurityhadbeeninstalledandintegratedwiththeNginxserver,Nginxproxy
capabilitieswasthenenabledtolistenforincomingrequestfromendusersonport 80 to
the containerized application; with ModSecurity WAF handling inspectionofincoming
trac as seen in the configuration file below:

```
Figure 17. 4 : Nginx reverse Proxy with modsecurity configuration
```

## Discussion

### Challenges Faced

We faced a couple of challenges during the implementation phase; a few of those are
highlighted below:

```
● Continuous iteration of jenkinsfile (configuration script)
● Limited computing resources
● Amount of Alerts send from configured SMTP server got the email address flagged
● Ease of collaboration with team mates
● Access to resources due to IP blocking via geo-tagging
● Scarcity of time for learning
```
### Improvements

```
● Introduction of vulnerability management tool: Thisbecomes necessary in
order to have all scan results in one window for all stakeholder to assess and action
on.
```
```
● Public Cloud Hosting : Migrate infrastructure to cloudin order to solve the problem
associated with limited resources and scaling.
```
```
● Separation of Services: In our case, we installedthe web application firewall on
the same hosts as the production web server. While this was done due to the
scarcity of resources, we do not recommend this practice in an enterprise
environment as it is an insecure practice.
```
```
● Security Layering: We highly recommend implementinglayered security in all
environments; most especially the production platforms by introducing security
tools like network firewall, IDS/IPS, SIEM as additions.
```
```
● Container Orchestration: Running the application ondocker engine might not be
the most ecient way to go about things. We highly recommend the use of
container orchestrators like Kubernetes in order to enjoy features like auto-scaling
and ease of rolling out upgrades.
```

### Skills Acquired

In the course of this project, we touched on a number of development and operation
areas. Research in these areas led us to learning new technologies and sharpening our
skills on the following

```
● Containerizing applications using Docker
● Code version management using Git
● Virtualization using VMware ESXi
● Implementation of web application firewall and application proxying using
ModSecurity and Nginx
● Configuring CI/CD pipelines using Jenkins
● Scripting using groovy syntax
● Artifact management using Docker Hub
● Application security tests using Snyk and Stack Hawk as SAST and DAST
respectively.
● General understanding of DevOps and DevSecOps concepts and workflow
● Application of this knowledge in real-life industry projects
● Monitoring container applications using Prometheus, Grafana and cAdvisor
● Secret management using Hashicorp
```
### Conclusion

The project was successful and covered a lot of topics, while requiring a lot of learning.
Irrespective of the challenges faced, we succeeded in delivering on every item in our
action plan within the space of 15 days.

We do hope that the content of this report serves as an instructive guide to anyone with
need to replicate any or every part of our work. To know more about the DevSecOps
concept, you can read extensively from the resources provided in the references session.

Our presentation related to this project can be foundhere.


## References

● https://www.atlassian.com/devops/devops-tools/devsecops-tools
● https://modsecurity.digitalwave.hu/
● https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/
● https://docs.github.com/en/organizations
● https://docs.snyk.io/integrations/git-repository-scm-integrations/github-integration
● https://prometheus.io/docs/guides/cadvisor/#monitoring-docker-container-metrics-using-
cadvisor
● https://prometheus.io/docs/alerting/latest/configuration/
● https://developer.hashicorp.com/vault
● https://docs.docker.com/
● https://www.jenkins.io/doc/
● Implementing DevSecOps Tool Chain using Open Source Tools.mp4


