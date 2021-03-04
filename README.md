# Potato Open Sauce Project
## dumaloo-release
<img src="https://raw.githubusercontent.com/PotatoProject/manifest/dumaloo-release/XDAThread/main.png">

## Setting up your machine ##

You must be running a 64-bit Linux distribution and must have installed some packages to build
Paranoid Android. Google recommends using [Ubuntu](http://www.ubuntu.com/download/desktop) for
this and provides instructions for setting up the system (with Ubuntu-specific commands) on
[the Android Open Source Project website](https://source.android.com/source/initializing.html#setting-up-a-linux-build-environment).

## Grabbing the source ##

[Repo](http://source.android.com/source/developing.html) is a tool provided by Google that
simplifies using [Git](http://git-scm.com/book) in the context of the Android source.

### Installing Repo ###

```bash
# Make a directory where Repo will be stored and add it to the path
$ mkdir ~/.bin
$ PATH=~/.bin:$PATH

# Download Repo itself
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo

# Make Repo executable
$ chmod a+x ~/.bin/repo
```

### Initializing Repo ###

```bash
# Create a directory for the source files
# You can name this directory however you want, just remember to replace
# WORKSPACE with your directory for the rest of this guide.
# This can be located anywhere (as long as the fs is case-sensitive)
$ mkdir WORKSPACE/POSP
$ cd WORKSPACE/POSP

# Install Repo in the created directory
# Use a real name/email combination, if you intend to submit patches
$ repo init -u https://github.com/PotatoProject/manifest -b dumaloo-release
```
### Downloading the source tree ###

This is what you will run each time you want to pull in upstream changes. Keep in mind that on your
first run, it is expected to take a while as it will download all the required Android source files
and their change histories.

```bash
# Let Repo take care of all the hard work
#
$ repo sync 
```

#### Syncing specific projects ####

In case you are not interested in syncing all the projects, you can specify what projects you do
want to sync. This can help if, for example, you want to make a quick change and quickly push it
back for review. You should note that this can sometimes cause issues when building if there is
a large change that spans across multiple projects.

```bash
# Specify one or more projects by either name or path

# For example, enter PotatoProject/android_frameworks_base or
# frameworks/base to sync the frameworks/base repository

$ repo sync PROJECT
```
### Preparing your system to build ###

```bash
# Installing git:
$ sudo apt install git

Running configuration script:
$ cd ~/
$ git clone https://github.com/akhilnarang/scripts
$ cd scripts
$ ./setup/android_build_env.sh

```
### Building ###

```bash
$ cd WORKSPACE/POSP

# Set up environment
$ . build/envsetup.sh

# Choose a target
$ lunch potato_$device-userdebug

# Build the code
$ brunch $device
```

## Submitting Patches ##

We're open source and patches are always welcome!

You can see the status of all patches at [Gerrit Code Review](https://gerrit.aospa.co/).

### Following the standard workflow ###

```bash
# Start by going to the root of the source tree
$ cd WORKSPACE

# Create a new branch on the specific project you are going to work on
# For example, `repo start fix-clock AOSPA/android_frameworks_base`
$ repo start BRANCH AOSPA/PROJECT
# You can also use the project path in place of the project name.
# The PROJECT_DIR is the portion after the android_ prefix on
# the AOSPA Github.  For example, android_frameworks_base translates
# into the directory frameworks/base.
# This applies to all repo commands that reference projects.
$ repo start BRANCH PROJECT_DIR

# Go inside the project you are working on
$ cd PROJECT_DIR

# Make your changes
...

# Commit all your changes
$ git add -A
$ git commit -a -s

# Upload your changes
$ cd WORKSPACE
$ repo upload AOSPA/PROJECT
# or
$ repo upload PROJECT_DIR
```
### Using plain git to upload ###

```bash
# Go inside the project you are working on
$ cd PROJECT_DIR

# Make your changes
...

# Commit all your changes
$ git add -A
$ git commit -a -s

# Upload your changes
$ git push ssh://USERNAME@review.potatoproject.co:29418/PotatoProject/REPO_NAME HEAD:refs/for/dumaloo-release


Credits
-------
 * [**AOSP**](https://android.googlesource.com)
 * [**AOSiP**](https://github.com/AOSiP)
 * [**Dirty Unicorns**](https://github.com/DirtyUnicorns)
 * [**LineageOS**](https://github.com/LineageOS)
 * 
### Reporting compilation issues
- You can reach us at [**Telegram**](https://t.me/SaucyPotatoesOfficial)
- For common porting related errors, visit [**Android Building Help**](https://t.me/AndroidBuildersHelp)
- Make sure you provide relevant logs, screenshots and details with all sources you used.

### Contributing
- You can contribute to this project by submitting changes to our [**Gerrit Code-Review**](https://review.potatoproject.co) server.

### Adding Support
- For adding your device to the list of supported devices, please reach us at [**Telegram**](https://t.me/SaucyPotatoesOfficial) with your device tree and previous works.
