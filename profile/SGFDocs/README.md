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

# Build and Run Market Delivery Project

**Prerequisites:**
- If you haven’t already done so, install cmake by running the cmake install msi file located in the <proj repo dir>\Platform\ThirdParty\Archives\Installed directory.
- The Market Delivery Project to be built (example: proj-vlt-alc) has been cloned. Be sure to clone recursively to ensure all submodules are cloned.

## Windows Build and Run

### Creating and Building Visual Studio Solution
- Run <proj repo dir>\Platform\ThirdParty\install.bat install ThirdParty libraries.
- Run <proj repo dir>\CIBuildScripts\run_cmake.bat to create the Visual Studio solution.
- Upon the successful completion of the run_cmake.bat script, open the ‘VLT_Mainline.sln’ located in the build directory (example: CIBuildScripts\build_vs2022_x64) and perform a Debug build of the solution.  
NOTE: You can continue on and perform the ‘Setup Test Games’ step while this solution is building.


### Setup Test Games
- Clone the igt-gsp/testgames-sgf Github repository.
- Create a System environment variable named CONTENT_PROJECT_ROOT and set its value to the full path to the ‘Content' directory located at the root of the testgames-sgf repo directory (example: E:\Github\testgames-sgf\Content).

### Run the SGF Platform
- Because the CONTENT_PROJECT_ROOT environment variable was added after we opened VLT_Mainline.sln, the VLT_Mainline.sln must be closed and re-opened to pickup this new environment variable.
- From within the VLT_Mainline.sln, right click on the Platform->SGF->GOOFExecutiveControl project and select “Set as Startup Project”.
- You can now run/debug (Debug->Start Debugging) the solution.

## Virtual VLT Testing Tool
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


<!--<details>
<summary><strong>Windows Build and Run </strong></summary>
</details>-->

CloneMarketDeliveryProject.mp4:
https://github.com/user-attachments/assets/7a1a999a-e7bc-4991-8e95-00848876f9a1

GitExtensionsCloneSubmodules.png:
<img width="650" height="568" alt="GitExtensionsCloneSubmodules" src="https://github.com/user-attachments/assets/344175d5-2796-411d-a06c-d9a3ba5c7faa" />

PullExistingLocalRepository.mp4:
https://github.com/user-attachments/assets/79070bec-8306-4bdc-a2f9-a92bfd7592ff

CreateFeatureBranches.mp4:
https://github.com/user-attachments/assets/d382f2e2-6d52-4679-8939-ba503f16ef4f

CodeModifications.mp4:
https://github.com/user-attachments/assets/7148f894-506f-42c7-937a-5fc8e2ad6ae6

CommitAndPushSubmoduleChanges.mp4:
https://github.com/user-attachments/assets/d67099fc-f2d2-46fd-9037-62a0c858f84a

CommitAndPushSupermoduleChanges.mp4:
https://github.com/user-attachments/assets/6d46209b-1153-4bf7-85c9-fce634619ddd

RunGithubActionsFBWBuild.mp4:
https://github.com/user-attachments/assets/80ebeb2f-ff22-455b-9584-7947e42605c1






		
		
