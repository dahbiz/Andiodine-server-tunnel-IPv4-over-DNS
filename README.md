# Andiodine-server
Andiodine is a DNS tunneling solution that allows you to route IPv4 traffic through a DNS server. This is very useful in situations where internet access is restricted but DNS queries are not. Furthermore, Andiodine is an excellent way to circumvent wifi logins and secure your web traffic in public places!

To create an Andiodine server you need:

       ✦ VPS server with an IPv4 adress.
       ✦ Domain name with A and NS records.

Follow the steps outlined below.
     
## Configuring Domain name.

Assume you have the domain name *domain.com*. 
  
  - Create an A record by pointing a subdomain  *subd1.domain.com* to your vps IP adress.
  - Create an NS record by pointing another subdomain  *subd2.domain.com* to subd1.domain.com.
  
Everything appears to be in order now!

## Configuring the VPS.

Login to your virtual server via SSH using the terminal or another ssh client and run the following commands as root.

### Update and install Iodine

           ♯ apt-get update
           ♯ apt-get install iodine
           
### Enable IPv4 IP-forwarding feature
```
           ♯ sysctl -w net.ipv4.ip_forward=1
```          
### Apply the following firewall rules
           
           ♯ /sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
           ♯ /sbin/iptables -A FORWARD -i eth0 -o dns0 -m state –state RELATED,ESTABLISHED -j ACCEPT
           ♯ /sbin/iptables -A FOlRWARD -i dns0 -o eth0 -j ACCEPT
           ♯ iptables-save > /etc/iptables.rules
           
### Run Andiodine in the background

           ♯ iodined -f -c -m 1280 -DDDDD -P xxxxx 10.0.0.1 subd2.domain.com &
           
**xxxxx** is the password, you can change it.

Now we've completed the server-side configuration, let's move on to the client-side.

### Andiodine android
Downlaod [iodine client](https://f-droid.org/en/packages/org.xapek.andiodine/)  for android 4.+. 

![Andiodine client](https://raw.githubusercontent.com/etriZiko/Andiodine-server/master/Iodine.jpg)

Connect and enjoy the freedom!

### AUTHOR MESSAGE
Please keep in mind that this is only for educational reasons and should not be used to facilitate illegal traffic or to hurt others.
