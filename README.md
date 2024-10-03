# Jarkom-Modul-2-IT10-2024

## Anggota Team:

| Nama | NRP                    |
|---------------|---------------------------------|
| Dani Wahyu Anak Ary    | 5027231038 |
| Abid Ubaidillah A      | 5027231089 |

### Soal:
1. Sebuah kerajaan besar di Indonesia sedang mengalami pertempuran dengan penjajah. Kerajaan tersebut adalah Sriwijaya. Karena merasa terdesak Sriwijaya meminta bantuan pada Majapahit untuk mempertahankan wilayahnya. Pertempuran besar tersebut berada di Nusantara. Untuk topologi lihat pada link ini.
Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave.

![image](https://github.com/user-attachments/assets/34bd368b-60ad-422e-b077-a110f6ced104)


2. Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.<br>
a.
```
echo 'zone "sudarsana.it10.com" {
    type master;
    notify yes;
    file "/etc/bind/jarkom/sudarsana.it10.com";
};' > /etc/bind/named.conf.local
``` 
b.
```
mkdir /etc/bind/jarkom
```
c.
```
cp /etc/bind/db.local /etc/bind/jarkom/sudarsana.it10.com
```
d.
```
echo '
;
; BIND data file for local loopback interface
;
$TTL    604000
@       IN      SOA     sudarsana.it10.com. root.sudarsana.it10.com. (
                        2023101001      ; Serial
                        604000         ; Refresh
                        06400         ; Retry
                        2419200         ; Expire
                        604000 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it10.com.
@       IN      A       192.238.1.3     ; IP Solok
www     IN      CNAME   sudarsana.it10.com.' > /etc/bind/jarkom/sudarsana.it10.com
```
e.
```
service bind9 restart
```
3. Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.

4. Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.

5. Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.
 
7. Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).
 
8. Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.
 
9. Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.
  
10. Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.
    
11. Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.

