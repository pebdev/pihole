# Pi-Hole - ads-catcher #
	
### What is it ? ###

This tool scans pi-hole logfiles to find youtube address of ads servers. It updates pi-hole blacklist automatically after a scan.


### How it works ? ###

**Ads-catcher** is called every 10 minutes to check pi-hole logfiles.
It does following actions :

- scan pihole logfiles
- extract addresses of ads servers
- filter result (to remove duplicated addresses, whitlist addresses, etc.)
- add blacklisted addresses to pihole list
- launch pi-hole update to take account of new adresses

**Ads-catcher-unlocker** (included in the package) is a tool that monitors server requests (throught pihole logs) to detect if your main video is blocked by an extreme filtering. If your are in this case, it will unlock main video.

<span style="color:red">Note 1 : this system needs time to remove ads but it has advantage to do the job alone, be patient.</span>

<span style="color:red">Note 2 : some time, your main video can be blocked. Ads-catcher includes a mechanism to detect and fix this situation, you just need to close and launch again your video.</span>


### Installation ###

Debian package is provided, you just need to download it ([release page](https://github.com/pebdev/pihole/releases)), and to launch dpkg :

	sudo dpkg -i <deb_file>

Content of the package :

	 /
	 ├── /etc/ads-catcher.cfg
	 ├── /usr/bin/ads-catcher
	 ├── /usr/bin/ads-catcher-blacklister
	 ├── /usr/bin/ads-catcher-unlocker
	 ├── /lib/systemd/system/ads-catcher.service
	 ├── /usr/share/doc/ads-catcher/copyright
	 ├── /usr/share/man/man1/ads-catcher.1.gz
	 ├── /usr/share/man/man1/ads-catcher-blacklister.1.gz
	 ├── /usr/share/man/man1/ads-catcher-unlocker.1.gz
	 
Note : you can see content with this command **dpkg -c < deb_file >**

During installation, ads-catcher parses all pihole logfiles to create a first database of youtube addresses to blacklist.


### Uninstall ###

To uninstall this package, just lanch this command :

	sudo dpkg -r ads-catcher


### Logfile ###

If you want to check actions of scripts, you can access to the logfile :

	cat /var/log/ads-catcher-blacklister.log


### Known issues ###

- no issue

### Todo ###

- nothing for the moment


### Link ###

Discussion on pi-hole forum : [link](https://discourse.pi-hole.net/t/how-do-i-block-ads-on-youtube/253/327)


## Changelog ##
**v1.3.0** *[md5:b6cb3e7d72ab4fe409ee57aea25ac5ee]*   
- [ADDED] ads-catcher-unlocker to detect blacklisted address of the main video   
- [ADDED] use -a option to parse all log files during installation   
- [ADDED] configuration file is back   
- [ADDED] now ads-catcher manages scripts execution   
- [CHANGED] ads-catcher renamed : ads-catcher-blacklister   
- [CHANGED] use systemd instead of crontab   

**v1.2.0** *[md5:82c64f9548f5215ebde262f62667f9cc]*   
- [ADDED] Option to parse all logfiles (useful for the initilization)    
- [CHANGED] Check new addresses only, not all addresses from the pihole logfile    
- [CHANGED] Now just refresh blacklist entries, not all gravity lists   
- [CHANGED] Internal refactoring   
- [UPDATED] Manual   
- [REMOVED] Separated logfiles feature   
- [REMOVED] History feature   
- [REMOVED] Configuration file (separated and blacklist options)   

**v1.1.1** *[md5:2f4f19d98ca644f405689ce9c79b322a]*   
- [FIXED] whitelist filtering issue that caused not working blacklist   
- [ADDED] google manifest in the whitelist

**v1.1.0** *[md5:8ce40ab7ec66ff37406317cf2676d9eb]*   
- [ADDED] option to write (1) ads-catcher blacklist files or (2) blocked addresses into the pi-hole balcklist (default: (2))  
- [ADDED] option to enable/disable backup files (default : disabled)   
- [ADDED] configuration file  
- [ADDED] deb package for easy install

**v1.0.0**   
- initial revision