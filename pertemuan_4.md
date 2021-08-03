# Belajar Bersama Flutter

Pertemuan 4, 5 Aug 2021


## Merangkum kembali apa yang telah dipelajari minggu lalu

Pada pertemuan minggu lalu kita telah berkenalan dengan Android Studio dan mengenal fungsi-fungsi penting, yang sering kita gunakan selama kita menulis kode aplikasi:
- berbagai daerah di layar
  - daerah sebelah kiri (terutama menemukan berkas kode)
  - daerah di bawah (di mana ditampakkan error dan pesan lainnya, termasuk terminal)
  - daerah di sebelah kanan
- icon-icon penting di barisan icon sebelah kanan atas
  - daftar emulator/hp (default <no devices selected>)
  - daftar nama berkas yang akan dijalankan kalau mengeksekusi Run
  - icon **Run** 
  - icon **Stop**
  - icon **AVD manager**

Hari ini kita maju selangkah lagi mengenal fungsi yang sangat menolong kala menulis kode:
- icon bola lampu, di mana terdapat jalan pintas ke berbagai widget dasar
- tanda posisi kesalahan (*error*) kalau ada di pinggir sebelah kanan
- tab **Problems** dan **Dart Analysis** di sebelah bawah

Selain itu kita juga telah mengenal anatomi sebuah aplikasi Android
- berkas utama **main.dart** dan **pubspec.yaml**
- blok kode yang merupakan pintu gerbang masuk ke aplikasi
- berbagai widget, yang dibongkar-pasang layaknya potongan-potongan lego
- widget-widget utama:
  - MaterialApp, yang menentukan desain/penampakkan aplikasi (warna, tombol, dlsb)
  - Scaffold, yang merupakan kerangka dasar aplikasi (bayangkanlah ini sebagai fondasi satu rumah yang sedang dibangun)
  - berbagai widget yang sering digunakan: Text, Image, Icon, Column, Row, dlsb.

Hari ini kita meneruskan memoles aplikasi Kartu Nama itu. Kalau kita cukup cepat, semoga selesai sehingga siap dan layak untuk dipamerkan/digunakan sebagaimana layaknya aplikasi lainnya di smartphone kita.

## Lanjutan introduksi ke Android Studio

Sebagai editor, Android Studio mempunyai berbagai alat yang menolong kita sebagai programmer dalam mengorganisir kode-kode kita. Kita elaborasi beberapa di antaranya di sini.

Pertama, icon bola lampu. Mari kita perhatikan apa yang tersedia di sana dan bagaimana menggunakannya. Jalan pintas yang terdaftar di sini sangat membantu, terutama untuk menghindari salah ketik kode. Perhatikan daftar widget yang ditampilkan di situ, itu adalah widget yang paling sering kita butuhkan. Termasuk yang paling penting adalah **Remove this widget**

Kedua, perhatikan tanda posisi kesalahan di pinggir sebelah kanan. Pesan di situ sangat menolong mengetahui sebab kesalahan dan bagaimana mengatasinya.

Ketiga, tab **Problems** dan **Dart Analysis** di sebelah bawah. Fungsinya mirip dengan yang sebelumnya, tetapi di sini daftarnya lebih panjang, jadi lebih membantu. Dalam banyak hal pesannya sangat jelas dan karena itu membantu dalam pemecahan masalah atau penyempurnaan kode aplikasi.

## Meneruskan pembuatan aplikasi Kartu Nama (Bongkar-pasang berbagai widget)

Kita ingat titik tolak aplikasi ini adalah menampilkan satu pesan teks ke layar. Tetapi kita ingin menampilkan bukan hanya satu pesan teks, melainkan beberapa dan juga ingin menampilkan foto/gambar.

Untuk itu widget yang telah ada, yakni Center tidak memadai untuk menampung berbagai widget lainnya.

Seperti kita sudah berkenalan kali lalu, widget ada yang single seperti widget **Text** (tidak memiliki widget lain sebagai anak), ada pula widget seperti **Center** yang memiliki satu widget lain sebagai anak, tetapi *hanya satu*, dan ada widget lainnya seperti **Column** yang memiliki *banyak* widget lainnya sebagai anak.

Kemudian kita juga sudah mengenal prinsip penempatan berbagai elemen widget di layar, yakni dengan menggunakan sistem baris (*row*) dan kolom (*column*). Semua apa yang tampil di layar yang bisa dilihat pengguna di susun berdasarkan sistem ini. Dan untuk membantu dalam penempatan berbagai elemen ini ada beberapa widget yang cocok untuk itu seperti widget **Row** dan widget **Column** yang terdapat dalam kategori **Layout**.

### Memasang foto lokal

1. Buat folder images di folder utama aplikasi di dalam Android Studio
2. Kopi foto yang diinginkan dari File Explorer Windows ke dalam folder images di Android Studio, mis. dengan nama foto_saya.jpg
3. Sunting berkas pubspec.yaml untuk memberitahu tentang adanya foto atau gambar dengan menambahkan baris berikut di bawah **flutter:** dan setelah **  uses-material-design: true**
```
   assets:
     - images/
```
4. Jalankan `flutter pub get` di Terminal atau klik **pub get** di pesan di sebelah kanan atas. Pastikan hasilnya sukses (Exit 0)
5. Buka berkas **main.dart** dan temukan lokasi gambar (kode `image: NetworkImage...` dst)
6. Ganti NetworkImage(...)  menjadi `AssetImage('images/foto_saya.jpg')`
7. Tambahkan properti berikut: `width: 150` untuk mengontrol ukuran foto.
8. Jalankan Android Emulator dan nikmati hasilnya.


### Membuat foto tampil bundar seperti layaknya foto profil

1. Ganti keseluruhan widget Image menjadi yang berikut
```
            CircleAvatar(
              radius: 75.0,
              backgroundImage: AssetImage('images/foto_saya.jpg'),
            ),
```
2. Stop dulu aplikasi dengan menekan icon **Stop** (icon kotak merah di barisan icon sebelah kanan atas)
3. Klik icon **Run**
4. Nikmati tampilan baru foto Anda.

### Mengubah ukuran teks nama Anda

1. Tambahkan kode berikut di dalam badan widget Text setelah teks (dan pastikan ada koma pemisah): `style: TextStyle(fontSize: 36.0, color: Colors.blue, fontWeight: FontWeight.bold)`
2. Nikmati hasilnya.


### Menambah icon telepon di depan nomor telepon

Hal ini membutuhkan satu widget yang memungkinkan kita meposisikan dua widget dalam satu baris. Dan seperti telah kita pelajari di atas widget untuk itu adalah **Row**

1. Melalui fungsi bola lampu, apit widget **Text** dengan widget **Row**
2. Sebelum widget **Text** sisipkan widget **Icon** dengan menuliskan kode berikut `Icon(Icons.phone, color: Colors.blue),` (perhatikan tanda koma di akhir widget Icon, yang memisahkannya dari widget berikutnya!
3. Jalankan dan lihat hasilnya? Ada yang aneh?
4. Kalau mau supaya di tempatkan di tengah tambahkan kode berikut `mainAxisAlignment: MainAxisAlignment.center,` sebelum properti **children**.
5. Kalau mau supaya ada jarak antara icon dan nomor telepon, sisipkan widget berikut di antara keduanya `SizedBox(width: 12.0),`
6. Nikmati aplikasi Kartu Nama Anda!


### Opsional: Menukar warna latar

1. Tentukan warna latar apa mau digunakan. Katakanlah misalnya orange.
2. Tambahkan kode berikut di Scaffold: `backgroundColor: Colors.orange,`


### Rencana untuk sesi berikutnya

Pada kelas minggu depan, kita memoles lagi kartu nama ini sehingga benar-benar tampil profesional!


## Referensi

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Ada banyak websites yang menawarkan berbagai tutorial gratis yang bermutu. Tinggal satu dua klik pencarian di Google.

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

