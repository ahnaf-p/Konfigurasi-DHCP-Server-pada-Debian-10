# Konfigurasi-DHCP-Server-pada-Debian-10
25 September 2025  

# DHCP Server
  DHCP (Dynamic Host Configuration Protocol) Server adalah server yang otomatis memberikan alamat IP dan informasi jaringan ke client. Jadi, kita nggak perlu set IP satu per satu secara manual.  
    
# Langkah Konfigurasi  
  1. Pertama-tama kita perlu memastikan paket DHCP Server sudah tersedia di Debian. Caranya jalankan perintah:

         apt install isc-dhcp-server -y
![](IMAGES/)  
    Jika muncul pesan *isc-dhcp-server is already the newest version*, berarti DHCP Server sudah terpasang dengan versi paling baru, jadi kita bisa langsung lanjut ke tahap konfigurasi.  
      
  2. Setelah DHCP Server berhasil install, kita perlu menambahkan Static IP. Hal ini bertujuan agar server selalu punya identitas jaringan tetap dan bisa menjadi pusat pembagian IP ke client. Untuk mengkonfigurasinya kita bisa menjalankan,  

    nano /etc/network/interfaces
  Lalu isi seperti berikut.  
![](IMAGES/)  
  Jangan lupa save dengan **CTRL + X lalu Y dan Enter**.  
    
  3. Jika sudah melakukan konfigurasi IP, jangan lupa restart network servicenya agar perubahan diterapkan, caranya kita bisa menggunakan,  
    
    systemctl restart networking
  Kemudian, untuk memastikan apakah alamat IP benar apa belum, gunakan,  

    ip a
![](IMAGES/)  
  Hasilnya akan menampilkan daftar interface jaringan. Jika pada interface enp0s3 sudah muncul IP 192.168.22.1/24, artinya konfigurasi berhasil diterapkan.  
    
  4. Nah selanjutnya kita konfigurasi DHCP Servernya. Pertama buka dhcpd.conf dengan text editor.

    nano /etc/dhcp/dhcpd.conf
  Disini kita cukup cari **Slighty** saja, dan buka tanda pagar nya. Lalu konfigurasi seperti berikut ini.  
![](IMAGES/)  
  
  Jika konfigurasi sudah selesai, simpan dengan CTRL + X, Y lalu Enter.  
    
**Penjelasan:**
- subnet 192.168.22.0 netmask 255.255.255.0  
    Menentukan network yang digunakan. Di sini, network yang dipakai adalah 192.168.22.0 dengan netmask 255.255.255.0 (atau /24).  
- range 192.168.22.50-192.168.22.100  
    Menentukan rentang IP yang boleh dipinjam client. Jadi, client akan mendapatkan IP mulai dari 192.168.22.50 sampai 192.168.22.100.  
- option domain-name-servers penguin.xyz  
    Menetapkan DNS yang akan digunakan client.  
- option domain-name  
    Nama domain jaringan lokal.  
- option routers 192.168.22.1  
    Menentukan alamat gateway yang akan dipakai client untuk akses keluar jaringan.  
- option broadcast-address 192.168.22.255  
    Menentukan alamat broadcast pada jaringan.  
- default-lease-time 600  
    Lama waktu default client bisa menyewa IP sebelum harus meminta ulang. Nilai 600 detik sama dengan 10 menit.  
- max-lease-time 7200  
    Lama waktu maksimum sebuah client bisa mempertahankan IP sebelum harus diperpanjang. Nilai 7200 detik berarti 2 jam.
  
  5. 
