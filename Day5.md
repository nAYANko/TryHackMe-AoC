# Day 5
Here we will learn the basics of DOS and the windows command prompt. We are shown some baisc dos commands

![Screenshot (107)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/e92722d2-d4ab-4e37-979a-f51848acffaf)

![Screenshot (108)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/490e4ee6-965c-4b32-9e80-ceee10dbc7d2)

********
1. cls to clear screen
2. dir to list contents if a directory
3. cd to change directory, eg. cd notes to switch to directory called notes, cd .. to go back to parent directory
4. type followed by filename to list file contents, OR use edit followed by file name to view and edt file content
.........................................................................
File signatures, commonly referred to as "magic bytes", are specific byte sequences at the beginning of a file that identify or verify its content type and format. These bytes often have corresponding ASCII characters, allowing for easier human readability when inspected. The identification process helps software applications quickly determine whether a file is in a format they can handle, aiding operational functionality and security measures.

In cyber security, file signatures are crucial for identifying file types and formats. You'll encounter them in malware analysis, incident response, network traffic inspection, web security checks, and forensics. Knowing how to work with these magic bytes can help you quickly identify malicious or suspicious activity and choose the right tools for deeper analysis.

Some examples of this are [PNG : 89 50 4E 47 0D 0A 1A 0A, GIF : 47 49 46 38, DOS executable : 4D 5A, Linux ELF executbale : 7F 45 4C 46, MP3 : 49 44 33]
..........................................................................

Navigating to C:\DEV\HELLO we see a file HELLO.C, we open it with "Borland Turbo C compiler" as `TC HELLO.C`

![Screenshot (112)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/bc423543-0f06-405f-9651-8b8b85552d9b)

Alt+C for compile menu and then 'BUILD ALL', now exit

![Screenshot (113)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/8fcdda85-cd2b-431b-9565-26a2b566986a)

We can see a file called HELLO.EXE and when we view that file with `EDIT HELLO.EXE`  we see the file signature to be "MZ" that shows its a windows or dos executable.


********

Now we move to the challenge,

We need to restore AC2023.BAK file,

1. We move to C:\TOOLS\BACKUP and run the command `BUMASTER.EXE C:\AC2023.BAK` which shows an error

![Screenshot (110)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/6e4c9ff8-4a95-4f3e-9ec9-36b0dd467bbb)

2.  We check the suggested file by `EDIT README.TXT` which opens a GUI to edit files, now naviagte to the 'troubleshooting' section

![Screenshot (111)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/31573c62-7f2c-4636-9d50-7c4e7ece25dc)

It says the file signature has to be "41 43" , alt+F and exit

3. Open AC2023.BAK with `EDIT AC2023.BAK` the current file signature is "XX", as we read it should be " 41 43 " which is "AC" when converted ASCII, make this change and save the file.


4. Run `BUMASTER.EXE C:\AC2023.BAK` again and this time is should work to give you the flag : "THM{0LD_5CH00L_C00L_d00D}"

![Screenshot (114)](https://github.com/nAYANko/TryHackMe-AoC/assets/147973815/62a572f9-f164-4e1c-9464-4b3dff9cac88)


ANSWERS TO QUESTIONS:
1. Size of AC2023.BAK -> 12,704 bytes  (dont forget that comma)
2. Name of the backup program -> BackupMaster3000    (found in the README.TXT file)
3. Correct bytes for file signature -> 41 43
4. The required flag -> THM{0LD_5CH00L_C00L_d00D}

