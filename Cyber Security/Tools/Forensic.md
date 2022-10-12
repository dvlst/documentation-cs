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
python3 vol.py -f memdump.raw windows.pslist | Select-String filename
```

- Filter Windows Handles after PID
```
python3 vol.py -f memdump.raw windows.handles --pid 1328
```

- Filter Windows Handles after PID and type
```
python3 vol.py -f memdump.raw windows.handles --pid 1328 | Select-String File | more
```

- Dump all files associated with PID 3784.
```
python3 vol.py -f memdump.raw windows.dumpfiles.DumpFiles --pid 3784 |
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
python vol.py -f memdump.raw windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion" --recurse
```

- Save memdump to a .dmp file
```
python3 vol.py -f memdump.raw windows.memmap.Memmap  --pid 368 -–dump
```

- ( Use Grep to find something in the .dmp file)
```
strings pid.368.dmp | grep "filename" | grep -v “filetype”
```

### Volatility2 Commands
- Show image information
```
python vol.py -f memdump.raw imageinfo
```

```
python vol.py -f memdump.raw kdbgscan
```

- Network Info from Windows
```
python vol.py --profile=Win7SP1x86_23418 netscan -f memdump.raw 
```

- Network Info from Linux
```
python vol.py --profile=SomeLinux -f memdump.raw linux_ifconfig
```

- Show Process Tree
```
python vol.py -f memdump.raw --profile=Win7SP1x86 pslist
```

- Show all running processes with full command line used
```
python vol.py -f memdump.raw --profile=Win7SP1x86 cmdline
```

- Dump an executable file
```
python vol.py -f memdump.raw --profile=Win7SP1x86 -p PID -D folder/
```

- Show the NTLM hash of the all users
```
python vol.py -f memdump.raw --profile=Win7SP1x86 hashdump
```

- Create a executable.exe file with PID
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 procdump --dump-dir . -p 368
```

- Create a executable.exe with physical memory adress
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000007dd6e038 -D .
```

- Search memdump after filename
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 filescan | grep -i filename
```

- Search memdump after file-extension
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 filescan | grep -i filename | grep -v filetype
```

- Search memdump after Windows Service Records
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 svcscan
```

- Search memdump after COMMAND_HISTORY
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 cmdscan
```

- Search memdump after CONSOLE_Informations
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 consoles
```

### [MemProcFS](https://github.com/ufrisk/MemProcFS)
- Alternative zu Volatility für Windows
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

## [Autopsy](https://www.autopsy.com/)
- Tool für Disk Forensic
- Vorinstalliert unter Kali Linux
- Bietet UI für Durchsuchung von Disks

### Syntax
- Starten von Autopsy
```
sudo autopsy
```

- Nachher kann man sich auf localhost:9999/autopsy verbinden

## [Photorec](https://www.cgsecurity.org/wiki/PhotoRec_Step_By_Step)
- Tool für Wiederherstellung von bereits gelöschten Files
- Vorinstalliert auf Kali Linux

### Syntax
```
photorec disk.img
```