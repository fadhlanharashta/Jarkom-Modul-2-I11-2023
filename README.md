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
8. Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.<br>
9. Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.<br>
10. Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh: Prabukusuma:8001, Abimanyu:8002, Wisanggeni:8003.<br>
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
### No 7 Answer
Nano into /etc/bind/jarkom/abimanyu.i11.com
```
nano /etc/bind/jarkom/abimanyu.i11.com
```
Edit as follows
![file7](https://cdn.discordapp.com/attachments/934661338934943774/1161987079744536597/image.png?ex=653a4bcc&is=6527d6cc&hm=30e71e9c11344dc36f193f55a83994dec053a082ad668617a4f232f6fccf6789&)<br>
Edit the /etc/bind/named.conf.options as follows
![fileedit7](https://cdn.discordapp.com/attachments/934661338934943774/1161987559707123833/image.png?ex=653a4c3e&is=6527d73e&hm=e1bd4b01ae9ee0e16df860a7631ea9ef886e704aa60a95153d8b10d7d4487345&)<br>
Then edit the named.conf.local in yudhistira as follows
![fileedit7-2](https://cdn.discordapp.com/attachments/934661338934943774/1161987934992486510/image.png?ex=653a4c98&is=6527d798&hm=3cc2b48541e9725ef54f563ce7873d74b2a76d62095b1990fe776c2aad9b44ab&)<br>
Restart Bind
```
service bind9 restart
```
Go to werkudara and Edit the /etc/bind/named.conf.options as follows
```
nano /etc/bind/named.conf.options
```
![fileeditwerk7](https://cdn.discordapp.com/attachments/934661338934943774/1161988419489116230/image.png?ex=653a4d0b&is=6527d80b&hm=97c449a3e76f6bebbbfbb8ac9c2f76c693a8c00c6bf2befc023f10c311b404a3&)<br>
Edit the named.conf.local in werkudara
![fileeditwerk7-2](https://cdn.discordapp.com/attachments/934661338934943774/1161988743247433828/image.png?ex=653a4d59&is=6527d859&hm=955964f529c85b34646f22aa21ed3cb87c630b023ad9dfe487ec0ffbb1dc6949&)<br>
Then copy the db_local to delegasi folder
```
cp /etc/bind/db.local /etc/bind/delegasi/baratayuda.abimanyu.i11.com
```
Edit the file /etc/bind/delegasi/baratayuda.abimanyu.i11.com
```
nano /etc/bind/delegasi/baratayuda.abimanyu.i11.com
```
![fileeditabimanyu7](https://cdn.discordapp.com/attachments/934661338934943774/1161989818067197972/image.png?ex=653a4e59&is=6527d959&hm=481ec2d895aa4c3a20543b186775421f84bd0fee658e8ca77c20341dfbc7e144&)<br>
Restart Bind and then test it
```
service bind9 restart
```
![fileeditabimanyu7](https://cdn.discordapp.com/attachments/934661338934943774/1161990010644471848/image.png?ex=653a4e87&is=6527d987&hm=797b03f3177696d384d793d31c2570cdf2949026d385d972006951ad38482c00&)<br>
### No 8 Answer
Change the file /etc/bind/delegasi/baratayuda.abimanyu.i11.com in werkudara
```
/etc/bind/delegasi/baratayuda.abimanyu.i11.com
```
![file8](https://cdn.discordapp.com/attachments/827014097219878982/1163800964164227153/image.png?ex=6540e51c&is=652e701c&hm=ba6f3ff09b5901a588d530926db666709c6364d3cba5ed32a779060f257a223c&)<br>
Restart the bind Go test in Nakula <br>
![check5](https://cdn.discordapp.com/attachments/827014097219878982/1163801012163850271/image.png?ex=6540e527&is=652e7027&hm=c3948cb90d4c3b05f662865d36297e57fe5deb0dd6e1b4d427a7b77018d519a6&)<br>
### No 9 Answer
Configuring the three nginx worker
```
apt-get update
apt install nginx php php-fpm
php -v
```
![file9](https://cdn.discordapp.com/attachments/827014097219878982/1163802194055794810/image.png?ex=6540e641&is=652e7141&hm=c9363d5bfc01e5074fc4040fa3c73f1d96ad3f81f4d014a351f4906887b5b111&)<br>
Make a new folder called jarkom (do this to all worker) <br>
![filefolder9](https://cdn.discordapp.com/attachments/827014097219878982/1163802665013231626/image.png?ex=6540e6b1&is=652e71b1&hm=ba4d933a8d748c4dc673799781f210c5f85f2b81248ca977d1603d674cb0b02b&)<br>
Edit a file in the folder named index php (each node is different (optional)), Wisangemi (an example) <br>
![fileedit9](https://cdn.discordapp.com/attachments/827014097219878982/1163803142476017714/image.png?ex=6540e723&is=652e7223&hm=4fd9714bd0904220ebe8329dcb8741b74eec294fc3b5e10f94db772efb7e74a5&)<br>
Edit the /etc/nginx/sites-available/jarkom
```
/etc/nginx/sites-available/jarkom
```
![fileedit9-2](https://cdn.discordapp.com/attachments/827014097219878982/1163803474442584064/image.png?ex=6540e772&is=652e7272&hm=a3e04077db2a2c986d4c23c524097ba60f192c4ca42114ee609bcb5f41b91994&)<br>
![fileedit9-3](https://cdn.discordapp.com/attachments/827014097219878982/1163803561239511101/image.png?ex=6540e787&is=652e7287&hm=d35527e4e7ea983f779207c26dd140ee5043f3a167e91d8c3f2242ba37085d42&)<br>
Do <br>
![filedo9](https://cdn.discordapp.com/attachments/827014097219878982/1163804488512045086/image.png?ex=6540e864&is=652e7364&hm=ed784012fc09e7da07dd1a6617622f5dd2898d0acd52802100c7b50fa9f4ee58&)<br>
Then test the nginx <br>
```
nginx -t
```
![filetest9](https://cdn.discordapp.com/attachments/827014097219878982/1163804520950800474/image.png?ex=6540e86c&is=652e736c&hm=9420eb30160c5199f207f04b6cc05d1d844f62bec00d1d04f7d3dc1041a98777&)<br>
### No 10 Answer
Using the Round Robin algorithm for arjuna.i11.com (Haven't finished)<br>
install bind and nginx in arjuna<br>
```
nano /etc/bind/named.conf.local
```
![file10](https://cdn.discordapp.com/attachments/827014097219878982/1163805910049759242/image.png?ex=6540e9b7&is=652e74b7&hm=8144313f73f14fd1625492ec257cc0b3679cc8b842bde078c76eb87ad7e13025&)<br>
Edit /etc/bind/jarkom/arjuna.i11.com
```
nano /etc/bind/jarkom/arjuna.i11.com
```
![file10-2](https://cdn.discordapp.com/attachments/827014097219878982/1163805938847842334/image.png?ex=6540e9be&is=652e74be&hm=f2d479f6e85164f55ebbe4c47e004b75d6a9347d93654cfa3ecc7c2261f2a992&)<br>
Edit file /etc/bind/jarkom/3.79.10.in-addr.arpa
```
nano /etc/bind/jarkom/3.79.10.in-addr.arpa
```
![file10-3](https://cdn.discordapp.com/attachments/827014097219878982/1163807935936344095/image.png?ex=6540eb9a&is=652e769a&hm=832b4cc053f522954f75dda0ce90c990c4e43d433ac9d0d2a0a22d911af36c6e&)<br>
Test the domain <br>
![filetest10](https://cdn.discordapp.com/attachments/827014097219878982/1163805994657251348/image.png?ex=6540e9cb&is=652e74cb&hm=19ebf521036c1b6a026b9dbe7c6df0c55ffef5443a9274d1f611bfb712ecbb37&)<br>
Back to Arjuna <br>
Make a new file in /etc/nginx/sites-available with the name of lb-jarkom then edit it <br>
```
nano /etc/nginx/sites-available/lb-jarkom
```
![check10](https://cdn.discordapp.com/attachments/827014097219878982/1163809659849809931/image.png?ex=6540ed35&is=652e7835&hm=9456a60530e3f1ce8831edc92c77da986a409400e3670a6c2fd212b05cb40cc5&)<br>
Write this command <br>
```
In -s /etc/nginx/sites-available/lb-jarkom /etc/nginx/sites-enabled
```
![restart10](https://cdn.discordapp.com/attachments/827014097219878982/1163809227467399178/image.png?ex=6540ecce&is=652e77ce&hm=b447d456221378926a76774c1ef1766c94d1ab934d12565dddc4444fc47ed894&)<br>
Then restart the nginx and bind <br>
```
lynx https://arjuna.i11.com
```
![restartfile10](https://cdn.discordapp.com/attachments/827014097219878982/1163809280990908576/image.png?ex=6540ecdb&is=652e77db&hm=b5e53000afc3d7936d351636ba4f13df5f35afaa976171176f747c7a72851817&)<br>
![file10-4](827014097219878982/1163810566549274707/image.png?ex=6540ee0d&is=652e790d&hm=81b6343fcdd3fcde887e035562ed44fe288430b06e59f16664cb25a270c9ce35&)<br>
