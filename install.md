# How to install/setup VirtualBox Web Console #

## Prepare the environment ##

Please note that you have to respect the installation order to get VirtualBox Web Console working! For example you first have to install Python before installing extensions - otherwise the extensions installers won't find Python on your system.

If you don't have Python installed, download and install **Python 2.6** from http://python.org/download/.

### Windows ###

  * Download and install the **Python Win32 Extensions** package from http://python.net/crew/mhammond/win32/Downloads.html. You need the corresponding packet for your installed Python version, e.g. "pywin32-214.win32-py2.5.exe" when you got Python 2.5 or "pywin32-214.win32-py2.6.exe" for 2.6. Be sure to grab the .exe installers and not the .zip file to avoid installation errors because of missing dependencies. Note that the PyWin page currently does not work correctly on 64-bit host systems so the VirtualBox Web Console will not work on 64-bit Windows hosts at this point. We are working with the PyWin maintainer so resolve this issue.

### Mac OS X ###

  * Unless you are running Mac OS 10.6 (Snow Leopard), you have to download the Python module **SimpleJSON** from http://pypi.python.org/pypi/simplejson/, change to the extraction directory and install it with

```
python setup.py install```

### Linux ###

If your Linux distribution does not ship Python 2.6 (check with `python --version`), you have to install **SimpleJSON** from your package repository. For Debian/Ubuntu systems, enter

```
sudo apt-get install python-simplejson```

### All platforms ###

Last but not least download and install at least **VirtualBox 3.0.6** from http://www.virtualbox.org/ and make sure you selected the option "VirtualBox Python Support" on the installer's feature page

To execute Python scripts everywhere on your system (and you need to for getting VBox Web Console to work later) you need to add you Python installation directory to your PATH environment variable.

**Warning:** If you already installed an older version (or beta) of VirtualBox on your machine, please re-install it using the latest version at http://www.virtualbox.org/ because of the missing VirtualBox Python bindings.

If, for whatever reasons, you want to reinstall the VirtualBox Python bindings manually, you have to open a command line in the VirtualBox installation directory (e.g. "C:\Program Files\Oracle\VirtualBox\") and go to the "sdk\install" sub directory. There you have to execute

```
python vboxapisetup.py install```

to install the bindings (again). Note that on Windows Vista and later, you have to execute this command from an administrator prompt.

## Get VBox Web Console ##

### Check out the code ###

Install SubVersion (SVN) from http://subversion.tigris.org/ and check out the latest sources from

```
svn checkout http://vboxweb.googlecode.com/svn/trunk/ vboxweb-read-only```

The above command gets all the sources of VirtualBox Web Console into a directory called "vboxweb-read-only".

**Note:** The so called "trunk" build (see URL above) always represents the latest version of VirtualBox Web Console which is compatible with the **latest** VirtualBox version (side note for techies: using the same API). To use an older version (starting at 3.0) of VirtualBox with VirtualBox Web Console you have to check out the appropriate branch.

For VirtualBox 3.1.x:
```
svn checkout http://vboxweb.googlecode.com/svn/trunk/ vboxweb-read-only```

For VirtualBox 3.0.x:
```
svn checkout http://vboxweb.googlecode.com/svn/branches/VBox-3.0 vboxweb-read-only```

From now on we're using the placeholder "root" for this directory. Please note that you cannot put back (commit) changes to the sources unless you have write access to the repository.

## Running VBox Web Console ##

Now that you installed and set up all the required components, let's try out starting up
VBox Web Console the first time! To do so, first start the server part of VBox Web Console by entering

```
python VBoxWebSrv.py```

in your command line (you have to be in your "root" directory -- see paragraph above). If nothing went wrong the server now is running.

Now open your browser (currently only IE 7+8 and Firefox are tested) and type in the URL

```
localhost:8080```

to see VBox Web Console in action. Depending on whether you already have some virtual machines configured yet you should see them in the VM list on the left side.

If you're done using/testing VBoxWeb console, press CTRL+C in your console window to quit the server part and close the web browser.

## Troubleshooting ##

**Question:** The VBox Python binding does not seem to work! What's wrong?

**Answer:** If you installed Python in the directory "C:\Python26", check out if the directory "C:\Python26\Lib\site-packages\vboxapi" exists. If this doesn't exist, re-install VirtualBox with "VirtualBox Python Support" selected.


---


**Question:** VBox Web Console wants to run on port 8080, but this port is already taken of "insert-your-favorite-app-here". What to do now?

**Answer:** Go to your "root" directory of VBoxWeb and edit the file called "VBoxWeb.conf". Go to the line "server.socket\_port = 8080" and just change the "8080" to a port you want to set VBoxWeb running on. Then restart the VBoxWeb server application.