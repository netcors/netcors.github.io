---
layout: post
title: "Setup IP Cloud di Mikrotik"
date: 2019-10-23 02:14
comments: true
categories: [Mikrotik]
author: mukti
---

MikroTik menawarkan beberapa layanan untuk perangkat RouterBOARD di atas RouterOS v6.14 yaitu salah satunya Cloud DDNS (Dynamic DNS). 
Layanan ini berfungsi untuk mempermudah akses saat mengkonfigurasi, mengatur, mengontrol, memelihara atau memantau perangkat MikroTik kamu.

> Note: RouterOS v6.27 ke atas untuk command "ip cloud enabled" diubah menjadi "ip cloud ddns-enabled" ini mungkin memerlukan beberapa perubahan pada script jika kamu menggunakan fitur ini dalam sebuah script.

> Note: RouterOS v6.43 ke atas akan menggunakan cloud2.mikrotik.com untuk berkomunikasi dengan server Cloud MikroTik. Versi yang lebih lama akan menggunakan cloud.mikrotik.com untuk berkomunikasi dengan server Cloud MikroTik.

> Note: IP/Cloud memerlukan lisensi Cloud Hosted Router (CHR).

## DDNS (Dynamic DNS)

adalah layanan yang memperbarui IPv4 address untuk record A dan IPv6 address untuk record AAAA secara berkala. 
Layanan seperti ini sangat berguna ketika ISP kamu telah memberikan IP address dinamis yang berubah secara berkala, tetapi kamu selalu membutuhkan IP address yang dapat digunakan untuk menghubungkan ke perangkat MikroTik dari jarak jauh. 
Di bawah ini kamu dapat menemukan detail operasi yang relevan dengan layanan DDNS IP/Cloud:

- Memeriksa perubahan outgoing IP address: setiap 60 detik
- Menunggu respons server Cloud MikroTik: 15 detik
- Record DDNS TTL: 60 detik
- Mengirim paket terenkripsi ke cloud.mikrotik.com atau cloud2.mikrotik.com menggunakan port UDP/15252

### Enable service DDNS / Cloud MikroTik

```
/ip cloud set ddns-enabled=yes
/ip cloud print

# Output
         ddns-enabled: yes
 ddns-update-interval: none
          update-time: yes
       public-address: 149.148.147.199
  public-address-ipv6: 2620:0:2d0:200::7
             dns-name: 527c049co125.sn.mynetname.net
               status: updated
```

> Note: Saat service diaktifkan, DNS name akan disimpan di server Cloud MikroTik secara permanen dan DNS name ini akan menyesuaikan dengan IP terakhir yang telah dikirim ke server Cloud MikroTik.

### Disable service DDNS / Cloud MikroTik

```
/ip cloud set ddns-enabled=no
```

> Note: Segera setelah kamu menonaktifkan service, perangkat kamu mengirim perintah ke server Cloud MikroTik untuk menghapus DNS name yang tersimpan.