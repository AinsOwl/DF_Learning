MISP - Malware Information Sharing Platform (open-source threat information platform)

MISP is effectively useful for the following use cases:
1) Malware Reverse Engineering
2) Security Investigations
3) Intelligence Analysis
4) Law Enforcement: Using Indicators to support forensic investigations.
5) Risk Analysis
6) Fraud Analysis: Sharing of financial indicators to detect financial fraud.

MISP provides IoC Database, Automatic Correlation, Data sharing, Import & Export Features, Event Graph, API Support

----------------------------
MISP Dashboard – The analyst’s dashboard in MISP helps track, share, and correlate events & IOCs
----------------------------

Menu Options
	Home → Go to start screen / event index / custom home page.
	Event Actions → Create, edit, delete, publish, search, and list events & attributes.
	Dashboard → Build a custom dashboard using widgets.
	Galaxies → Quick access to MISP Galaxies list.
	Input Filters →
		Control how data is entered.
		Admins set regex replacements, blocklists, export restrictions.
		Users can view the rules.
	Global Actions → Info & settings:
		Profile, manual, news, terms.
		View organisations + histogram of contributions.
	MISP → Link back to base URL.
	Name → Current logged-in user (auto from email).
	Envelope → Notifications / proposals for your org.
	Logout → End session immediately.

Event Creation Distribution Options:
	Org only → just your org.
	Community → your org + same server + synced servers.
	Connected → community + servers two hops away.
	All → everyone, globally shared.
	
Attributes & Attachments
	Add attributes → Manually or import (OpenIOC, ThreatConnect, etc.).
	IDS flag → Mark attribute for use as IDS signature (else it’s just context).
	Batch import → Paste multiple values (e.g., IPs), each on a new line → system splits into separate attributes.

Which user has the role to publish events?  →  Organizations Admin


Feeds = threat intel sources (IOCs, events, adversaries).
Uses:
	Exchange threat info.
	Preview + import events/attributes.
	Correlate events with feed data.

Managed by: Site Admin (analysts use them)

Taxonomies (classification system using tags)
Uses:
	Categorise events/IOCs/actors.
	Enable external processing (e.g., VirusTotal).
	Ensure proper classification before publishing.
	Enrich IDS exports with relevant tags.

Machine tag structure:
	Namespace → property type.
	Predicate → property attached.
	Value → detail (number/text).

Found under Event Actions (enabled by Site Admin)


<_____ DFIR _____>

# Introduction

Tools
Eric Zimmerman’s Tools	:	Windows forensics tools (registry, file system, timeline, artifacts)
KAPE (Kroll Artifact Parser & Extractor) By Eric Zimmerman	:	Automates artifact collection + parsing and can generate timelines of events.
Autopsy	:	Analyzes disks, mobiles, USBs and uses plugins to speed up artifact extraction.
Volatility	:	Memory forensics tool (Windows + Linux). Extracts info from memory dumps.
Redline (by FireEye)	:	Incident response tool. Collects and analyzes forensic data from systems.
Velociraptor	:	Open-source endpoint monitoring + forensics + response. Enterprise-grade, very powerful.

SOP for IR acc. to NIST SP-800-61 Incident Handling Guide
1) Preparation
2) Detection and Analysis
3) Containmnet, Eradication, and Recovery
4) Post-Incident Activity

Incident Handler's Handbook by SANS defines the steps as: (PICERL)
1) Preparation
2) Identification
3) Containment
4) Eradication
5) Recovery
6) Lessons Learned

# Windows Forensics

Windows Registry : Collection of database containing system's configuration data.
5 Roots Keys:
	HKEY_CURRENT_USER [HKCU]
		Current logged-in user's settings. Profile info: Folders, colors, control panel, etc.
	HKEY_USERS [HKU]
		All loaded user profiles. Basically HKCU is a sub-key of HKU.
	HKEY_LOCAL_MACHINE [HKLM]
		Computer wide settings (apply to all users)
	HKEY_CLASSES_ROOT [HKCR]
		File associations: which program opens which file type
		Merged view of 
			HKLM\Software\Classes → defaults (all users).
			HKCU\Software\Classes → overrides (current user).
		Writing keys\values:
			Defaults → stored under HKLM\Software\Classes.
			If user-specific exists → stored under HKCU\Software\Classes.
	HKEY_CURRENT_CONFIG [HKCC]
		Current hardware profile used at system startup.
	
Accessing registry of a disk image which are located at "C:\Windows\System32\Config" directory.
1) DEFAULT (mounted on HKEY_USERS\DEFAULT)
2) SAM (mounted on HKEY_LOCAL_MACHINE\SAM)
3) SECURITY (mounted on HKEY_LOCAL_MACHINE\Security)
4) SOFTWARE (mounted on HKEY_LOCAL_MAHINE\Software)
5) SYSTEM (mounted on HKEY_LOCAL_MACHINE\System)

Apart from above the other 2 hives containing user information can be found in User profile directory.
For Windows 7 or above, User Profile is located at C:\Users\<username>\
1) NTUSER.DAT (mounted on HKEY_CURRENT_USER when a user logs in)
2) USRCLASS.DAT (mounted on HKEY_CURRENT_USER\Software\Classes) -> Located at %localappdata%\Microsoft\Windows

The Amcache Hive [Located at C:\Windows\AppCompat\Programs\Amcache.hve]
Contains info on programs that were recently run on the system.

Transaction Logs [Located at C:\Windows\System32\Config]:
	Act like a changelog/hournal for registry hives.
	Stores recent changes that may not yet be written into the hive itself.
	With the same name but .LOG, .LOG2, .LOG2, etc.
	Example: SAM.LOG for SAM
	Important to check in forensics since they may reveal modifications not visible in the main hive.
	
Backups [Located at C:\Windows\System32\Config\RegBack]
	Opposite of logs → contain older copies of registry hives.
	Updated roughly every 10 days.
	Useful if keys were deleted or modified recently and need recovery.
	

KAPE : 
	Live data cquisition and analysis tool which can be used to acquire registry data. Primarily a CLI. 


## In Registry for System Information and System Accounts:

OS Version	:	SOFTWARE\Microsoft\Windows NT\CurrentVersion

Control Sets (System Startup Info)	:
	📍 SYSTEM\ControlSet001 / SYSTEM\ControlSet002 → Boot & Last Known Good configs.
	📍 HKLM\SYSTEM\CurrentControlSet → Active control set when system is live.
	📍 SYSTEM\Select\Current → Which control set is active.
	📍 SYSTEM\Select\LastKnownGood → Last known good config.

Computer Name	:	SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName

Time Zone	:	SYSTEM\CurrentControlSet\Control\TimeZoneInformation

Network Info	:	
	Active Interfaces:
	📍 SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces
	➡️ Shows IPs, DHCP, DNS, Subnet Mask.

	Past Networks:
	📍 SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Unmanaged
	📍 SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed
	➡️ Shows SSIDs, last connected time.

Autoruns (Persistence)
	📍 NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run
	📍 NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce
	📍 SOFTWARE\Microsoft\Windows\CurrentVersion\Run
	📍 SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
	📍 SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
	➡️ Startup programs (malware persistence often hides here).

	Services Startup:
	📍 SYSTEM\CurrentControlSet\Services
		Start = 0x02 → Auto start at boot.
		
SAM (User & Account Info)
	📍 SAM\Domains\Account\Users
	➡️ User RIDs, login count, last login, last failed login, password policy, group membership.
	

## Recent Files
Windows RecentDocs: NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
	Useful for last opened files & file-type-specific investigations.
	MRU list (Most Recently Used) puts the latest file on top.
	Subkeys by extension (e.g., .pdf, .jpg) show last used files of that type
	
Office Recent Files: NTUSER.DAT\Software\Microsoft\Office\VERSION
(Office 365 + Live ID tied)	NTUSER.DAT\Software\Microsoft\Office\VERSION\UserMRU\LiveID_####\FileMRU
	Stores MRU lists for Office apps (Word, Excel, PowerPoint).
	Unlike RecentDocs, stores full file paths.
	
🗂 ShellBags (Folder Views & Accessed Folders)
Keys:
	USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags
	USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU
	NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU
	NTUSER.DAT\Software\Microsoft\Windows\Shell\Bags
Details:
	Tracks folder view/layout preferences.
	Reveals folders browsed by user.
	Best parsed with ShellBag Explorer.
	
💾 Open/Save & LastVisited Dialog MRUs
Keys:
	NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDlMRU
	NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU
Details:
	Tracks paths where files were last opened/saved.
	Helps reconstruct user’s file access behavior.
	
Windows Explorer Address & Search Bars
Keys:
	NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths (Tracks manual inputs in Explorer address bar)
	NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery (Stores keywords searched in Explorer)

Together, these registry locations give a timeline of user activity:
	RecentDocs → what files were opened.
	Office MRUs → what docs were worked on.
	ShellBags → what folders were accessed.
	Open/Save MRUs → where files were picked/saved.
	TypedPaths/WordWheel → what locations/keywords were searched.

## Evidence of Execution

UserAssist : Tracks applications executed through Windows Explorer (not command-line)
	NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count
Data Stored:
	Program names (ROT13 encoded).
	Execution count.
	Last execution time (FILETIME).
Limitations: Doesn’t log programs executed via CLI.

Use Eric Zimmerman’s UserAssist.exe parser for clean results

ShimCache \ Application Compatibility Cache (AppCompatCache) : Tracks executables for application compatibility / backward compatibility.
	SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache
Data Stored:
	Executable filename.
	File size.
	Last modified time (from filesystem).
Limitations: It records presence of execution attempt, not proof that it ran successfully.

Use AppCompatCacheParser.exe (Eric Zimmerman tool) to parse → CSV output.

Command example: AppCompatCacheParser.exe --csv <output_path> -f <SYSTEM_hive> -c <control_set>

AmCache	:	Extended tracking of executed programs (more detailed than ShimCache).
	C:\Windows\AppCompat\Programs\Amcache.hve
Data Stored:
	Full execution path.
	SHA1 hash of executables.
	Installation, execution, and deletion times.
	Volume GUID association.
Registry Path Inside Hive:	Amcache.hve\Root\File\{Volume GUID}\

Stronger forensic value since it contains cryptographic hashes and timestamps.

BAM/DAM (Background Activity Monitor / Desktop Activity Moderator): Tracks last execution time and paths of applications, focusing on background processes and power optimization.
	SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}
	SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}
Data Stored: Program path, Last execution time and Linked to specific user SID.
✅ Important for timeline analysis (especially in post-breach persistence checks)

CTF Tip:
If you need “what ran and when”, prioritize:
AmCache → for SHA1 + execution timestamps.
BAM/DAM → for last run programs per user.
UserAssist → for Explorer-launched apps.
ShimCache → for file presence & modified times.

## External Devices/USB device forensics

Device identification: Identify unique USB devices that were connected
	SYSTEM\CurrentControlSet\Enum\USBSTOR
	SYSTEM\CurrentControlSet\Enum\USB
What you get: Vendor ID, Product ID, Version, and sometimes Serial Number.

First/Last Times
	SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####
Values:
	0064 → First connection time
	0066 → Last connection time
	0067 → Last removal time

USB device Volume Name: name of the connected drive
	SOFTWARE\Microsoft\Windows Portable Devices\Devices
What you get: Friendly name/label of the USB device.
Correlation: Match the GUID here with the Disk ID under USBSTOR to link volume names to specific devices.

## FAT FILE SYSTEM 
Clusters → Smallest allocation unit, stores file data.
Directory → Stores metadata (filename, starting cluster, length).
File Allocation Table (FAT) → Maps cluster chains, tracks status (used, free, end-of-file).

👉 Files = data in clusters + directory entry + FAT chain.

🔹 FAT Variants
Attribute			FAT12		FAT16		FAT32 (28-bit)
Addressable bits	12			16			28
Max clusters		4,096		65,536		268,435,456
Cluster size		512B–8KB	2KB–32KB	4KB – 32KB
Max volume size		32MB		2GB			2TB (Win limits to 32GB)
Max file size		~4GB		~4GB		~4GB

🔹 Usage & Relevance
FAT12 → obsolete (old floppy disks).
FAT16 → rare, but still on small storage.
FAT32 → common on USB drives, SD cards, cameras.

Limitation → max file size = 4GB (cannot store larger single files).

✅ Forensics view:
FAT systems are simple → good for recovery, as file structure is flat.
Deleted files can often be recovered unless clusters are overwritten (directory entry remains, FAT chain marked free).
FAT timestamps (Created, Modified, Accessed) can help in timeline analysis.

🔹 exFAT File System

Why created?
	FAT32 limited to 4GB per file.
	NTFS too heavy for lightweight media devices.
	Microsoft designed exFAT (Extended FAT) at the request of digital device makers.

🔹 Key Features
	Default for SD cards > 32GB (adopted by cameras, phones, storage devices).
	Cluster size: 4KB – 32MB.
	Max file size: 128 PB (no 4GB limitation).

Max volume size: 128 PB.
Max files per directory: ~2.8 million.

Optimizations:
	Lower overhead than FAT.
	Lightweight compared to NTFS.
	No journaling (like FAT, so recovery artifacts may persist).

🔹 Forensic Relevance
	Large media evidence → most modern SDXC cards (64GB+) use exFAT.
	Deleted file recovery: Similar to FAT, but with larger cluster sizes (risk of slack space).
	Timestamps: exFAT keeps Created, Modified, and Accessed times (but with 10ms granularity, UTC based).

Cross-platform: Supported natively in Windows & macOS (Linux requires exFAT driver).

Why NTFS > FAT/exFAT:
NTFS adds journaling, access controls, volume shadow copies, alternate data streams, and the Master File Table (MFT). 
These features make it more secure, reliable, and forensic-rich compared to FAT/exFAT.

Important NTFS artifacts:
	$MFT → Contains metadata of all files.
	$LOGFILE → Journaling of metadata changes.
	$UsnJrnl → Tracks file changes.
	$Extend → Extra system data.
	
MFTECmd tool usage:
	Command to parse MFT into CSV:
		MFTECmd.exe -f "C:\Users\THM-4n6\Desktop\triage\C\$MFT" --csv "C:\Users\THM-4n6\Desktop\output"
	
	You can also parse $Boot, $J, etc. (but not $LOGFILE yet).
	Results → open with EZViewer (in EZTools) or Excel.

File System		Deletion Marker in Metadata		Space Tracking					Data Overwritten?
FAT12/16/32		Dir entry 1st byte → 0xE5;		FAT entries set to 0x0000		Not immediately 
				FAT chain cleared	
exFAT			Dir entry 1st byte → 0xE5;		Allocation Bitmap cleared		Not immediately 
				Stream entries kept	
NTFS			MFT flag IN_USE cleared;		Bitmap marks clusters free		Not immediately 
				$BITMAP updated	
ext2/3/4		Inode link count decremented	Block bitmap marks free			Not immediately (but journaling may zero)
HFS+			Catalog entry removed			Allocation file marks free		Not immediately
APFS			Metadata reference dropped(CoW)	Space marked free in container	Not immediately (snapshots preserve)


EVIDENCE OF EXECUTION

Windows Prefetch (.pf files)
	C:\Windows\Prefetch
What it shows:	Last execution time(s); Number of executions; Files/devices accessed by the program
Prefetch Parser:	PECmd.exe -d "C:\users\thm-4n6\Desktop\triage\C\Windows\Prefetch" --csv "C:\output"
-f for a file and -d for a directory

Windows 10 Timeline (ActivitiesCache.db)
	C:\Users\<username>\AppData\Local\ConnectedDevicesPlatform\{random}\ActivitiesCache.db
What it shows:	Applications executed; Focus (active) time of each app
Tool & Usage: WxTCmd.exe -f <path-to-timeline-file> --csv <path-to-save-csv>
WxTCmd.exe -f "C:\users\thm-4n6\Desktop\triage\C\Users\<username>\AppData\Local\ConnectedDevicesPlatform

Jump Lists (AutomaticDestinations-ms / CustomDestinations-ms)
	C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations
What it shows: Applications used, Files opened via apps, First and last execution times
Tool & Usage: JLECmd.exe -d "C:\users\thm-4n6\Desktop\triage\C\Users\<username>\AppData\Roaming\Microsoft\Windows\Rec
JLECmd.exe -f <path-to-Jumplist-file> --csv <path-to-save-csv>


Shortcut Files (.lnk)
	C:\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent\
	C:\Users\<username>\AppData\Roaming\Microsoft\Office\Recent\
LECmd.exe -d "C:\Users\THM-4n6\Desktop\triage\C\Users\<username>\AppData\Roaming\Microsoft\Windows\Recent" --csv C:\output

IE/Edge WebCache (WebCacheV*.dat)
	C:\Users\<username>\AppData\Local\Microsoft\Windows\WebCache\WebCacheV*.dat
What they show: Browsing history; Files accessed (with prefix file:///C:/...); Even non-browser file opens are recorded


## Setupapi.dev.log
	C:\Windows\inf\setupapi.dev.log

What it records: Device installation/setup activity; USB Device ID and Serial Number; First & last connected times
Use case: Identify when a USB device was first introduced and last used.

Example log snippet:
>>>  [Device Install (Hardware initiated) - USBSTOR\Disk&Ven_SanDisk&Prod_Cruzer_Glide&Rev_1.00\1234567890ABCDEF&0]
>>>  Section start 2022/12/01 15:32:44.123

Here: 1234567890ABCDEF → Device Serial Number; Timestamp → First connection

