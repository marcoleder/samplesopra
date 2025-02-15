# Getting Started

### MacOS, Linux and WSL
If you are using MacOS, Linux or WSL(Windows-Subsystem-Linux), you can skip directly to the [installation part](https://github.com/marcoleder/samplesopra/blob/main/README.md#installation)

### Windows
If you are using Windows, you first need to install WSL(Windows-Subsystem-Linux). You might need to reboot your computer for the installation, therefore, save and close all your other work and programs

1. Download the following [powershell script](./windows_prerequisites.ps1)\
![downloadWindowsScript](https://github.com/user-attachments/assets/9985eb1a-32a3-47c3-964c-a18ba5f92683)

---
2. Open a new powershell terminal **with admin privileges** and run the following command and follow the instructions. Make sure that you open the powershell terminal at the path where you have downloaded the powershell script, otherwise the command will not work because it can not find the script. You can list currently accessible files in the powershell terminal with ```dir``` and you can use ```cd``` to navigate between directories
   ```shell
   C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -ExecutionPolicy Bypass -File .\windows_prerequisites.ps1
   ```
---
3. If you experience any issues, try re-running the script a couple of times. If the installation remains unsuccessful, follow this [youtube tutorial](https://youtu.be/GIYOoMDfmkM) or post your question in the OLAT forum
---
4. After successful installation, you can open WSL/Ubuntu. You will need to choose a username and password, although no characters will be shown on the screen when typing the password but the system recognizes your input, no worries :) After these four steps your setup should look similar to [this picture](./initialUbuntuSetup.png)


# Installation
1. Open a new MacOS, Linux or WSL(Windows-Subsystem-Linux) terminal. Make sure you have git installed, you can check that by running
   ```shell
   git --version
   ```
   The output should be something similar to ```git version X.XX.X```, if not, try to install git in one of the following ways
   #### MacOS
   ```shell
   brew install --formulae git
   ```
   #### Linux/WSL
   ```shell
   sudo apt-get install git
   ```
   If you are not using Ubuntu, you will need to install git with your package manager of choice
---
2. Clone the repository with git using the following command
   ```shell
   git clone https://github.com/HASEL-UZH/sopra-fs25-template-client
   ```
---
3. Navigate to the cloned directory in the terminal, in example with ```cd sopra-fs25-template-client```
---
4. Inside the repository folder (with ```ls``` you can list files) there is a bash script _setup.sh_ that will install everything you need, according to the system you are using. Run the following command and follow the instructions
   ```shell
   source setup.sh
   ```
The screenshot below shows an example of how this looks
![sourceScript](https://github.com/user-attachments/assets/01059677-8aff-4875-b66d-8086be15af43)

The installation script _setup.sh_ can take a few minutes, please be patient and do not abort the process. If you encounter any issues, please close the terminal and open a new one and try to run the command again

# Troubleshooting the installation
If the four steps above did not work for you and re-running the setup.sh script a couple of times did not help, try running the following steps manually
1. Open a new MacOS, Linux or WSL(Windows-Subsystem-Linux) terminal and navigate to the repository with ```cd```. Then ensure that curl is installed
   ```shell
   curl --version
   ```
   The output should be something similar to ```curl X.X.X```, if not, try to install curl in one of the following ways
      #### MacOS
   ```shell
   brew install --formulae curl
   ```
   #### Linux/WSL
   ```shell
   sudo apt-get install curl
   ```
   If you are not using Ubuntu, you will need to install git with your package manager of choice
---
2. Download Determinate Nix
   ```shell
   curl --proto '=https' --tlsv1.2 -ssf --progress-bar -L https://install.determinate.systems/nix -o install-nix.sh
   ```
---
3. Install Determinate Nix
   ```shell
   sh install-nix.sh install --determinate --no-confirm --verbose
   ```
---
4. Install direnv using nix
   ```shell
   nix profile install nixpkgs#direnv
   ```
   If you encounter a permission error, try running with sudo
   ```shell
   sudo nix profile install nixpkgs#direnv
   ```
---
5. Find out what shell you are using and hook direnv into your shell according to [this guide](https://github.com/direnv/direnv/blob/master/docs/hook.md)
   ```shell
   echo $SHELL
   ```
---
6. Allow direnv to access the repository
   ```shell
   direnv allow
   ```

If the six troubleshooting steps above still did not work for you, try the following as a **last resort**: Open a new terminal and navigate to the client repository with ```cd```. Run the command. Close the terminal again and do this for each of the six commands above, running each one in its own terminal, one after the other.
   
---

### Running the app after successful installation
```bash
npm run dev
# or
yarn dev
# or
deno task dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the
result.

You can start editing the page by modifying `app/page.tsx`. The page
auto-updates as you edit the file.

This project uses
[`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts)
to automatically optimize and load [Geist](https://vercel.com/font), a new font
family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js
  features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out
[the Next.js GitHub repository](https://github.com/vercel/next.js) - your
feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the
[Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme)
from the creators of Next.js.

Check out our
[Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying)
for more details.

---

Now that Ubuntu / WSL2 is installed, you will need to copy the whole repository folder over to the WSL2 filesystem (otherwise, the disk IO performance will be horrible).\
You can do this either by using the Windows explorer or in the command line in WSL2.

1. Windows explorer: In the left overview of all folders and drives there should be a new filesystem called Linux (also check in the network tab).\
Open the Linux drive and open the folder named "home", followed by your username.\
Copy the whole repository folder from your current location to the Linux folder /home/your-username (note that the folder will initially be empty).\
Finally, delete the folder from your current location such that you only have the folder inside the Linux filesystem.

2. Using the terminal: Open a new Ubuntu / WSL2 terminal window.\
This will automatically open your home folder of the Linux file system.\
You then need to locate where the repository / folder that you have downloaded resides.\
You can use the ```cp -ar``` command to copy the folder from the Windows drive to the Linux filesystem.\
The command takes the following arguments: cp **source_file** _target_file_\
Thus we need to specify **source_file** the folder we want to copy from Windows filesystem and the _target_file_ where to copy the folder to in the Linux filesystem.\
As visible in [this screenshot](./copyFolderToUbuntu.png), the repository folder resides under the C drive in /mnt/c/\
If your file is not on your C drive, the folder path will be something like /mnt/d/\
In the screenshot, the downloaded repository folder is in the Downloads folder of the current user on the C drive, thus the path for **source_file** is ```/mnt/c/Users/immol/Downloads```\
The terminal in [the screenshot](./copyFolderToUbuntu.png) is currently in the home directory, indicated by ~ in the path in blue.\
As we want to copy the folder to the home folder (/home/your-username) we can specify the current directory (.) as the _target_file_, thus the dot at the end of the command.\
If you happen to not be in the home folder, you can also run the command with explicitly copying to the home folder as such:
```bash
cp -ar /mnt/c/your-path /home/your-username
```
Else you can run
```bash
cp -ar /mnt/c/your-path .
```
with . indicating to copy to the current path (in this case your home folder).\
You can check if the repository was successfully copied over using ```ls``` to list folders and files, as visible in [the screenshot](./copyFolderToUbuntu.png).\
You can then delete the downloaded folder / repository from the Windows filesystem in the explorer.



