Mintty as a terminal for WSL (Windows Subsystem for Linux).

<img align=right src=wsltty.png>

### Overview ###

WSLtty components
* wsltty package components (see below) in the user’s local application folder 
  `%LOCALAPPDATA%`
* a wsltty configuration directory in the user’s application folder `%APPDATA%`
  (“home”-located configuration files from a previously installed version 
  will be migrated to the new default location)
* Start Menu shortcuts to start a WSL shell (with some variations, see below)
* `*.bat` scripts to invoke WSL from the command line (see below)
* optional context menu entries for Windows Explorer to start a WSL shell in the respective folder
* install/uninstall context menu items from Start Menu subfolder `WSLtty`
* an uninstall script that can be invoked manually to remove shortcuts and context menu entries

### Installation ###

#### WSLtty installer ####

Run the [installer](https://github.com/mintty/wsltty/releases) to install 
the components listed above.
If Windows complains with a “Windows protected your PC” popup, 
you may need to click “Run anyway” to proceed with the installation.
You may need to open the Properties of the installer first, tab “General” 
section “Security” (if available) and select “Unblock”, 
to enable the “Run anyway” button.

#### Installation from source repository ####

Download or checkout the wsltty repository.
Invoke `make`, then `make install`.
Note this has to be done within a Cygwin environment.

#### Installation to non-default locations ####

(For experts)
Within the installation process, provide parameters to the script `install.bat`.
The optional first parameter designates the installation target,
the optional second parameter designates the configuration directory.

### Invocation ###

WSLtty can be invoked with
* installed Start Menu shortcuts (or Desktop shortcuts if copied there)
* *.bat scripts
* Explorer context menu (if installed from the Start Menu `WSLtty` subfolder)

Starting the mintty terminal directly from the WSLtty installation location 
is discouraged because that would bypass some essential options.

### Configuration ###

#### Command line scripts `wsl*.bat` ####

WSLtty installs the following scripts into `%LOCALAPPDATA%\Microsoft\WindowsApps` 
(and a copy in its application folder `%LOCALAPPDATA%\wsltty`):

* For each installed WSL distribution D, D`.bat` to start in the current folder/directory
* For each installed WSL distribution D, D`~.bat` to start in the WSL user home
* `wsl.bat` to start the default WSL installation in the current folder/directory
* `wsl~.bat` to start the default WSL installation in the WSL user home
* `wsl-l.bat` to start the default WSL installation with a login shell

Given that `%LOCALAPPDATA%\Microsoft\WindowsApps` is in your PATH,
the scripts can be invoked from cmd.exe, PowerShell, or via WIN+R.

#### Start Menu and Desktop shortcuts ####

In the Start Menu, the following shortcuts are installed:
* For each installed WSL distribution D, D` in Mintty` to start in the WSL user home

In the Start Menu subfolder WSLtty, the following shortcuts are installed:
* For each installed WSL distribution D, D` in Mintty` to start in the Windows %USERPROFILE% home
* For each installed WSL distribution D, D` ~ in Mintty` to start in the WSL user home
* `WSL % in Mintty` to start the default WSL installation in the Windows %USERPROFILE% home
* `WSL ~ in Mintty` to start the default WSL installation in the WSL user home
* `WSL -l in Mintty` to start the default WSL installation with a login shell

WSLtty does not install Desktop shortcuts. If you want them, copy the 
desired ones from the Start Menu subfolder `WSLtty`.

To ensure a login shell to start in your Linux home directory, 
add a `cd` command to your `$HOME/.profile` on Linux side.

#### Context menu entries ####

WSLtty provides context menu entries for all installed WSL distributions,
to start a respective WSL shell in a specific folder from an Explorer window. 
They are not installed by default.
To add or remove context menu entries, run the respective script from the 
Start Menu subfolder `WSLtty`.

#### Mintty settings ####

Mintty can maintain its configuration file in various locations, 
with the following precedence:
* file given with mintty option `-c` (not used by wsltty default installation)
* file `config` in directory given with mintty option `--configdir`
  * This is `%APPDATA%\wsltty\config` in the default wsltty installation.
* `%HOME%\.minttyrc` (usage deprecated with wsltty)
* `%HOME%\.config\mintty\config` (usage deprecated with wsltty)
* `%APPDATA%\mintty\config`
* `%LOCALAPPDATA%\wsltty\etc\minttyrc` (usage deprecated with wsltty)

Note:
* `%APPDATA%\wsltty\config` is the new user configuration file location. 
  Further subdirectories of `%APPDATA%\wsltty` are used for language, 
  themes, and sounds resource configuration. 
  Note the distinction from `%LOCALAPPDATA%\wsltty` which is the default 
  wsltty software installation location.
* The `%APPDATA%\mintty\config` option provides the possibility to 
  maintain common mintty settings for various installations (like 
  wsltty, Cygwin, MinGW/msys, Git for Windows, MinEd for Windows).
* (About deprecated options) By default, `%HOME%` would refer to the 
  root directory of the cygwin standalone installation hosting wsltty. 
  So `%HOME%` would mean `%LOCALAPPDATA%\wsltty\home\%USERNAME%`.
  If you define `HOME` at Windows level, this changes accordingly.
  Note, however, that the WSL `HOME` is a completely different setting.

#### Shell selection ####

To invoke your favourite shell, replace `/bin/bash` with its pathname 
in the Desktop or Start Menu shortcuts and `*.bat` launch scripts, 
or Explorer context menu commands.

### Components ###

For mintty, see the [Mintty homepage](http://mintty.github.io/) 
(with further screenshots), 
the [Mintty manual page](http://mintty.github.io/mintty.1.html), 
<br>and the [Mintty Wiki](https://github.com/mintty/mintty/wiki), 
including a [Hints and Tips page](https://github.com/mintty/mintty/wiki/Tips).

It is based on [Cygwin](http://cygwin.com) 
and includes its runtime library ([sources](http://mirrors.dotsrc.org/cygwin/x86/release/cygwin)).

For interacting with WSL, it uses [wslbridge](https://github.com/rprichard/wslbridge).

