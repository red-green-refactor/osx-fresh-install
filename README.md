#Rails Developer guide to reinstalling OSX

Below you will find a series of instructions on how to reinstall your mac OS and set up RVM (a ruby version manager).  I have also included helpful links to commonly used programs in the development community.

Before you begin make sure to backup any personal settings that you would like to keep.  For example, custom bash scripts, aliases, profile settings, terminal color profiles, browser bookmarklets, bookmarks, git aliases (configs), etc, etc.

##Reinstalling the OS.

**note:**  You must have a wireless internet connection available to reinstall your OS.

Restart the computer, once you hear the mac startup sound hold down [cmd + r], this will launch the mac recovery system.

Now choose "Terminal" from the Utilities menu, and run the following command

```
diskutil cs list
```

With this command entered, you will see a hierarchal tree of the encrypted volume, the first entry is the core storage group. Get the UUID from this group and use the following command to erase the hard drive:

```
diskutil cs delete UUID
```

After the disk is erased, close terminal.

Select Reinstall OS X, click continue and follow the instructions.

##Reinstall your applications
After the OS is installed you can start installing all your applications.

**Note:** if you haven't upgraded to Mavericks yet I suggest doing so now before installing any applications. Also, if you plan on using file vault I would start that up after mavericks is installed. 

Here is a list of commonly used applications for references (along with links)

Chrome:
https://www.google.com/intl/en/chrome/browser/

Skype:
http://www.skype.com/en/download-skype/skype-for-computer/

iAntivirus:
https://itunes.apple.com/us/app/iantivirus/id523947195

iTerm2:
http://www.iterm2.com/#/section/home

Sublime Text 3:
http://www.sublimetext.com/3

Screenhero:
http://screenhero.com/

Teamviewer:
http://www.teamviewer.com/en/download/mac.aspx

Licecap:
http://www.cockos.com/licecap/

Caffeine:
https://itunes.apple.com/us/app/caffeine/id411246225

Dropbox:
https://www.dropbox.com/downloading

Balsamiq:
http://balsamiq.com/download/

LiveReload:
https://itunes.apple.com/us/app/livereload/id482898991
https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei (chrome plugin)

VMware Fusion:
http://www.vmware.com/products/fusion

**Note:** this would also be the time to install your other applications like photoshop, illustrator or any other applications.

##Install Xcode and command line tools.

Install xcode: http://itunes.apple.com/us/app/xcode/id497799835

Install Xcode developer tools.  Open terminal and type the following command:

```
xcode-select --install
```

A pop-up will appear asking you to install the command line developer tools, choose ‘Install’

After installing Xcode you have to agree to the Xcode license.  You can do that by running the following command:

```
sudo xcodebuild -license
```

##Install Homebrew and dependancies

To install homebrew open the terminal and type the following command:

```
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
```

As listed in the output you should run the following command before installing anything via homebrew and follow the onscreen instructions:

```
brew doctor
```

Install older apple GCC toolchain

```
brew install apple-gcc42
```

Install other dependancies via Homebrew.

Below are common dependancies used but these are not required dependancies. Install what is needed for your particular application. 

```
brew install imagemagick
brew install phantomjs
brew install ghostscript
brew install qt
```

##Install mysql (5.5)

I am installing mysql 5.5 instead of 5.6 as 5.6 causes all types of issues in my rails build. To install 5.5 open terminal and run the following command:

```
brew tap homebrew/versions
brew install mysql55
```

After installing mysql you will see instructions in terminal on how to start mysql as well as how to have mysql auto start when the computer starts up.

To have mysql start at login type the following command into terminal:
```
ln -sfv /usr/local/opt/mysql55/*.plist ~/Library/LaunchAgents
```

Then to load mysql55 now type:

```
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql55.plist
```

Type the following command into terminal to add mysql to your path:

```
echo 'export PATH=/usr/local/opt/mysql55/bin:$PATH' >> ~/.bash_profile
```

##Installing ruby

**Install a ruby version manager**
I prefer RVM so my instructions will be for that.  But RVM isn’t the only option available.  These days the cools kids are using rbenv which is a bit more light weight and easier to setup. You might want to checkout rbenv first and decide which is right for you. (https://github.com/sstephenson/rbenv)

To install RVM with the latest stable version of ruby, open the terminal and run the command below:

```
curl -sSL https://get.rvm.io | bash -s stable --ruby
```

After RVM is install you can check that it is working by typing ‘rvm’ into the terminal.

**Note:** you will have to either open a new terminal or type ‘source ~/.rvm/scripts/rvm’ to load rvm after installation.  I prefer just opening an new terminal window but the choice is yours. 

To install a different version of ruby simply type ‘rvm install (your ruby version)’.  In the example below I will be installing 1.9.3 as I need it for the project I am setting up.

Open the terminal and type the command below to install 1.9.3:

```
rvm install 1.9.3
```

##Install bundler

Open terminal and type the following command to install bundler:

```
gem install bundler
```

##Install rails

You can install rails with the following command ‘gem install rails --version “=your version number”’.

In the example below I am installing rails 3 as it is what I need for the project I am setting up. Open terminal and type the following command to install rails:

```
gem install rails --version “=3.2.17”
```

After installation type the following command to check your rails version:

```
rails -v
```

If terminal outputs ‘Rails 3.2.17’ you are all setup.

##Party time

Now it’s time to pat yourself on the back as you have successfully:

1. Reinstalled your OS (and Mavericks)
2. Installed a whole bunch of applications
3. Installed xCode and developer tools
4. Installed Homebrew and dependancies
5. Installed a ruby version manager (RVM)
6. Installed ruby 
7. Installed Rails

##Optional Mac modifications

These are things that I just like and thought that you may like them as well.

**Add recent files stack to dockbar:**
```
defaults write com.apple.dock persistent-others -array-add '{ "tile-data" = { "list-type" = 1; }; "tile-type" = "recents-tile"; }'; Killall Dock
```

**Show hidden files in finder:**
```
defaults write com.apple.finder AppleShowAllFiles true; Killall Finder
```
