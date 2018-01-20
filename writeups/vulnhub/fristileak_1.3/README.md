## Recon:

dirb result:
/cgi-bin/: possible shellshock attack
/images: listable
/icons: listable
/robot.txt

robot.txt content:
/cola
/sisi
/beer

Since all subdirectories and box name are drinks, it's easy to guess `/fristy` to be a subdirectory too.

## Exploit

/frist gives us login page

In dev console, there are username (eezeepz) and base64 encoded password. Decoded the base64 string gives a password image.
Login with provided credentials and an upload page is presented.

Upload a php backdoor with name `backdoor.php.jpg` since the upload page only checks if file is ended with jpg/png/gif.

## Privilege Escalation

Go to `/home/eezeepz` and found a note saying we can run some of the commands using admin priviledge.
By echoing `chmod 777 /home/admin` to `/tmp/runthis`, the cron job will make admin folder accessible in a min.

Read admin folder can further get crypted password for user `admin` and `fristigod`.

change to user `fristigod` by using `su` and found an executable file name `doCom` under a hidden folder.
By running `sudo -l` will give us following result:

```
User fristigod may run the following commands on this host:
    (fristi : ALL) /var/fristigod/.secret_admin_stuff/doCom
```

which means we can run `doCom` as user `fristi`. Therefore running the following command will give us root access:

`sudo -u fristi ./doCom bash`

since `doCom` will run the arguments as command using root privilege.

