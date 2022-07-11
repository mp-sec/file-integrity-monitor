# file-integrity-monitor
# Forewards 
This is a proof of concept, and I am inexperienced with Powershell scripting. Additionally, I built the Windows 10 machine VM used for this from an ISO file generated from the media creator tool from Microsoft: https://www.microsoft.com/en-us/software-download/windows10. I used Virtual Box for running the image, but it shouldn't matter what you use for the virtualization. 

# Creating VM and Environment
In the fresh VM, I created a folder called FIM for the project on the Desktop. Inside of the FIM folder I created a .ps1 script file for the FIM itself, and a folder called Files that will contain three files that will be checked by the FIM. 
![image](https://user-images.githubusercontent.com/99374038/178180707-d30ec7ff-9ea2-4a5a-8c6c-506f38b7e267.png)
The Powershell script will check specifically for this folder structure so if you want to use this, then you will need to make the appropriate edits to the script file to go to the right place. 

# Unable to Run Script 
If running the script returns an error regarding about_Execution_Policies, you can use the command *Get_ExecutionPolicy -list* to see the current policy states: 
![image](https://user-images.githubusercontent.com/99374038/178181179-ad8e0003-5ad8-4afb-a88f-2716b2292c14.png)
This can be corrected by going to the script settings on Windows 10:
![image](https://user-images.githubusercontent.com/99374038/178181576-9a1866c9-4267-462c-b420-927d6a60c08a.png)  You need to ensure this setting is enabled and applied, which will end up looking like this when it is:
![image](https://user-images.githubusercontent.com/99374038/178181626-52bc71aa-2ba4-4200-85f9-90dd0373b3aa.png)
Powershell scripts can now be run locally. 

# Usage 
When running the script, the user will be prompted with either getting the current hashes of the files or enabling the FIM to monitor for hash changes in the files. Collecting the hashes will create a new file in the FIM directory called FIM-hashes.txt:
![image](https://user-images.githubusercontent.com/99374038/178183007-e423a201-c16b-43c8-af61-6a8ec30f52c8.png)
The formatting within the file is (filepath)|(file hash). 

Enabling the FIM will create a persistent monitor that checks for hash changes every second for all of the files in the Files folder, and create a simple alert to say as much. To provide an example, I ran the FIM before changing the contents of one of the files in the File folder. This caused the following error message to appear every second: 
![image](https://user-images.githubusercontent.com/99374038/178183910-9d6c17dd-6c84-4699-862f-13572b7b41db.png)
