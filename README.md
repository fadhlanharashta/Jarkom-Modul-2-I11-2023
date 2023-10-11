# Jarkom-Modul-2-I11-2023
Muhammad Fadhlan Ashila Harashta <br>
Hanifi Abrar Setiawan <br>
I Putu Arya Prawira Wiwekananda <br>

## Topology
![topology](https://cdn.discordapp.com/attachments/934661338934943774/1161561002656157757/image.png?ex=6538befb&is=652649fb&hm=d18b00fa523b6e04a21c2b27281f381c6d5e7380716ddc05d688f2562594d2b1&)
## Question
1. Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut <br>
2. Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.<br>
3. Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.<br>
4. Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.<br>
5. Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)<br>
6. Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.<br>
7. Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.<br>
