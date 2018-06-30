# CEDFP v0.1  
## Claymore ETH DevFleaProxy  

### Warning:  
This software is for educational purposes only. :P  
There, you can't sue me now. ;)  
The authors will take no responsibility for any damages (legal, material, physical, monetery, emotional and/or mental) caused by the use or misuse of their creation.  
AKA: "You're on your own buddy."

By using this program you agree to donate 1 out of 100 intercepted devfees to the developers.  
(About one devflea session every 4 days)  

Written by somebody for the private-locker community.  
The "Community Owned" pools  
https://www.private-locker.com/  
https://discord.gg/4tHbunB  
https://twitter.com/Private_Locker  

&nbsp;

Usage:  
`./cedfp.<arch> <local ip/hostname> <local port> <remote ip/hostname> <remote port> \`  
`<your wallet address(. or /)workername>`

Example:  
`./cedfp.amd64 localhost 9326 pool.private-locker.com 6239 \`  
`0x0123456789AbCdEf0123456789aBcDeF01234567.devflea`

The workername can be different.  We suggest using a unique worker name just to see your devfleas come back :)

Ports can be within the range of 1024 to 65535.

Your wallet address is case sensitive, make it the same as in your miner config.  If you do not set it exactly the same EVERY connection will be considered a devflea!  We do not want to see a 12 gpu rig connect on a donation round and mine there for 12hrs m'k.  Ok I'm lieing... but don't do it :) Make sure your normal miners are not detected as a devflea.

&nbsp;

**Designed from the ground up with low latency in mind.**

&nbsp;

This proxy is a little tricky to setup but if you do it right you will take back your ETH Claymore devfleas without any penalty.  
Tested with Claymore v11.8 without -allpools. (I do not know a pool that needs it yet)  

&nbsp;

First of all, we would like to start with a list of things that __***DO NOT WORK***!__  

### __DO ***NOT*** DO THIS:__  

A)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local host to 127.0.0.1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local port to CORRECT pool port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote host to the pools hostname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote port to the pools non ssl port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set Claymore to connect to the proxys local host and port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore complains about being behind a proxy  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore sends 10% stale shares like clockwork  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-devflea goes through 127.0.0.1 (caught by proxy)  

B)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local host to 127.0.0.1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local port to WRONG pool port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote host to the pools hostname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote port to the pools non ssl port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set Claymore to connect to the proxys local host and port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore complains about being behind a proxy  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore sends 10% stale shares like clockwork  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-devflea goes through 127.0.0.1 (caught by proxy)  

C)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Take possession of the pool domain and set it 127.0.0.1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local host to 127.0.0.1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local port to CORRECT pool port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote host to the pools hostname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote port to the pools non ssl port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set Claymore to connect to the pools host and port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore complains about being behind a proxy  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore sends 10% stale shares like clockwork  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-devflea goes through pool hostname ssl port  

D)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Take possession of the pool domain and set it 127.0.0.1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local host to 127.0.0.1  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy local port to WRONG pool port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote host to the pools hostname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy remote port to the pools non ssl port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set Claymore to connect to the pools host and the proxys local port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore complains about being behind a proxy  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore sends 10% stale shares like clockwork  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-devflea goes through pool hostname non ssl port (caught by proxy)  

### **THANKS FOR NOT DOING THE ABOVE METHODS!**  
### **YOU WILL LOSE 9% INSTEAD OF SAVING 1%**  

&nbsp;

#### Here are things that do work:  

A)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy transparent on the CORRECT non ssl pool port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set Claymore to connect to pool hostname CORRECT port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore stops complaining about being behind a proxy  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore stops staling shares  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-devflea goes through pool ssl port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;(the proxy is not ssl "YET!" We do not even know if that will work "YET!")  

B)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the proxy transparent on a random port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set Claymore to connect to pools hostname on the random port  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore stops complaining about being behind a proxy  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-Claymore stops sending stale shares  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-devflea goes through non ssl random pool port (caught by proxy!)  

A) Will probably work when I add ssl to the proxy  
**B) WORKS!**  

&nbsp;

If you do not know what a transparent proxy is, Google it ;)  
For my installation I used my OpenWRT router to host the transparent proxy.  My rig is hopping through that point anyways so it's not an extra network hop, practically 0ms latency this way.  Now I will not go into the details of turning your stock router into a Linux  based open source routing monster, but you can visit OpenWRTs website it's all there.

Any linux i386, amd64, mips will run this proxy, use what you've got.

&nbsp;

## Here's how to set it up on an OpenWRT router:  

A) If you don't already have an OpenWRT based routing device: get or make one  

B) Setup your router so it works like you want it to (wifi lan bla bla)

C) SSH your router as root

D) Package installation, we need a few things type in these commands:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# opkg update`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# opkg install libpthread wget openssl-util screen nano`

E) Add a proxy user because you never want to run anything as root unless you really have to:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# echo "proxy:x:1000:1000:proxy:/home/proxy:/bin/ash" >> /etc/passwd`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# echo "proxy:x:1000:" >> /etc/group`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# mkdir -p /home/proxy`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# chown 1000:1000 /home/proxy`

F) Set the new users password:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# passwd proxy`
  
  
G) Set the transparent proxy firewall rule:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~#  nano /etc/firewall.user`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Add this line to the bottom:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`iptables -t nat -I PREROUTING -p tcp -d <pool hostname> --dport <some random port #> \`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`-j REDIRECT --to-port <proxy local port>`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;example:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# iptables -t nat -I PREROUTING -p tcp -d eth.pool.private-locker.com \`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`--dport 12345 -j REDIRECT --to-port 54321`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Save and exit "CTRL+x"

H) Restart the firewall to apply the custom rule:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`root@OpenWRT:~# /etc/init.d/firewall restart`

I) Logout of your router, login with new proxy user.

J) Download CEDFP uncompress it and delete the tarball:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`proxy@OpenWRT:~# wget https://github.com/private-locker/CEDFP/raw/master/cedfp-current-mips.tar`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`proxy@OpenWRT:~# tar -xf cedfp-current-mips.tar`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`proxy@OpenWRT:~# rm cedfp-current-mips.tar`  

K) Start a proxy screen (that screen program we installed earlier) If you don't know how to use it, Google is your best friend.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`proxy@OpenWRT:~# screen -S proxy`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ok... just the basics do:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"CTRL+a d" (you just exited the screen)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Type: `screen -r proxy` (you just rejoined your proxy screen)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Rince and repeate 3 times so you remember :P  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can view your screen list and see if you are attached to it with: `screen -list`

L) Make sure you are attached to your screen! start your proxy:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`./cedfp.mips <router lan ip/hostname> <proxy local port> <pool ip/hostname> <pool non ssl port #> \`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`<your wallet address(. or /)workername>`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;example:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`./cedfp.mips 192.168.0.1 54321 eth.private-locker.com 6824 \`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`0x0123456789AbCdEf0123456789aBcDeF01234567.devflea`

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can sit there and watch it or "CTRL+a d" out of your screen and logout of your router.  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;You can always rejoin your screen later, just ssh your router with the proxy user and type:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`screen -r proxy`

M) Set claymore to connect to the pools hostname with that random port # you chose in the firewall rule. Start Claymore

&nbsp;

Future plans:  
A) Add SSL support.  
B) Lower the donation agreement when the authors can eat 3 meals a day. (a car and house would be nice too) ;)

&nbsp;

Inspiration:  
A) Realizing that Claymore is making MILLIONS a month off the back of little homebrew GPU miners.  
B) Robin Hood, Steal from the rich give to the poor.

&nbsp;

Happy devfee free mining from the Private Locker community.
