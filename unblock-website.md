# Unblock Website

### Metode Host File

Buka hosts file

* Lokasi Host File di Windows

```text
%WinDir%\System32\Drivers\Etc\Hosts
```

* Lokasi Host File di Linux / MacOS

```text
/etc/hosts
```

Masukkan alamat ip & website di baris terbawah untuk membuka block website tersebut, contohnya sebagai berikut:

```text
185.199.108.153 madecanggih.dev www.madecanggih.dev
185.199.109.153 madecanggih.dev www.madecanggih.dev
185.199.110.153 madecanggih.dev www.madecanggih.dev
185.199.111.153 madecanggih.dev www.madecanggih.dev
```

Simpan perubahan hosts tersebut.

### Cara Mengetahui Alamat IP

Gunakan [Google DNS \(dns.google.com\)](https://dns.google.com/), masukkan alamat, misalnya `madecanggih.dev` kemudian klik `Resolve` , akan muncul beberapa Alamat IP dalam format `angka.angka.angka.angka` 

Cara lain dengan menggunakan terminal / command prompt jalankan perintah berikut, dan Alamat IP akan muncul setelahnya 

```text
ping madecanggih.dev
```

