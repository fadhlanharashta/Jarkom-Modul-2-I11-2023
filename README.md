# Jarkom-Modul-2-I11-2023
Muhammad Fadhlan Ashila Harashta <br>
Hanifi Abrar Setiawan <br>
I Putu Arya Prawira Wiwekananda <br>

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


