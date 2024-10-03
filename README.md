# Jarkom-Modul-2-IT10-2024

## Anggota Team:

| Nama | NRP                    |
|---------------|---------------------------------|
| Dani Wahyu Anak Ary    | 5027231038 |
| Abid Ubaidillah A      | 5027231089 |

### Soal Dan Pengerjaan:
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
3. Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.<br>
a.
```echo 'zone "pasopati.it10.com" {
    type master;
    notify yes;
    file "/etc/bind/jarkom/pasopati.it10.com";
};' >> /etc/bind/named.conf.local
```
b. 
```
cp /etc/bind/db.local /etc/bind/jarkom/pasopati.it10.com
```
c. 
```
echo '
;
; BIND data file for local loopback interface
;
$TTL    604000
@       IN      SOA     pasopati.it10.com. root.pasopati.it10.com. (
                        2023101001      ; Serial
                        604000         ; Refresh
                        06400         ; Retry
                        2419200         ; Expire
                        604000 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it10.com.
@       IN      A       192.238.2.7     ; IP Kotalingga
www     IN      CNAME   pasopati.it10.com.' > /etc/bind/jarkom/pasopati.it10.com
```
d. 
```
service bind9 restart
```
4. Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.<br>
a.
```
echo 'zone "rujapala.it10.com" {
    type master;
    notify yes;
    file "/etc/bind/jarkom/rujapala.it10.com";
};' >> /etc/bind/named.conf.local
```
b.
```
cp /etc/bind/db.local /etc/bind/jarkom/rujapala.it10.com
```
c.
```
echo '
;
; BIND data file for local loopback interface
;
$TTL    604000
@       IN      SOA     rujapala.it10.com. root.rujapala.it10.com. (
                        2023101001      ; Serial
                        604000         ; Refresh
                        06400         ; Retry
                        2419200         ; Expire
                        604000 )       ; Negative Cache TTL
;
@       IN      NS      rujapala.it10.com.
@       IN      A       192.238.3.3     ; IP Tanjungkulai
www     IN      CNAME   rujapala.it10.com.' > /etc/bind/jarkom/rujapala.it10.com
```
d.
```
service bind9 restart
```
5. Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.<br>
 a.
```
ping sudarsana.it10.com -c 4
```
b.
```
ping www.sudarsana.it10.com -c 4
```
c.
```
ping pasopati.it10.com -c 4
```
d.
```
ping www.pasopati.it10.com -c 4
```
6. Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).<br>
Untuk script.sh:<br>
a.
```
echo 'zone "2.238.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/2.238.192.in-addr.arpa";
};' >> /etc/bind/named.conf.local
```
b.
```
mkdir -p /etc/bind/jarkom
```
c.
```
cp /etc/bind/db.local /etc/bind/jarkom/2.238.192.in-addr.arpa
```
d.
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it10.com. root.pasopati.it10.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.238.192.in-addr.arpa.   IN      NS      pasopati.it10.com.
7                       IN      PTR     pasopati.it10.com.
' > /etc/bind/jarkom/2.238.192.in-addr.arpa
```
e. 
```
service bind9 restart
```
Untuk testing.sh:<br>
a. 
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```
b.
```
apt-get update
apt-get install dnsutils
```
c. 
```
echo nameserver 192.238.2.5 > /etc/resolv.conf
```
7. Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.<br>
Untuk Majapahit.sh:<br>
a.
```echo 'zone "sudarsana.it10.com" {
    type slave;
    masters { 192.238.2.5; }; 
    file "/var/lib/bind/sudarsana.it10.com";
};
```
b. 
```
zone "pasopati.it10.com" {
    type slave;
    masters { 192.238.2.5; }; 
    file "/var/lib/bind/pasopati.it10.com";
};
```
c. 
```
zone "rujapala.it10.com" {
    type slave;
    masters { 192.238.2.5; }; 
    file "/var/lib/bind/rujapala.it10.com";
};'  > /etc/bind/named.conf.local
```
d. Pastikan untuk restart kembali setelah memasukkan config.<br>
Untuk Sriwijaya.sh:<br>
a.
```
echo 'zone "sudarsana.it10.com" {
        type master;
        file "/etc/bind/jarkom/sudarsana.it10.com";
        allow-transfer { 192.238.3.2; };
        also-notify { 192.238.3.2; };
};' > /etc/bind/named.conf.local
```
b. 
```
echo 'zone "pasopati.it10.com" {
        type master;
        file "/etc/bind/jarkom/pasopati.it10.com";
        also-notify { 192.238.3.2; };
        allow-transfer { 192.238.3.2; };

};' >> /etc/bind/named.conf.local
```
c. 
```
echo 'zone "rujapala.it10.com" {
        type master;
        file "/etc/bind/jarkom/rujapala.it10.com";
        also-notify { 192.238.3.2; };
        allow-transfer { 192.238.3.2; }; 
   
};' >>/etc/bind/named.conf.local
```
d. Pastikan untuk restart kembali setelah memasukkan config.
8. Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.<br>
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it10.com. root.sudarsana.it10.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it10.com.
@       IN      A       192.238.1.3
@       IN      AAAA    ::1
www     IN      CNAME   sudarsana.it10.com.
cakra   IN      A       192.238.3.4
```
  
9. Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.<br>
a.
```
echo "
options {
        directory \"/var/cache/bind\";
        allow-query{any;};
        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
" > /etc/bind/named.conf.options
```
b. 
```
echo '

zone "panah.pasopati.it10.com"{
        type master;
        file "/etc/bind/panah/panah.pasopati.it10.com";
};
'>> /etc/bind/named.conf.local
```
c.
```
mkdir /etc/bind/panah
```
d. 
```
echo "
\$TTL    604800
@       IN      SOA     panah.pasopati.it10.com. root.panah.pasopati.it10.com. (
                        2021100401      ; Serial
                        604800         ; Refresh
                        86400         ; Retry
                        2419200         ; Expire
                        604800 )       ; Negative Cache TTL
;
@               IN      NS      panah.pasopati.it10.com.
@               IN      A       192.238.2.7       ;
www             IN      CNAME   panah.pasopati.it10.com.
" > /etc/bind/panah/panah.pasopati.it10.com
```
e. 
```
service bind9 restart
```
Untuk sriwijaya.sh:<br>
a. 
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it10.com. root.pasopati.it10.com. (
                        2023101001      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it10.com.
@       IN      A       10.72.1.4
www     IN      CNAME   pasopati.it10.com.
ns1     IN      A       10.72.2.3     ; IP georgopol
panah   IN      NS      ns1' > /etc/bind/jarkom/pasopati.it10.com
```
b. 
```
echo "options {
    directory \"/var/cache/bind\";

    // If there is a firewall between you and nameservers you want
    // to talk to, you may need to fix the firewall to allow multiple
    // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

    // If your ISP provided one or more IP addresses for stable
    // nameservers, you probably want to use them as forwarders.
    // Uncomment the following block, and insert the addresses replacing
    // the all-0's placeholder.  
    // };

    //========================================================================
    // If BIND logs error messages about the root key being expired,
    // you will need to update your keys.  See https://www.isc.org/bind-keys
    //========================================================================
    //dnssec-validation auto;

    allow-query { any; };
    auth-nxdomain no;
    listen-on-v6 { any; };
};" > /etc/bind/named.conf.options
```
c. 
```
service bind9 restart
```
10. Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.<br>
a.
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     panah.pasopati.it10.com. root.panah.pasopati.it10.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      panah.pasopati.it10.com.
@       IN      A       192.238.2.7
@       IN      AAAA    ::1
www     IN      CNAME   panah.pasopati.it10.com.
log     IN      A       192.238.2.7
www.log IN      CNAME   panah.pasopati.it10.com.
```
Pastikan Restart setelah memasukkan konfig

