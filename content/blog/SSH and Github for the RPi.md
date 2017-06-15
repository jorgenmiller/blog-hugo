+++
date = "2017-06-14"
title = "SSh and Github for the RPi"

+++

It is annoying to have to plug in a monitor, keyboard, and mouse to the Raspberry Pi. It is also annoying to not be able to access the files or the RPi from elsewhere. SSH and GitHub can help here.

SSH allows a Pi to be used remotely. To SSH, first you need the IP address. you can `hostname -I` on your Pi to get the IP address. Although it may show a long string of numbers, the IP address should be four numbers separated by periods. For example, `173.2.20.192` could be an IP address. Once you have the IP address, use the command `ssh <username>@<IP adress>` to connect. The default username is pi. `ssh pi@173.2.20.192` could connect to a pi. The first time you connect, it will give you a prompt. Type `yes` to continue. Then it will ask for you password on the pi. The default password is raspberry. If you want a graphical application like Idle or Scratch, use `ssh -Y <username>@<IP address>`. When you are finished, type `exit` to quit the SSH session.

Github will allow the Pi to push its files to the cloud and allow other devices to later access them. `sudo apt install git` to get git, so you can use GitHub. On your pi (or while using SSH) you need to identify who you are.
~~~~unix
git config --global user.name "<Your name>"
git config --global user.email "<Your email>"
~~~~
Then, make sure you are inside the directory you want on GitHub. Use `git init` to make it a git repository. `ls -a` to check that there is a `.git` folder in your directory. To add your files to the repository, `git add -A` to add all the files. Then use `git commit -m"<commit message>"` to commit the files. Now, make or login to Your GitHub account. make a new repository and give your it a name. Now your repository exists. It will bring you to a setup screen. It will give you commands to use under the 'push an existing repository' section. They will look like this.
~~~~unix
git remote add origin (...)
git push -u origin master
~~~~
Now if you look on Github, the files in your folder should now be online. You can now use these commands to add your files to GitHub.
~~~~unix
git add -A
git commit -m"<commit message>"
git push
~~~~

Now you can remotely use a Raspberry Pi with SSH and access a folder of your pi from GitHub.
