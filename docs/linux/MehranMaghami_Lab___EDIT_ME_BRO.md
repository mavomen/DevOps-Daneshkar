 Review Regular Expressions
In this part, you use the grep command to review how you can use regular expressions for filtering.
Note: Your output may differ than the output shown below as the state of the VM is based on the most recent
iteration that you downloaded as well as any changes you may have made. However, you should get some
output from the passwd file but your highlighted output will differ.
a. Use the grep command to filter the contents of the passwd file to display the line from the passwd file
containing devasc. Notice that the two instances of devasc are highlighted. Also notice that the grep
command is case-sensitive. The instance of DEVASC is not highlighted.
devasc@labvm:~$ grep devasc /etc/passwd
devasc:x:900:900:DEVASC,,,:/home/devasc:/bin/bash
devasc@labvm:~$
b. Use the grep command to show how many times root appears in the passwd file. Notice that all three
instances of root are highlighted.
devasc@labvm:~$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
devasc@labvm:~$
Lab - Linux Review
Mehran Maghami Page 9 of 15
c. Use the grep command with the anchor character ^ to find the word, but only at the beginning of the line.
Notice that only the word at the beginning of the line is highlighted.
devasc@labvm:~$ grep '^root' /etc/passwd
root:x:0:0:root:/root:/bin/bash
devasc@labvm:~$
d. Use the grep command with the anchor character $ to find a word at the end of a line.
devasc@labvm:~$ grep 'false$' /etc/passwd
tss:x:106:114:TPM software stack,,,:/var/lib/tpm:/bin/false
lightdm:x:107:117:Light Display Manager:/var/lib/lightdm:/bin/false
hplip:x:115:7:HPLIP system user,,,:/run/hplip:/bin/false
devasc@labvm:~$
e. Use the grep command with the anchor character . to match specific length words with different letters in
them. Notice that not only is daem highlighted, but also dnsm is highlighted.
devasc@labvm:~$ grep 'd..m' /etc/passwd
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
avahi-autoipd:x:110:121:Avahi autoip daemon,,,:/var/lib/avahiautoipd:/usr/sbin/nologin
usbmux:x:111:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
avahi:x:113:122:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
colord:x:116:125:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
pulse:x:117:126:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
devasc@labvm:~$
f. Use the grep command to find lines where only the numbers 8 or 9 are present. Notice that only the lines
containing an 8, a 9, or both are returned.
devasc@labvm:~$ grep '[8-9]' /etc/passwd
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
uuidd:x:103:109::/run/uuidd:/usr/sbin/nologin
devasc:x:900:900:DEVASC,,,:/home/devasc:/bin/bash
systemd-network:x:999:999:systemd Network Management:/:/usr/sbin/nologin
systemd-resolve:x:998:998:systemd Resolver:/:/usr/sbin/nologin
systemd-timesync:x:997:997:systemd Time Synchronization:/:/usr/sbin/nologin
systemd-coredump:x:996:996:systemd Core Dumper:/:/usr/sbin/nologin
rtkit:x:108:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
devasc@labvm:~$
g. Use the grep command to find literal characters. Notice that only the lines containing a comma are
returned.
devasc@labvm:~$ grep '[,]' /etc/passwd
devasc:x:900:900:DEVASC,,,:/home/devasc:/bin/bash
tss:x:106:114:TPM software stack,,,:/var/lib/tpm:/bin/false
rtkit:x:108:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
Lab - Linux Review
Mehran Maghami Page 10 of 15
avahi-autoipd:x:110:121:Avahi autoip daemon,,,:/var/lib/avahiautoipd:/usr/sbin/nologin
usbmux:x:111:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
kernoops:x:112:65534:Kernel Oops Tracking Daemon,,,:/:/usr/sbin/nologin
avahi:x:113:122:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
hplip:x:115:7:HPLIP system user,,,:/run/hplip:/bin/false
colord:x:116:125:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
pulse:x:117:126:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
devasc@labvm:~$
h. Use the grep command to find occurrences of zero or more of the pattern preceding it. Notice that only
the lines with either new and ne are returned.
devasc@labvm:~$ grep 'new*' /etc/passwd
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
messagebus:x:100:103::/nonexistent:/usr/sbin/nologin
_apt:x:102:65534::/nonexistent:/usr/sbin/nologin
tcpdump:x:104:110::/nonexistent:/usr/sbin/nologin
systemd-network:x:999:999:systemd Network Management:/:/usr/sbin/nologin
kernoops:x:112:65534:Kernel Oops Tracking Daemon,,,:/:/usr/sbin/nologin
saned:x:114:124::/var/lib/saned:/usr/sbin/nologin
devasc@labvm:~$
Pa
