# SGF Platform Repositories Overview

The SGF Platform repositories can be broken down into the following categories.

- **Common Repos** - set of repositories that are used across market deliveries
	- **Core Platform Repos** - SGF core functionality repos
		- *platform-sgf* - repo containing the core SGF platform functionality
		- *platform-thirdparty* - repo containing open source thirdparty libraries
		- *licenses-sgf* - repo containing thirdpary libray licensing information
		
	- **Protocol Repos** - set of repositories for communicating to various host systems.
		- *protocol-g2s* - protocol for EGM to communicate with G2S host system
		- *protocol-sas* - protocol for EGM to communicate with SAS host system
		- *protocol-mdi* - protocol for platform to communicate with media display browers
		- *protocol-eipp* - 

		
	- **Microcontroller Repos** - set of repositories .
		- *unv-svc-\** - set of universal services repositories
		
	- **GSN Extension Apps** - Platform extension apps based on GSN
		- *gsn-topper-app* - extension app for communication to the topper.
		
- **Market Repos** - repositories containing market specific functionality.  These repositories follow the naming convention of "market-[product type]-[market name]".  Currently accepted product types are 'VLT' and 'AWP'.  Examples: market-vlt-alc, market-awp-spain

- **Market Delivery Project Repos** - These repositories essentially bring together the Market Repo and some subset of the Common Repos to create the directory strucure required to build and deliver the SGF Platform for a specific market.  These repositories follow the naming convention of "proj-[product type]-[market name]".  Examples: proj-vlt-alc, proj-awp-spain

The following is a breakdown of how a Market Delivery Project is assembled.
```
proj-vlt-xyz/             # Market Delivery Project Repo for VLT product and XYZ market
├── Market/               # Submodule reference to the market-vlt-xyz repo (required)
├── OpenSourceLicenses/   # Submodule reference to the licenses-sgf repo (required)
├── Platform/             # Submodule reference to the platform-sgf repo (required)
│   ├── ThirdParty/       # Submodule reference to the platform-thirdparty repo (required)
├── Protocol/
│   ├── G2S/              # Submodule reference to the protocol-g2s repo (optional depending on market)
│   ├── MDI/              # Submodule reference to the protocol-mdi repo (optional depending on market)
│   ├── SAS/              # Submodule reference to the protocol-sas repo (optional depending on market)
│   ├── EIPP/             # Submodule reference to the protocol-eipp repo (optional depending on market)
├── GSNApps/
│   ├── GSNTopperApp/     # Submodule reference to the gsn-toppper-app (optional depending on market)
│   ├── ...               # Submodule references to other GSN Extension App repos (optional depending on market)
├── MicroController/
│   ├── Core/             # Submodule reference to the unv-svc-core (optional depending on market)
│   ├── EGMClient/        # Submodule reference to the unv-svc-egm-client (optional depending on market)
│   ├── ...               # Submodule reference to other Microcontroller Repos (optional depending on market)
```


# SGF Development Process
The SGF Development Process is based on the Git feature branch workflow.  Please read the information at the following link to have a good foundation for the details to follow.

[***<ins>Git feature branch workflow</ins>***](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)

The following is a breakdown of the general steps to be used for the SGF Development Process.

- **Sync Market Delivery Project -** bring you local market delivery project (i.e. proj-vlt-aglc) up to date with the Github repo via git clone command (no local repo exists) or git pull command (updating an existing repo).
- **Create Feature Branches -** Create feature branches for the super module and for all submodules that will be modified as part of the feature development task.
- **Development Work -** At this point all the development tasks are performed to complete the implementation and unit testing of the feature development task.
- **Pull Request Process for Modified Submodules -** Go through the Github pull request process for each modified submodule such that all changes are reviewed. 

The followings sections provide more detail for each of the above steps.  

NOTES:  
- In the following sections, an example of above the SGF Development Process for a feature called “sync-aglc-with-latest-perforce-changes” will be shown.
- All git related functions are referenced in the following pages are demonstrated using the Git Extension UI tool.

## Sync Market Delivery Project  

### Clone Market Delivery Project  
If you don’t have an existing local repo for the Market Delivery Project to be worked on, you will need to clone the repository from Github.  

**Example:**

The following video is an example of cloning a proj-vlt-aglc market delivery project Github repo to a local repo. 

https://github.com/user-attachments/assets/7a1a999a-e7bc-4991-8e95-00848876f9a1

Cloning a repository containing submodules in Git Extensions will only clone the contents of the super module, it will not clone the submodules.  To clone submodules in Git Extensions, right click on the super module and select “Update”.

<img width="650" height="568" alt="GitExtensionsCloneSubmodules" src="https://github.com/user-attachments/assets/344175d5-2796-411d-a06c-d9a3ba5c7faa" />

### Pull/Update Existing Local Repository  
If you have an existing local repository that you would like to perform your feature work on, use the following steps to make sure this existing local repo is completely up to date with the remote repository.

The best way to bring the local repo up to date is to do the following.

- Switch the proj super module to the default branch (main or rel- branch).
- For each submodule:  
	- Switch to the default branch (main or rel- branch).
	- Check if there are any lingering modified files in your working directory.  These files should either be stashed or reset as you want to be starting with no changes in your working directory.
	- Do a pull command.

**Example:**

The following video shows the process of bring an existing local repo up to date and ready for the start of development on a new feature.  Please note that due to attachment file size limitations in Confluence the video ends after updating the Platform submodule, the full process would include all the submodules.

https://github.com/user-attachments/assets/79070bec-8306-4bdc-a2f9-a92bfd7592ff


## Create Feature Branches  
The next step after syncing your local market delivery project is to create a feature branch for the super module and any submodules that will be modified during the feature development task.  The following are the steps to create and push/publish the new feature branches.  

- Create feature branch for the super module.
- Push/publish the newly created branch for the super module.
- For each submodule to be modified:
	- Open the submodule repo.
	- Switch to the default branch (main or rel- branch).
	- Create the feature branch for the submodule
	- Push/publish the newly created feature branch.
- For each submodule that will NOT be modified:
	- Open the submodule repo.
	- Switch to the default branch (main or rel- branch).

**Example:**

The “sync-aglc-with-latest-perforce-changes” feature will require modifications to the Market and G2S submodules.  The following video shows the process for creating feature branches for the super module, the Market submodule, and the G2S submodule.

NOTE: The below video does not show switching to the default branch for the submodules that won’t be modified.

https://github.com/user-attachments/assets/d382f2e2-6d52-4679-8939-ba503f16ef4f

## Development Work

This step consists of the following tasks.

- Code Modifications
- Build and Run Market Delivery Project
- Commit and Push Submodule Changes
- Commit and Push Super Module Changes
- Run Github Actions Feature Branch Workflow Build

Please note the intent should be to perform these above tasks many times throughout the Development Work step building up the feature interatively.

The following sections provide more detail for each of these tasks.

### Code Modifications  
This task just requires the developer to makes the required code modifications for the feature being developed.  Unlike Perforce, Git does not require any checkouts for files to be modified, the developer just needs to make the required modifications in workspace associated with the super modules local repo (in our example, this would be E:\Github2\proj-vlt-aglc).

**Example:**

For the “sync-aglc-with-latest-perforce-changes” feature, the files modified since the last sync from Perforce for AGLC are copied to the local proj-vlt-aglc.  The following video shows how you can view the workspace modified Market and G2S submodule files.

https://github.com/user-attachments/assets/7148f894-506f-42c7-937a-5fc8e2ad6ae6

### Build and Run Market Delivery Project

**Prerequisites:**
- If you haven’t already done so, install cmake by running the cmake install msi file located in the <proj repo dir>\Platform\ThirdParty\Archives\Installed directory.
- The Market Delivery Project to be built (example: proj-vlt-alc) has been cloned. Be sure to clone recursively to ensure all submodules are cloned.

#### Windows Build and Run

##### Creating and Building Visual Studio Solution
- Run <proj repo dir>\Platform\ThirdParty\install.bat install ThirdParty libraries.
- Run <proj repo dir>\CIBuildScripts\run_cmake.bat to create the Visual Studio solution.
- Upon the successful completion of the run_cmake.bat script, open the ‘VLT_Mainline.sln’ located in the build directory (example: CIBuildScripts\build_vs2022_x64) and perform a Debug build of the solution.  
NOTE: You can continue on and perform the ‘Setup Test Games’ step while this solution is building.


##### Setup Test Games
- Clone the igt-gsp/testgames-sgf Github repository.
- Create a System environment variable named CONTENT_PROJECT_ROOT and set its value to the full path to the ‘Content' directory located at the root of the testgames-sgf repo directory (example: E:\Github\testgames-sgf\Content).

##### Run the SGF Platform
- Because the CONTENT_PROJECT_ROOT environment variable was added after we opened VLT_Mainline.sln, the VLT_Mainline.sln must be closed and re-opened to pickup this new environment variable.
- From within the VLT_Mainline.sln, right click on the Platform->SGF->GOOFExecutiveControl project and select “Set as Startup Project”.
- You can now run/debug (Debug->Start Debugging) the solution.

#### Linux Build and Run

#### Virtual VLT Testing Tool
The Virtual VLT tool allows the user to simulate things like adding money, opening/closing doors, tech/audit key access, .... The Virtual VLT tool (VirtualVLT.exe) can be found at the following location.

**Installation:**  
If the VirtualVLT has not previously been installed, extract the <proj repo dir>\Platform\SGF\Tools\VirtualVLT\VirtualVLT.7z zip file to a global location outside the <proj repo dir>.  This tool basically never changes and therefore can be used going forward for an SGF Platform you run.

**Initial Setup:**  
When you first run the VirtualVLT tool, it will be defaulted to connecting to the Core/Platform running on your local machine (i.e. 127.0.0.1). If this is the way you are using it, then there is no need to make any changes to the "IP addresses of remote target" or "IP addresses of this computer". However, if you are trying to connect to a Core/Platform running on a different computer, you must set the "IP addresses of remote target" or "IP addresses of this computer" values appropriately and press the "Set End Point" buttons.

**Features:**  
The following are the most commonly used features.
1. Money Deposit - simulating the deposit of money to the VLT.
2. Door Control - Opening and Closing of doors.
3. Key Control - Audit and Tech key control for access to the backoffice.

<img width="662" height="691" alt="image" src="https://github.com/user-attachments/assets/2ec3e3f2-ba3c-4b5c-b67e-1c286d145263" />

### Commit and Push Submodule Changes
Now that some code changes have been implemented and unit tested, you can now push the submodule changes to Github.  Please note that since you are working on a feature branch there should be no concern about “breaking the build” for others and therefore committing and pushing to Github should be done often.

**Example:**

The following video shows the committing and pushing to Github of the Market and G2S submodule modifications for the  “sync-aglc-with-latest-perforce-changes” feature.

https://github.com/user-attachments/assets/d67099fc-f2d2-46fd-9037-62a0c858f84a

### Commit and Push Super Module Changes  
At this point you may be wondering why there are any super module changes to be committed/pushed since we haven’t explicitly made an super module changes.  The way that git submodules work is that the repository that contains one or more submodules (what we have been calling the super module) keeps a commit reference for each of its submodules.  In other words, the super module is always referencing a specific snapshot in time (a specific commit) for each of its submodules.  Therefore, the only way for the super module to have knowledge of the changes we have made to the submodules is to commit and push that latest submodule commit referencing to the super module repository.

**Example:**

The following video shows the commit and push of the super module changes.

https://github.com/user-attachments/assets/6d46209b-1153-4bf7-85c9-fce634619ddd


### Run Github Actions Feature Branch Workflow Build
The running of the Feature Branch Workflow in Github Actions essentially allows the developer to build and package the current state of the feature branch.  This can be thought of as something equivalent to CI builds in Jenkins.  The following are the steps to run the feature branch workflow 

- Go to the super module repository in Github
- Select the “Actions” tab
- Find and select the Actions Workflow that is named FeatureBranchWorkflow or the workflow that ends with “_fbw” (feature branch workflow).
- Press the “Run workflow” dropdown menu and choose the branch you want the workflow run on and then press the “Run workflow“ button.

**Example:**

The following video shows the Github Actions Feature Branch Workflow being run on the “sync-aglc-with-latest-perforce-changes” branch of the proj-vlt-aglc repository.

https://github.com/user-attachments/assets/80ebeb2f-ff22-455b-9584-7947e42605c1


## Pull Request Process  
After the Develop Work for the feature has been completed, the next step is to go through the pull request process to ensure your changes are ready to be merge back to the main branch.  The following diagram provides an overview of the pull request process.

<img width="943" height="446" alt="image" src="https://github.com/user-attachments/assets/3f978fa2-65d7-47d5-8ccd-93021f9a2a1d" />

### Pull Request Mod
After feature or bug fix implementation is complete, the first step initiate the start of the pull request process is to open (or update an existing) a pull request.  The following steps detail how to create/open a pull request.

The following are the steps to open a pull request in Github.
- Create Jira issue for the feature developed.
- Go to the repository where the pull request is to be opened.
- Select the branch the pull request is to be created against.
- Press the “Contribute” dropdown and then press the “Open pull request” button.
- Add an appropriate title for the pull request.
- Specify the Jira issue in the description->Jira Issue field.
- Press the “Create pull request” button.
- Add appropriate reviewers for the feature developed.

**Example:**

The following example video shows the opening of a pull request in the protocol-g2s Github repository which is the repository associated with the G2S submodule.  For the “sync-aglc-with-latest-perforce-changes” feature, this same process would need to be repeated for the market-vlt-aglc Github repository.

https://github.com/user-attachments/assets/56686eae-64e1-4dbb-890a-0a46f6b69616

### Continuous Integration  
Upon modification to the pull request, a continuous integration pipeline will be triggered that validates the pull requests changes by performing the following checks.

- Component Build
- Unit Testing
- Static Code Analysis

#### Component Build  
This check validates that the code modifications associated with the pull request did not introduce any build issues.  A failed pull request ‘Build’ check will look like the following.

<img width="678" height="555" alt="image" src="https://github.com/user-attachments/assets/a6127582-fbc5-4203-9930-5c6aef4ccabe" />

All failed pull request ‘Build’ checks must be fixed before continuing.

#### Unit Testing  
A series of unit tests are run to validate the runtime functionality of the component.  A failed pull request ‘Automated-Tests’ check will look like the following.

<img width="682" height="586" alt="image" src="https://github.com/user-attachments/assets/526392da-493b-457b-a33a-1d0823c146b9" />


All failed pull request ‘Automated-Tests’ checks must be fixed before continuing.

Known Issues:  
- There is an occasional platform crash that occurs, this is indicated by a “GOOF crash suspected” message in the CI pipeline Job Summary Info (see below image).  The developer should retrigger the pull request CI pipeline (close and then reopen the pull request) to ensure this is the known platform crash.  This crash occurs very rarely, therefore multiple platform crashes in a row is an indication that the pull request changes may have introduced a platform crash and therefore should be investigated.

<img width="795" height="390" alt="image" src="https://github.com/user-attachments/assets/d4ceff04-85f6-44cc-83be-b8d0d8075fef" />

- The 'Automated-Tests' will occasionally hang in the GOOFUtilitiesTest. A retrigger the pull request CI pipeline (close and then reopen the pull request) will be required.

#### Static Code Analysis
SonarQube static code analysis scan is performed to validate that no unwanted code quality issues have been introduced.  A failed pull request ‘SonarQube’ check will look like the following.

<img width="653" height="580" alt="image" src="https://github.com/user-attachments/assets/a443a502-3cac-45fa-a59c-f8c6a612c52d" />

A link to the SonarQube scan results can be found in the 'Job Summary Info” output of the CI pipeline.

<img width="717" height="246" alt="image" src="https://github.com/user-attachments/assets/2247a993-9782-4ce1-beda-91d509cc8cbb" />

Following this link will bring you to a page that looks like the following.

<img width="1081" height="496" alt="image" src="https://github.com/user-attachments/assets/7566a0fe-bfa8-4507-8030-12e6cd494211" />

The developer is responsible for making sure that any new issues (other then Code Smells, see note below) are resolved with one of the following statuses.

- Resolve as fixed
- Resolve as false positive
- Resolve as won’t fix

NOTE: Code Smells can be ignored.

### Code Review  
The developer is expected to work with the reviewer(s) to resolve any issues/concerns the reviewer(s) may highlight.  Any code changes that come out of this review process are expected to go through the Development Work steps.  

When the pull request is approved by at least one reviewer, the pull request status will change from something that looks like the following.

<img width="860" height="267" alt="image" src="https://github.com/user-attachments/assets/a22e6e37-2042-403b-85f5-edbb8e651390" />

To something that looks like the following:

<img width="928" height="297" alt="image" src="https://github.com/user-attachments/assets/8f45ea91-b8f9-4e64-8240-885202432c97" />


### Merge Pull Request
After the pull request reviews are approved, the next and final step is to merge the pull request changes back into the main branch.  The “Squash and merge“ pull request merge type is the recommended option to be used.

**Example:**

The following video shows the merging of the market-vlt-aglc pull request and the protocol-g2s pull request associated with the “sync-aglc-with-latest-perforce-changes“ feature.

https://github.com/user-attachments/assets/631099ea-abfe-4d71-8116-4f8f151a0916




