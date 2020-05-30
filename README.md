![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2020-05-30)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
89.234.157.254|marylou.nos-oignons.net|9
18.27.197.252|wholesomeserver.media.mit.edu|9
185.165.168.229|-|9
46.165.230.5|tor-exit.dhalgren.org|9
193.70.13.31|ns3061803.ip-193-70-13.eu|9
37.49.226.183|-|8
185.220.100.253|tor-exit-2.zbau.f3netze.de|8
77.247.181.165|politkovskaja.torservers.net|8
77.247.181.162|chomsky.torservers.net|8
158.69.35.227|tor-exit.ubermen.net|8
37.49.226.155|-|8
51.77.135.89|ns31066279.ip-51-77-135.eu|8
37.49.226.173|-|8
77.247.181.163|lumumba.torservers.net|8
51.75.52.118|ns3130898.ip-51-75-52.eu|8
195.206.105.217|zrh-exit.privateinternetaccess.com|8
51.158.111.157|157-111-158-51.rev.cloud.scaleway.com|8
193.70.12.205|ns3061447.ip-193-70-12.eu|8
37.49.226.230|-|7
37.49.226.237|-|7
37.49.226.181|-|7
51.15.80.14|14-80-15-51.rev.cloud.scaleway.com|7
27.78.14.83|localhost|7
104.244.72.115|tor-exit-hermes.greektor.net|7
185.232.65.105|-|7
217.170.205.14|tor-exit-5014.nortor.no|7
185.220.100.252|tor-exit-1.zbau.f3netze.de|7
185.170.114.25|this-is-a-tor-node---10.artikel5ev.de|7
37.49.226.23|-|7
185.220.101.214|-|7
185.220.101.210|-|7
185.220.101.211|-|7
193.70.12.236|ns3061478.ip-193-70-12.eu|7
193.70.12.238|ns3061480.ip-193-70-12.eu|7
193.70.12.219|ns3061461.ip-193-70-12.eu|7
45.95.168.221|maxko-hosting.com|7
185.220.101.213|-|7
171.25.193.20|tor-exit0-readme.dfri.se|7
37.49.226.152|painstress.online|7
37.49.226.157|-|7
194.61.24.177|-|7
51.75.144.43|ns3129517.ip-51-75-144.eu|7
185.220.101.193|-|7
51.15.177.65|tor.tor.loki.life.tor.life.loki.tor.tor.loki.life.life.tor.life.loki.tor.loki.life|7
185.220.100.241|tor-exit-14.zbau.f3netze.de|7
193.70.12.240|ns3061482.ip-193-70-12.eu|7
185.220.101.229|-|7
23.129.64.197|-|7
185.220.101.207|-|7
185.220.101.202|-|7
185.100.87.206|geri.enn.lu|7
