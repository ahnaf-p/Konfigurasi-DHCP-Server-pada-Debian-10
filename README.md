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
