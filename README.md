# Jarkom-Modul-2-F12-2022

Nama Anggota | NRP
------------------- | --------------
Hesekiel Nainggolan | 5025201054
Khuria Khusna | 5025201053
Afiq Akram | 5025201270

1. Semua node terhubung pada router Ostania, sehingga dapat mengakses internet (1). 
## Jawaban Soal 1 
---
Pertama-tama kami membuat sebuah node yang terhubung dengan internet dengan nama NAT1. Node tersebut kemudian disambungkan dengan router Ostania melalui interface `nat0` menuju interface `eth0`. Selanjutnya konfigurasi IP router Ostania seperti gambar berikut:

![Foto](./img2/img2/no1b.PNG)
<br>

kemudian membuat topologi sesuai dengan apa yang diminta oleh soal :

![Foto](./img2/img2/no1a.PNG)
<br>

Kemudian setting network dari masing-masing node ubuntu dengan fitur Edit network configuration. IP yang dipakai ialah IP Prefix dari kelompok: `10.35`
setelah itu kita buat dalam node `/root/.bashrc` command `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 10.46.0.0/16` dan kita atur juga pada node yang lain dalam node `/root/.bashrc/` dengan command `echo 'nameserver 192.168.122.1' > /etc/resolv.conf` agar setiap kita menutup dan membuka kembali project kita, kita tidak perlu lagi untuk mengetik hal tersebut dalam console.
setelah itu kita akan coba untuk memastikan apakah node-nodenya bisa mengakses internet :

![Foto](./img2/img2/no1c.PNG)
<br>

2. Untuk mempermudah mendapatkan informasi mengenai misi dari Handler, bantulah Loid membuat website utama dengan akses wise.yyy.com dengan alias www.wise.yyy.com pada folder wise.
## Jawaban Soal 2 
---
Hal pertama yang harus dilakukan ialah membuat script untuk menyimpan setting konfigurasi pada `/etc/bind/named.conf.local` yang dilakukan dalam script untuk pembuatan zone baru yang berisi `nama zone`, `type nya`, dan `lokasi konfigurasi db localnya`. Detilnya seperti gambar berikut:

![Foto](./img2/img2/no2a.PNG)
<br>

Lalu kami membuat sebuah script untuk mengcreate directory baru `wise`, mengcopy script yang berisikan pembuatan zone kedalam directory `/etc/bind/named.conf.local`, serta berisi `service bind9 restart` yang mana akan menyimpan konfigurasi db local yang bernama `wise`.

![Foto](./img2/img2/no2c.PNG)
<br>

Selanjutnya kami melakukan membuat suatu script untuk melakukan perubahan local host, serta membuat alias dengan `www` :

![Foto](./img2/img2/no2d.PNG)
<br>

kemudian untuk melakukan pengecekan apakah berhasil atau tidak, maka bisa dicek pada node client `Garden` :

![Foto](./img2/img2/no2e.PNG)
<br>

3. Setelah itu ia juga ingin membuat subdomain eden.wise.yyy.com dengan alias www.eden.wise.yyy.com yang diatur DNS-nya di WISE dan mengarah ke Eden.
## Jawaban Soal 3
---
Hal pertama yang kita lakukan ialah membuat membuat script untuk menyimpan setting konfigurasi pada `/etc/bind/named.conf.local` yang dilakukan dalam script untuk pembuatan zone baru yang berisi `nama zone`, `type nya`, dan `lokasi konfigurasi db localnya`. Detilnya seperti gambar berikut:

![Foto](./img2/img2/no3a.PNG)
<br>

Lalu kami membuat sebuah script untuk mengcreate directory baru dengan nama `wise` , mengcopy script yang berisikan pembuatan zone kedalam directory `/etc/bind/named.conf.local`, serta berisi `service bind9 restart` yang mana akan menyimpan konfigurasi db local yang bernama `wise`.

![Foto](./img2/img2/no3b.PNG)
<br>

Selanjutnya kami melakukan membuat suatu script untuk melakukan perubahan local host, serta membuat alias dengan `www` :

![Foto](./img2/img2/no3c.PNG)
<br>

kemudian untuk melakukan pengecekan apakah berhasil atau tidak, maka bisa dicek pada node client `Garden` :

![Foto](./img2/img2/no3d.PNG)
<br>

4. Buat juga reverse domain untuk domain utama.
## Jawaban Soal 4
---
Dalam menyelesaikan pembuatan reverse dns `(Record PTR)` kami pertama-tama menginisialisasi sebuah zone baru pada scrpt `/etc/bind/wise/2.35.10.in-addr.arpa` dengan detil sebagai berikut:

![Foto](./img2/img2/no4a.PNG)
<br>

Kemudian buat suatu script yang mengatur konfigurasi `db.local` pada `reverse dns`dengan menambahkan dua hal ini:<br>
`2.35.10.in-addr.arpa.       IN      NS      wise.F13.com.`<br>
`2       IN      PTR       wise.F13.com.` 

![Foto](./img2/img2/no4b.PNG)
<br>

kemudian untuk melakukan pengecekan apakah berhasil atau tidak, maka bisa dicek pada node client `SSS` :

![Foto](./img2/img2/no4c.PNG)
<br>

5. Agar dapat tetap dihubungi jika server WISE bermasalah, buatlah juga Berlint sebagai DNS Slave untuk domain utama.
## Jawaban Soal 5
---
Pertama kita harus ke  **Wise** dahulu dimana kita menambahkan `notify, also-notify  (dengan Berlint [10.35.3.2]) dan allow-transfer (dengan Berlint [10.46.3.2])`  di folder wise pada `/etc/bind/named.conf.local`

![Foto](./img2/img2/no5a.PNG)
<br>

Selanjutnya kita ke  **Berlint**  dimana kita menkonfigurasi zone Dns Slavenya di `/etc/bind/named.conf.local` dengan type slave dan memasukan IP yang menjadi masternya yaitu IP Wise `[10.35.2.2]` lalu kita lakukan restart ` service bind9 restart`

![Foto](./img2/img2/no5b.PNG)
<br>

lalu kita lakukan ping di `Garden` untuk mengetes dns slavenya berhasil atau tidak dengan mengetik `ping wise.F13.com`

![Foto](./img2/img2/no5c.PNG)
<br>

6. Karena banyak informasi dari Handler, buatlah subdomain yang khusus untuk operation yaitu operation.wise.yyy.com dengan alias `www.operation.wise.yyy.com` yang didelegasikan dari WISE ke Berlint dengan IP menuju ke Eden dalam folder operation.
## Jawaban Soal 6
---
Hal pertama yang harus dilakukan ialah membuat script untuk menyimpan setting konfigurasi pada `/etc/bind/named.conf.local` yang dilakukan dalam script untuk pembuatan zone baru yang berisi `nama zone`, `type nya`, dan `lokasi konfigurasi db localnya`. Detilnya seperti gambar berikut:

![Foto](./img2/img2/no6a.PNG)
<br>

Lalu kami membuat sebuah script untuk mengcreate directory baru `operation`, mengcopy script yang berisikan pembuatan zone kedalam directory `/etc/bind/named.conf.local`, serta berisi `service bind9 restart` yang mana akan menyimpan konfigurasi db local yang bernama `operation`.

![Foto](./img2/img2/no6b.PNG)
<br>

Selanjutnya kami melakukan membuat suatu script untuk melakukan perubahan local host, serta membuat alias dengan `www` :

![Foto](./img2/img2/no6b.PNG)
<br>

Selanjutnya kita ke **Berlint** dimana kita menkonfigurasikan pada `etc/bind/named.conf.options`

![Foto](./img2/img2/no6c.PNG)
<br>

kemudian untuk melakukan pengecekan apakah berhasil atau tidak, maka bisa dicek pada node client `SSS` :

![Foto](./img2/img2/no6d.PNG)
<br>

7. Untuk informasi yang lebih spesifik mengenai Operation Strix, buatlah subdomain melalui Berlint dengan akses `strix.operation.wise.yyy.com` dengan alias `www.strix.operation.wise.yyy.com` yang mengarah ke Eden
## Jawaban Soal 6
---
Hal pertama yang harus dilakukan ialah membuat script untuk menyimpan setting konfigurasi pada `/etc/bind/named.conf.local` yang dilakukan dalam script untuk pembuatan zone baru yang berisi `nama zone`, `type nya`, dan `lokasi konfigurasi db localnya`. Detilnya seperti gambar berikut:

![Foto](./img2/img2/no7a.PNG)
<br>

Lalu kami membuat sebuah script untuk mengcreate directory baru `operation`, mengcopy script yang berisikan pembuatan zone kedalam directory `/etc/bind/named.conf.local`, serta berisi `service bind9 restart` yang mana akan menyimpan konfigurasi db local yang bernama `operation`.

![Foto](./img2/img2/no7c.PNG)
<br>

Selanjutnya kami melakukan membuat suatu script untuk melakukan perubahan local host:

![Foto](./img2/img2/no7b.PNG)
<br>


kemudian untuk melakukan pengecekan apakah berhasil atau tidak, maka bisa dicek pada node client `SSS` :

![Foto](./img2/img2/no7d.PNG)
<br>
