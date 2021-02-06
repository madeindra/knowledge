# HTTP Live Stream

HTTP Live Stream, atau yang biasa disingkat HLS.

Terkadang, ketika kita ingin mengunduh video yang kita tonton di internet, misalnya video kucing lucu yang ingin kita bagikan ke teman kita. Tapi sayangnya, tidak semua website meletakkan video di website mereka dalam format yang bisa diunduh, HLS adalah salah satunya.

#### 

#### Menggunakan Extension di Chrome

Untuk mengunduh video HLS, ada dua _extension_ di Chrome yang saya rekomendasikan:

* [HLS Downloader](https://github.com/puemos/hls-downloader-web-extension): Mengunduh video HLS dengan mudah dalam format `.ts`
* [Stream Recorder](https://www.hlsloader.com/): Tidak hanya mengunduh, bisa juga untuk merekam video HLS ke dalam format `.mp4`

#### 

#### Menggunakan youtube-dl

Selain dengan _extension_, kita juga bisa mengunduh dengan `youtube-dl`. Untungnya, program ini tidak hanya mendukung Youtube, seperti namanya, tapi juga banyak website lain. [Klik untuk mengunjungi _repository_ Github youtube-dl](https://github.com/ytdl-org/youtube-dl).

Misalnya kita menemukan video yang menarik di Youtube dan kita ingin mengunduhnya, cukup salin URL video tersebut, bentuknya seperti ini:

```text
https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

Kemudian kita bisa menggunakan _command_ ini untuk mengunduh video itu. 

```text
youtube-dl https://www.youtube.com/watch\?v=dQw4w9WgXcQ
```

Kalau dilihat, ada perbedaan pada URL nya, sebelum `?` terdapat `\` , ini disebut _escaping_. Karena tanpa melakukan _escaping_, program tidak bisa membaca URL dengan benar.



#### HLS Terenkripsi

HLS bisa dienkripsi, contohnya dengan `AES-128`. Untuk kasus ini, kita bisa mengunduh video menggunakan _extension_ HLS Downloader.

Terkadang video yang terenkripsi tidak bisa dimainkan. Untuk mengatasi ini, kita bisa merekam videonya dengan _extension_ Stream Recorder, tapi bisa jadi kualitas videonya sedikit berbeda dari kualitas aslinya. 

Tentu ada cara untuk melakukan dekripsi file `.ts` yang sudah diunduh, ikuti langkah berikut:

1. Unduh `ffmpeg`, [klik untuk m](https://ffmpeg.org/)engunjungi website.
2. Buka halaman yang memuat video dan cari file `m3u8` . Kita bisa memanfaatkan `View Source` atau buka _developer tool_ dan masuk ke bagian `Network` , ini berlaku untuk _browser_ Google Chrome.
3. Buka file `m3u8` dan cari bagian `EXT-X-KEY` . Disana akan tertulis `URI`, buka `URI` di dalam _browser_ dan kunci enkripsi akan terunduh secara otomatis, ubah file kunci enkripsi tersebut menjadi `enc.key` \(penamaan tidak harus sama\).
4. Dalam file `m3u8`, ubah `URI` pada bagian `EXT-X-KEY` menjadi `enc.key` \(atau nama lain yang digunakan di langkah sebelumnya\).
5. Dalam file `m3u8`, cari bagian `EXTINF` , terdapat nomor pada bagian ini. Nomor tersebut adalah durasi dari pecahan video. Jumlahkan seluruh durasi yang ada pada bagian `EXTINF` untuk mengetahui total durasi video.
6. Hapus semua bagian `EXTINF`  dan buat bagian `EXTINF` baru yang angkanya memuat total durasi video.
7. Di bawahnya, gunakan nama dari file `.ts` yang diunduh.
8. Letakkan file `.ts`, `.key`, dan `.m3u8` pada satu lokasi yang sama.
9. Coba mainkan file `m3u8` menggunakan _media player_ seperti VLC, kita sudah bisa memainkan video tersebut secara normal.
10. Untuk mengubah video menjadi mp4, jalankan _command_ `ffmpeg` berikut:

```text
ffmpeg -protocol_whitelist file,tls,tcp,https,crypto -allowed_extensions ALL -i name_of_file.m3u8 -c copy name_of_file.mp4
```

