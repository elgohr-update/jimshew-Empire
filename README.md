![Empire](https://user-images.githubusercontent.com/20302208/70022749-1ad2b080-154a-11ea-9d8c-1b42632fd9f9.jpg)

[1.1]: http://i.imgur.com/tXSoThF.png (twitter icon with padding)
[2.1]: http://i.imgur.com/P3YfQoD.png (facebook icon with padding)
[3.1]: http://i.imgur.com/yCsTjba.png (google plus icon with padding)
[4.1]: http://i.imgur.com/YckIOms.png (tumblr icon with padding)
[5.1]: http://i.imgur.com/1AGmwO3.png (dribbble icon with padding)
[6.1]: http://i.imgur.com/0o48UoR.png (github icon with padding)

[1]: https://twitter.com/bcsecurity1
[2]: http://www.facebook.com/XXXXXXX
[3]: https://plus.google.com/XXXXXXX
[4]: http://XXXXXXX.tumblr.com
[5]: http://dribbble.com/XXXXXXX
[6]: http://www.github.com/BC-SECURITY
[7]: https://www.bc-security.org/blog

![GitHub contributors](https://img.shields.io/github/contributors/BC-SECURITY/Empire)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/BC-SECURITY/Empire)
![GitHub stars](https://img.shields.io/github/stars/BC-SECURITY/Empire)
![GitHub](https://img.shields.io/github/license/BC-Security/Empire)
[![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/fold_left.svg?style=flat)](https://twitter.com/BCSecurity1)

Keep up-to-date on our blog at [https://www.bc-security.org/blog][7]

# Empire
Empire 3.0 is a post-exploitation framework that includes a pure-PowerShell 2.0 Windows agent, and compatibility with Python 2.x/3.x Linux/OS X agents. It is the merger of the previous PowerShell Empire and Python EmPyre projects. The framework offers cryptologically-secure communications and a flexible architecture. On the PowerShell side, Empire implements the ability to run PowerShell agents without needing powershell.exe, rapidly deployable post-exploitation modules ranging from key loggers to Mimikatz, and adaptable communications to evade network detection, all wrapped up in a usability-focused framework. PowerShell Empire premiered at [BSidesLV in 2015](https://www.youtube.com/watch?v=Pq9t59w0mUI) and Python EmPyre premeiered at HackMiami 2016. BC-Security presented updates to further evade Microsoft Antimalware Scan Interface (AMSI) and JA3/S signatures at [DEF CON 27](https://github.com/BC-SECURITY/DEFCON27).

Empire relies heavily on the work from several other projects for its underlying functionality. We have tried to call out a few of those people we've interacted with [heavily here](http://www.powershellempire.com/?page_id=2) and have included author/reference link information in the source of each Empire module as appropriate. If we have failed to properly cite existing or prior work, please let us know at Empire@BC-Security.org.

Empire is developed by [@harmj0y](https://twitter.com/harmj0y), [@sixdub](https://twitter.com/sixdub), [@enigma0x3](https://twitter.com/enigma0x3), [@rvrsh3ll](https://twitter.com/424f424f), [@killswitch_gui](https://twitter.com/killswitch_gui), [@xorrior](https://twitter.com/xorrior), and [@bcsecurity1](https://twitter.com/BCSecurity1). While the main fork for Empire is no longer maintained, this fork is maintained by [BC-Security](https://www.bc-security.org) and will continue to receive periodic updates.

## Release Notes
There are some major upgrades in Empire 3.0. Many of these have lingered on various branches of the Empire project and have finally been consolidated, as well as, there being several new updates. The biggest change to mention is the conversion of the Empire base code from Python 2.7 to Python 2.7/3.x compatible. This will ensure that Empire continues to function as Kali drops Python 2.7 support. The conversion also causes some issues in the way that bytes and strings are handled which will likely cause some unfound errors. 

We have tested the core http listeners (http, http_hop, http_mapi, redirector) and confirmed that they work in both Python 2.7 and 3.x. We have also tested the Mimikatz modules and several of the launchers.

In addition to the code conversion, there are some minor UI updates, a few new modules, and new functionality. The full list of changes can be reviewed in the changelog.

## Install

To install and run:

```sh
git clone https://github.com/BC-SECURITY/Empire.git
cd Empire
sudo ./setup/install.sh
```

There's also a [quickstart here](http://www.powershellempire.com/?page_id=110) and full [documentation here](http://www.powershellempire.com/?page_id=83).

## Docker
If you want to run Empire using a pre-built docker container:
```bash
docker pull bcsecurity/empire:{version}
docker run -it bcsecurity/empire:{version}

# with persistent storage
docker pull bcsecurity/empire:{version}
docker create -v /empire --name data bcsecurity/empire:{version}
docker run -it --volumes-from data bcsecurity/empire:{version}

# if you prefer to be dropped into bash instead of directly into empire
# docker run -it --volumes-from data bcsecurity/empire:{version} /bin/bash
```

All image versions can be found at: https://hub.docker.com/r/bcsecurity/empire/
* The last commit from master will be deployed to the `latest` tag
* The last commit from the dev branch will be deployed to the `dev` tag
* All github tagged releases will be deployed using their version numbers (v3.0.0, v3.1.0, etc)

## Quickstart

Check out the [Empire wiki](https://github.com/EmpireProject/Empire/wiki/Quickstart) for instructions on getting started with Empire.

## To Do List

* ~~Port code to work with Python 3~~
* [Invoke-SocksProxy](https://github.com/p3nt4/Invoke-SocksProxy)
* Function name randomization
* ~~JA3/S signature randomization~~
* ~~Multi-menu function calls~~
* Function name aliasing
* ~~Update to [Mimikatz 2.2.0](https://github.com/gentilkiwi/mimikatz)~~

## Contribution Rules

Contributions are more than welcome! The more people who contribute to the project the better Empire will be for everyone. Below are a few guidelines for submitting contributions.

* Beginning with version 3.0, we will require that all updates be both Python 2.x/3.x compatible.
* Submit pull requests to the [dev branch](https://github.com/BC-SECURITY/Empire/tree/dev). After testing, changes will be merged to master.
* Depending on what you're working on, base your module on [./lib/modules/powershell_template.py](lib/modules/powershell_template.py) or [./lib/modules/python_template.py](lib/modules/python_template.py). **Note** that for some modules you may need to massage the output to get it into a nicely displayable text format [with Out-String](https://github.com/PowerShellEmpire/Empire/blob/0cbdb165a29e4a65ad8dddf03f6f0e36c33a7350/lib/modules/situational_awareness/network/powerview/get_user.py#L111).
* Cite previous work in the **'Comments'** module section.
* If your script.ps1 logic is large, may be reused by multiple modules, or is updated often, consider implementing the logic in the appropriate **data/module_source/*** directory and [pulling the script contents into the module on tasking](https://github.com/PowerShellEmpire/Empire/blob/0cbdb165a29e4a65ad8dddf03f6f0e36c33a7350/lib/modules/situational_awareness/network/powerview/get_user.py#L85-L95).
* Use [approved PowerShell verbs](https://technet.microsoft.com/en-us/library/ms714428(v=vs.85).aspx) for any functions.
* PowerShell Version 2 compatibility is **STRONGLY** preferred.
* TEST YOUR MODULE! Be sure to run it from an Empire agent and test both Python 2.x/3.x functionality before submitting a pull to ensure everything is working correctly.
* For additional guidelines for your PowerShell code itself, check out the [PowerSploit style guide](https://github.com/PowerShellMafia/PowerSploit/blob/master/README.md).
