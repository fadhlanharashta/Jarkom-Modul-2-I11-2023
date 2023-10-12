# Jarkom-Modul-2-I11-2023
Muhammad Fadhlan Ashila Harashta - 5025211068<br>
Hanifi Abrar Setiawan - 5025211066<br>
I Putu Arya Prawira Wiwekananda - 5025211065<br>

## Topology
![topology](https://cdn.discordapp.com/attachments/934661338934943774/1161561002656157757/image.png?ex=6538befb&is=652649fb&hm=d18b00fa523b6e04a21c2b27281f381c6d5e7380716ddc05d688f2562594d2b1&)
## Configuration
### Yudhistira
```
auto eth0
iface eth0 inet static
  address 10.79.1.2
  netmask 255.255.255.255.0
  gateway 10.79.1.1
```
### Nakula COnfiguration
```
auto eth0
iface eth0 inet static
  address 10.79.1.3
  netmask 255.255.255.255.0
  gateway 10.79.1.1
```
### Sadewa Configuration
```
auto eth0
iface eth0 inet static
  address 10.79.2.2
  netmask 255.255.255.255.0
  gateway 10.79.2.1
```
### Wekudara Configuration
```
auto eth0
iface eth0 inet static
  address 10.79.2.3
  netmask 255.255.255.255.0
  gateway 10.79.2.1
```
### Prabukusuma Configuration
```
auto eth0
iface eth0 inet static
  address 10.79.3.2
  netmask 255.255.255.255.0
  gateway 10.79.3.1
```
### Abumanyu Configuration
```
auto eth0
iface eth0 inet static
  address 10.79.3.3
  netmask 255.255.255.255.0
  gateway 10.79.3.1
```
### Wisanggeni Configuration
```
auto eth0
iface eth0 inet static
  address 10.79.3.4
  netmask 255.255.255.255.0
  gateway 10.79.3.1
```
### Arjuna Configuration
```
auto eth0
iface eth0 inet static
  address 10.79.3.5
  netmask 255.255.255.255.0
  gateway 10.79.3.1
```
## Terminal Setup 
### Terminal Setup for Pandudewanata
```
uptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.79.0.0/16
```
To see the nameserver
```
cat /etc/resolv.conf
```
### Terminal Setup for Other Nodes
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
Check the nameserver
```
cat /etc/resolv.conf
```
## Question
1. Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut <br>
2. Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.<br>
3. Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.<br>
4. Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.<br>
5. Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)<br>
6. Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.<br>
7. Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.<br>
## Answer
### No 2 Answer
Create main website arhuna.i11.com. <br>
Use nano to edit named.conf.local
```
nano /etc/bind/named.conf.local
```
Inside write
```
zone "arjuna.i11.com"  {
  type master;
  file "/etc/bind/jarkom/arjuna.i11.com";
};
```
Make directory for websites
```
mkdir /etc/bind/jarkom
```
Copy db.local into the directory
```
cp /etc/bind/db.local /etc/bind/jarkom/arjuna.i11.com
```
Use nano to edit the file
```
nano /etc/bind/jarkom/arjuna.i11.com
```
Edit the file as follows
![filesoal2](https://cdn.discordapp.com/attachments/934661338934943774/1161566522498617344/image.png?ex=6538c41f&is=65264f1f&hm=75cc7913b3019496e626f9facb90918201e0daffad63f94bfb43b53c6cc168cb&)
Go to other nodes terminal and then try to ping arjuna.i11.com
![pingsoal2](https://cdn.discordapp.com/attachments/934661338934943774/1161567307869458443/image.png?ex=6538c4db&is=65264fdb&hm=73f531be9d57335d1859fb4b0d60fc165c99769582afededcbfc09eb49e60157&)
### No 3 Answer
A website which accesses abimayu.i11.com with aliases www.abimayu.i11.com<br>
Nano into /etc/bind/named.conf.local
```
nano /etc/bind/named.conf.local
```
Inside write
```
zone "abimanyu.i11.com"  {
  type master;
  file "/etc/bind/jarkom/abimanyu.i11.com";
};
```
Copy db.local into the directory
```
cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.i11.com
```
Use nano to edit the file
```
nano /etc/bind/jarkom/abimanyu.i11.com
```
Inside the file edit as follows
![filesoal3](https://cdn.discordapp.com/attachments/934661338934943774/1161569811210436688/image.png?ex=6538c72f&is=6526522f&hm=a3e213a03d769e998a15e286b9e7c540d4c850aecf2c9424f6cc0eafbc1b558c&)
Restart Bind
```
service bind9 restart
```
Go to other nodes terminal and then try to ping abimanyu.i11.com
![pingsoal3](https://cdn.discordapp.com/attachments/882933764735533076/1161570904384479252/image.png?ex=6538c834&is=65265334&hm=13badc90443f9fe034e8d5b470c1e24d21dc8225c673a0add16b8b1e54e7a26f&)

### No 4 Answer
Nano into /etc/bind/jarkom/abimanyu.i11.com
```
nano /etc/bind/jarkom/abimanyu.i11.com
```
Edit the file as follows
![filesoal4](https://cdn.discordapp.com/attachments/934661338934943774/1161573294818992211/image.png?ex=6538ca6e&is=6526556e&hm=a3d5a915afda1d5ffec7497042fc7dba9c488527202575680d762bb46d1a56a9&)
Restart bind
```
service bind9 restart
```
Ping parikesit.i11.com from other nodes
![pingsoal4](https://cdn.discordapp.com/attachments/934661338934943774/1161573767080837180/image.png?ex=6538cadf&is=652655df&hm=39b5059b1bf7f9cb6cfa95f02fb2354efb746931edaec2e57d3ec59acd4acede&)

### No 5 Answer
Nano into /etc/bind/jarkom/abimanyu.i11.com
```
nano /etc/bind/jarkom/named.conf.local
```
Inside edit as follows
![filesoal5](https://cdn.discordapp.com/attachments/934661338934943774/1161978079963529256/image.png?ex=653a436a&is=6527ce6a&hm=870ef4b29d9de6ccb3239c9ed44ccd413d95b15637da6ba406cb6379080a7b0b&)
Copy file into jarkom directory
```
cp /etc/bind/db.local /etc/bind/jarkom/1.79.10.in-addr.arpa
```
Nano into the file and then edit the file as follows
```
nano /etc/bind/jarkom/1.79.10.in-addr.arpa
```
![filesoaledit5](https://cdn.discordapp.com/attachments/934661338934943774/1161980431718174800/image.png?ex=653a459b&is=6527d09b&hm=fedd6b1608a5b94f97d117f8011c6275efd10461b7862467a79044a93cd09c6b&)
Restart Bind
```
service bind9 restart
```
Go to other nodes and check if its working by using this code
```
host -t PTR 10.79.1.2
```
Result:
![check5](https://cdn.discordapp.com/attachments/934661338934943774/1161981849447440444/image.png?ex=653a46ed&is=6527d1ed&hm=a89260abd1dd6972aa551a6d9558ca213fb11c6fedc9334dfb52207ba3b684c7&)

### No 6 Answer
Edit named.conf.local as follows
```
nano /etc/bind/jarkom/named.conf.local
```
![file6](https://cdn.discordapp.com/attachments/934661338934943774/1161982804184285224/image.png?ex=653a47d1&is=6527d2d1&hm=f14a946f4ee9b462aa0868af0ab5f663a105a673aaeade1be188895f184b6b77&)
Restart Bind
```
service bind9 restart
```
Install bind9 in werkudara
```
apt-get update
```
```
apt get-install bind9 -y
```
Open named.conf.local in werkudara and edit as follows
![file6werk](https://cdn.discordapp.com/attachments/934661338934943774/1161983640989880341/image.png?ex=653a4898&is=6527d398&hm=3bce9db00c3a23ec76632066257d3f9005d925a5472580c1ae7bd95f76562815&)
Restart Bind in werkudara
```
service bind9 restart
```
Stop bind in yudhistira
```
service bind9 stop
```
![stop6](https://cdn.discordapp.com/attachments/934661338934943774/1161984360493363220/image.png?ex=653a4944&is=6527d444&hm=c3c65f5ea5e526dde1ec298bed088f18c6eb938241babff6aef5e3fb1361a53f&)<br>
Because the client to test is nakula, change the nameserver too <br>
![change6werk](https://cdn.discordapp.com/attachments/934661338934943774/1161984805802623086/image.png?ex=653a49ae&is=6527d4ae&hm=26373bb29c7f72177af11bcd0350d7a0f14c1419623d0b2397a7790e9b05c973&)<br>
Ping abimanyu from nakula <br>
![ping6](https://cdn.discordapp.com/attachments/934661338934943774/1161984820751118336/image.png?ex=653a49b1&is=6527d4b1&hm=f63c72816f1ef1c236a80620424894cd2279805954a155914e4061c878a1f73a&)
