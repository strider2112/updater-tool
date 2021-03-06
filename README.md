# updater-tool
A tool, for debian Linux distros (that have aptitude), for checking for updates and assist in updating. Written in BASH.

So far this tool contains two scripts, written entirely in BASH (I am working on porting it to something like C, or maybe a different scripting language like Python, but I just quickly tapped this together to assist in a problem I had). Currently, this tool is very limited, and can really only be used on ubuntu systems with certain dependancies.

The Problem: I have several Ubuntu-Based distributions that have their own MOTD when each user logs in. I need to be able to show available updates when someone logs in, so that they know if any packages need updating. apt-check (part of update-notifier) can provide this functionality, but it can slow down the login process depending on network speed - because apt-check has to connect to the canonical server to check for updates to aptitude packages. Sometimes, a user would open the terminal and the terminal would appear to hang for 2-3 seconds before the MOTD finally pops up. I had 1-2 hours to come up with something, quickly, that could work. I can now continue to work on it and make it better.

The Solution: Create a script that calls for apt-check periodically (such as once per day, as a Cron-job) and updates a file, somewhere on the system, that contains the pre-formatted "update" text - which can be added into the MOTD.

The Solution's Problem: This makes a problem where, if you see that you have updates and you update by running apt update/upgrade, the next time you log in the script may not have run and the system will still tell you that you have updates.

The Solution's Problem's Solution: So I created two scripts. The update-checker, and a custom update-helper - all the update-helper does is assist in the process of going through aptitude to update the out of date packages. However, to assist in user-usability, it makes calls back to the update-checker so that there are no gaps left in the system.

Dependancies:
  1. BASH - since it's a bash script, currently, it requires bash. 
  2. Python - Python is required for the apt-check script. (sudo apt install python)
  3. update-notifier - update-notifier is required because it contains the apt-check script. (sudo apt install update-notifier)
  
Installation (Root Required):
  1. Clone this repository, run the command: git clone https://github.com/strider2112/updater-tool
  2. run the command: cd updater-tool && chmod +x install
  3. run the command: sudo ./install
  4. the programs can be run by executing "check-for-updates" and "updater". Depending on your system, they may require root.
      check-for-updates saves the updates.txt formatted file in /usr/local/share/updater-tool/data by default, with r/w permissions
  
Installation (No Root):
  1. Clone this repository, run the command: git clone https://github.com/strider2112/updater-tool
  3. run the command: cd updater-tool
  3. run the command: ./install
  4. the programs can be run by executing "check-for-updates" and "updater".
      check-for-updates saves the updates.txt formatted file in ..updater-tool/data by default, with r/w permissions
      
Uninstall (with root):
  1. run the command: cd updater-tool && chmod +x .uninstall
  2. run the command: sudo ./.uninstall
  
Uninstall (no root):
  1. run the command: rm -r updater-tool

WIP:
- Work on the scripts to make them more distro-friendly
- Work on porting it to a more flexible language, such as python or C
