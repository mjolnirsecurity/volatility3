# volatility3
commands and test dumps
OS information
python3 vol.py -f file.dmp windows.info.Info

Hashes/Passwords
python3 vol.py -f file.dmp windows.hashdump.Hashdump #Grab common windows hashes (SAM+SYSTEM)
python3 vol.py -f file.dmp windows.cachedump.Cachedump #Grab domain cache hashes inside the registry
python3 vol.py -f file.dmp windows.lsadump.Lsadump #Grab lsa secrets

Memory Dump
python3 vol.py -f file.dmp --profile=Win7SP1x86 memdump -p 2168 -D conhost/

List processes
python3 vol.py -f file.dmp windows.pstree.PsTree # Get processes tree (not hidden)
python3 vol.py -f file.dmp windows.pslist.PsList # Get process list (EPROCESS)
python3 vol.py -f file.dmp windows.psscan.PsScan # Get hidden process list(malware)

Dump Process
python3 vol.py -f file.dmp windows.dumpfiles.DumpFiles --pid <pid> #Dump the .exe and dlls of the process in the current directory

Command Line data
python3 vol.py -f file.dmp windows.cmdline.CmdLine #Display process command-line arguments

Privileged Tokens
#Get enabled privileges of some processes
python3 vol.py -f file.dmp windows.privileges.Privs [--pid <pid>]
#Get all processes with interesting privileges
python3 vol.py -f file.dmp windows.privileges.Privs | grep "SeImpersonatePrivilege\|SeAssignPrimaryPrivilege\|SeTcbPrivilege\|SeBackupPrivilege\|SeRestorePrivilege\|SeCreateTokenPrivilege\|SeLoadDriverPrivilege\|SeTakeOwnershipPrivilege\|SeDebugPrivilege"

SSID/SID
python3 vol.py -f file.dmp windows.getsids.GetSIDs [--pid <pid>] #Get SIDs of processes
python3 vol.py -f file.dmp windows.getservicesids.GetServiceSIDs #Get the SID of services

Strings
strings file.dmp > /tmp/strings.txt
python3 vol.py -f /tmp/file.dmp windows.strings.Strings --strings-file /tmp/strings.txt

UserAssist
python3 vol.py -f file.dmp windows.registry.userassist.UserAssist

Network connections
python3 vol.py -f file.dmp windows.netscan.NetScan

Malware Hunting
python3 vol.py -f file.dmp windows.malfind.Malfind [--dump] #Find hidden and injected code, [dump each suspicious section]
#Malfind will search for suspicious structures related to malware
python3 vol.py -f file.dmp windows.driverirp.DriverIrp #Driver IRP hook detection
python3 vol.py -f file.dmp windows.ssdt.SSDT #Check system call address from unexpected addresses

Timeliner
python3 vol.py -f file.dmp timeLiner.TimeLiner
