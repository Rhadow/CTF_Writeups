# In reverse shell
python -c 'import pty; pty.spawn("/bin/bash")'
Ctrl-Z

# In Kali
=======Optional=======
echo $TERM (result a)
stty -a (result b)
======================
stty raw -echo
fg

# In reverse shell
reset
=======Optional=======
export SHELL=bash
export TERM=(result a from above)
stty row (row from result b) col (col from result b)
======================

