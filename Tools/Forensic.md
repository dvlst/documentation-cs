## [Volatility](https://www.volatilityfoundation.org/releases)
- Tool zum Memory Dumps analyisieren
- [Cheat Sheet Tools Volatility Commands](https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/memory-dump-analysis/volatility-examples)
- [Volatility Command Reference](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference)

### Volatility 2 install Windows
- Clone Repository from GitHub
```
git clone https://github.com/volatilityfoundation/volatility.git
```

- Make sure Python27 is installed
- Add Python27 to PATH System Variable (/Path/to/Python27/ & /Path/to/Python27/Scripts/)
- Rename python.exe (Python3) to python3.exe (%APPDATA%/Local/Programs/Python/Python310/)
- Install Visual C++ for Python27 from [Wayback Machine](https://web.archive.org/web/20190720195601/http://www.microsoft.com/en-us/download/confirmation.aspx?id=44266)

- Install distorm3 with pip
```
pip install distorm3
```
- Install pycrypto with pip
```
pip install pycrypto
```

### Volatility3 install Windows
- Clone Repository from GitHub
```
git clone https://github.com/volatilityfoundation/volatility3.git
```

- If you get an error with pip3 you can reinstall it wth following command:
```
python3 -m pip install --upgrade --force-reinstall pip
```

- Install requirements
```
pip3 install -r requirements.txt
```

- If you have an C++ error you must install the [C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)
- Then you have to install the Desktop developement with C++

![[Pasted image 20220828213350.png]]

- If you get an Python-Snappy error while installing the requirements you have to install the python snappy module from the [Unofficial Windows Binaries for Python](https://www.lfd.uci.edu/~gohlke/pythonlibs/#python-snappy)
```
pip3 install \Path\To\python-snappy
```

- With this command you can show your supported version (cp310-cp310 worked for me):
```
pip3 debug --verbose
```

- You have to edit the requirements.txt to edit the python-snappy version:
```
...
python-snappy==0.6.1
```

- Install the symbols required for the different OS ([windows](https://downloads.volatilityfoundation.org/volatility3/symbols/windows.zip) [mac](https://downloads.volatilityfoundation.org/volatility3/symbols/mac.zip) [linux](https://downloads.volatilityfoundation.org/volatility3/symbols/linux.zip)) and unpack them into the /volatility3/volatility3/symbols/ folder

### Volatility3 Commands
- Show Info about the image
```
python3 vol.py -f memdump.raw windows.info
```

- Network Info from Windows
```
python3 vol.py -f memdump.raw windows.netscan
```

- Show Process Tree
```
python3 vol.py -f memdump.raw windows.pslist
```

- Show Hidden Processes
```
python3 vol.py -f memdump.raw windows.psscan
```

- Filter process tree after filename
```
python3 vol.py -f memdump.raw windows.pslist | Select-String [Filename]
```

- Filter Windows Handles after PID
```
python3 vol.py -f memdump.raw windows.handles --pid [PID]
```

- Filter Windows Handles after PID and type
```
python3 vol.py -f memdump.raw windows.handles --pid [PID] | Select-String File | more
```

- Dump all files associated with PID.
```
python3 vol.py -f memdump.raw windows.dumpfiles.DumpFiles --pid [PID]
```

- See executed programs with command option history.
```
python3 vol.py -f memdump.raw windows.cmdline.CmdLine
```

- See active network connections and listening programs.
```
python3 vol.py -f memdump.raw windows.netstat
```

- Dump the Windows user password hashes.
```
python3 vol.py -f memdump.raw windows.hashdump.Hashdump
```

- Print out the Windows Registry UserAssist.
```
python3 vol.py -f memdump.raw windows.registry.userassist.UserAssist
```

- List all available Windows Registry hives in memory.
```
python3 vol.py -f memdump.raw windows.registay.hivelist.HiveList
```

- Dump the ntuser hive based on a keyword filter.
```
python3 vol.py -f memdump.raw -o "dump" windows.registry.hivelist --filter Doe\ntuser.dat --dump
```

- Print a specific Windows Registry key.
```
python3 vol.py -f memdump.raw] windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion" --recurse
```

- Print a specific Windows Registry key, subkeys and values.
```
python3 vol.py -f memdump.raw windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion" --recurse
```

- Save memdump to a .dmp file
```
python3 vol.py -f memdump.raw windows.memmap.Memmap?? --pid 368 -???dump
```

- ( Use Grep to find something in the .dmp file)
```
strings pid.368.dmp | grep [Filename] | grep -v [Filetype]
```

- Search memdump after COMMAND_HISTORY
```
python3 -f memdump.raw windows.cmdline
```

- Check SID of User which executed a Process with PID
```
python3 vol.py -f memdump.raw --profile=Win7SP1x86_23418 --pid [PID] windows.getsids.GetSIDs
```

- Check SID of User which executed a Service with PID
```
python3 vol.py -f memdump.raw --profile=Win7SP1x86_23418 --pid [PID] windows.getsids.GetServiceSIDs
```

### Volatility2 Commands
- Show image information
```
python2 vol.py -f memdump.raw imageinfo
```

```
python2 vol.py -f memdump.raw kdbgscan
```

- Network Info from Windows
```
python2 vol.py --profile=Win7SP1x86_23418 netscan -f memdump.raw 
```

- Network Info from Linux
```
python2 vol.py --profile=SomeLinux -f memdump.raw linux_ifconfig
```

- Show Process Tree
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86 pstree
```

- Show Process List
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86 pslist
```

- Show all running processes with full command line used
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86 cmdline
```

- Dump an executable file
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86 procdump -p [PID] -D [Path]
```

- Show the NTLM hash of the all users / Find out Password Hash
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86 hashdump
```

- Create a executable.exe file with PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 procdump -D [Path] -p [PID]
```

- Create a executable.exe with physical memory adress
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 dumpfiles -Q [Adresse] -D [Path]
```

- Extract a Driver File with PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 -p [PID] moddump -D [Path]
```

- Extract a DLL File with PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 -p [PID] dlldump -D [Path] 
```

- Find hidden injected Code / DLLs with PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 -p [PID] malfind
```

- Search linked DLL from PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 -p [PID] impscan
```

```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 -p [PID] dlllist
```

- Search memdump after filename
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 filescan | grep -i [Filename]
```

- Search memdump after file-extension
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 filescan | grep -i [Filename] | grep -v [Filetype]
```

- MFT Parser (Shows Files from the Master File Table / Every File on NTFS File System with Info)
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 mftparser
```

- Search memdump after Windows Service Records
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 svcscan
```

- Search memdump after COMMAND_HISTORY
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 cmdscan
```

- Search memdump after CONSOLE_Informations
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 consoles
```

- Check SID of User which executed a Process with PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 -p [PID] getsids
```

- Check SID of User which executed a Service with PID
```
python2 vol.py -f memdump.raw --profile=Win7SP1x86_23418 --pid [PID] getservicesids
```

- Search for additional modules
```
python2 vol.py -h | grep [Text]
```

### [MemProcFS](https://github.com/ufrisk/MemProcFS)
- Alternative zu Volatility f??r Windows
- Memory Dump in Laufwerk mounten:
```
MemProcFs.exe -device memory-dump.raw -forensic 1 
```

## log2timeline / [plaso](https://plaso.readthedocs.io/en/latest/sources/user/Using-log2timeline.html)
- Plaso-File aus vhdx oder memory dump erstellen
- vhdx-File mit Disk2vhd aus Sysinternals erstellen auf Windows
- Plaso-File erstellen:
```
log2timeline.py --storage-file *Name*.plaso *Name*.VHD
```

## [timesketch](https://github.com/kovakina/timesketch/blob/master/docs/SearchQueryGuide.md)
- Plaso-File anaylisieren mit GUI
- [Search query Guide](https://timesketch.org/guides/user/search-query-guide/)

### Syntax
- Show Shutdown
```
data_type:"windows:registry:shutdown"
```

```
data_type:"windows:evtx:record" AND event_identifier:"1074"
```

- Prefetch Info of Executable
```
data_type:"windows:prefetch:execution" AND executable:"[EXE.exe]"
```

- Show Autostart Applications
```
parser:"windows_run"
```

- Filter for specific File
```
"[FILE]"
```

## [Autopsy](https://www.autopsy.com/)
- Tool f??r Disk Forensic
- Vorinstalliert unter Kali Linux
- Bietet UI f??r Durchsuchung von Disks

### Syntax
- Starten von Autopsy
```
sudo autopsy
```

- Nachher kann man sich auf localhost:9999/autopsy verbinden

## [Photorec](https://www.cgsecurity.org/wiki/PhotoRec_Step_By_Step)
- Tool f??r Wiederherstellung von bereits gel??schten Files
- Vorinstalliert auf Kali Linux

### Syntax
```
photorec disk.img
```