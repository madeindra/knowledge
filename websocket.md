# Websocket

Websocket is a protokol komunikasi yang memungkinkan terjadinya komunikasi 2-arah _\(full-duplex\)_, seperti ketika kita berbicara menggunakan telepon.

### 

### Kenapa Harus Websocket?

Protokol komunikasi yang sering kita gunakan adalah HTTP. Setiap mengakses website, kita menggunakan HTTP atau HTTPS \(versi yang lebih aman\).

Tapi kenapa tidak menggunakan HTTP untuk komunikasi 2-arah?

Komunikasi pada HTTP memang terjadi antara 2 pihak, namun komunikasi ini hanya terjadi 1-arah _\(half-duplex\)_.

Misalnya, kita yang ingin mengakses website sebagai _client_ dan penyedia website sebagai _server, ****_sebelum _client_ mendapatkan konten website, _client_ mengirim permintaan lewat _browser_ , ketika permintaan tersebut sampai di _server,_ barulah _server_ mengirim balasan permintaan kita, setelah permintaan kita dibalas, sambungan tersebut akan diakhiri.

Artinya, komunikasi hanya terjadi 1-arah, _server_ tidak bisa menjawab bersamaan dengan saat _client_ sedang mengirim permintaan.

Berbeda dengan komunikais Websocket, ketika sambungan sudah terjadi_,_ kedua pihak bisa saling mengirim data tanpa harus menunggu pihak lain selesai. 

### \*\*\*\*

### **Contoh Penggunaan Websokcet**

Websocket sering digunakan dalam aplikasi _chatting_. 

