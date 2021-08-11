# Belajar Bersama Flutter

Pertemuan 5, 12 Aug 2021


## Merangkum kembali apa yang telah dipelajari minggu lalu

Pada pertemuan ke-4 minggu lalu kita telah memoles aplikasi [Kartu Nama](https://github.com/sslaia/kartu_nama) dengan menambah beberapa fitur: menambah foto sendiri, menambah icon, mengenal beberapa widget yang berkaitan (CircleAvatar, Icon, Row, Column), mengenal beberapa properti dari widget Text (mengubah besar serta gaya huruf, mengubah warna). Kita juga telah berkenalan bagaimana mengedit berkas pubspec.yaml dengan menambahkan informasi tentang PATH gambar.

Minggu ini kita membuat aplikasi [Kartu Nama](https://github.com/sslaia/kartu_nama) itu tampil profesional dan layak dipamerkan/dipajang kepada orang lain.


## Berkenalan dengan keseharian para programmer: *refactoring*

Bagi seorang programmer menulis satu aplikasi itu tidak pernah selesai sekali jadi. Umumnya setelah aplikasi selesai, muncul ide baru untuk membuat aplikasi tsb. lebih baik, entah memperbaiki desain atau malah menambah fitur baru. Karena itu satu aplikasi mengalami update terus menerus, ada versi 1.0, 2.0 dst.

Seluruh proses membongkar-pasang satu aplikasi untuk mengadopsi fitur baru dinamakan *refactoring*. Tidak jarang untuk mencapai tujuan itu, kerangka aplikasi harus diubah, berarti gonta-ganti widget sana sini.

Hal yang sama terjadi dengan aplikasi [Kartu Nama](https://github.com/sslaia/kartu_nama). Masih ingat penampilan pertama aplikasi, yang hanya menampilkan satu teks di tengah? ![Refactoring Kartu Nama](./kartu_nama/kartu_nama3.jpg?raw=true) Kemudian kita menghapus widget tertentu (widget **Center**), menambahkan yang lain (widget **Image**, **Text**, **Icon** dan **SizedBox**), bahkan menggunakan widget yang memiliki anak-anak (*children*) (widget **Row** dan **Column**) dlsb. Karena kita ingin memasang foto, icon, memasang berbagai elemen di layar, kita telah membongkar-pasang (*refactoring*) aplikasi tsb. Jadi secara Anda tidak sadari Anda telah menjalani hidup nyata sebagai programmer!


## Membuat aplikasi Kartu Nama tampil profesional

Bagaimana kita membuat aplikasi Kartu Nama tsb. tampil lebih profesional? Perubahan sedikit bisa mengakibatkan efek visual yang kuat.

![Refactoring Kartu Nama](./kartu_nama/kartu_nama_refactoring.jpg?raw=true)

Coba lihat mis. konsep pertama kartu nama dalam gambar di atas. Bagus, sederhana dan *to the point*. Tetapi bandingkan dengan gambar sebelah kanan. Hanya dengan memberi warna latarbelakang berbeda, kesan yang muncul terasa lebih intensif. Hal ini kemudian diperkuat lagi dengan membuat nama lebih besar serta menampilkan nomor telepon, alamat email serta alamat rumah dalam gaya sebuah kartu (menggunakan widget **Card**), yang memiliki efek bayangan.

Bagaimana kita mencapai hal tsb.? Silakan membuka kode [Kartu Nama pada Pertemuan 5](https://github.com/sslaia/kartu_nama/blob/pertemuan-5/lib/main.dart) Dan sambil mengamati perubahan dalam kode itu, kita mengimplementasikan berbagai perbaikan yang disebut di atas.


## Membuat teks dapat diklik (*clickable*)

Ada banyak widget yang bisa digunakan untuk mencapai hal yang sama. Dalam latihan ini kita menggunakan paket [linkable](https://pub.dev/packages/linkable)

1. Buka [linkable](https://pub.dev/packages/linkable) dan ikuti petunjuk instalasi di sana.
2. Impor paket tsb. di awal berkas **main.dart**: 
```
import 'package:linkable/linkable.dart';
```
3. Ganti widget **Text** dengan **Linkable** dan tempatkan **text:** di depan parameter string.
4. Selesai! Silakan mencoba sendiri apakah kini aplikasi menelpon otomatis terbuka bila mengklik nomor telepon dalam aplikasi tsb.


## Menyesuaikan Manifest.xml aplikasi Android

Kalau tidak terjadi apa-apa, walaupun telah memasang widget **Linkable** di atas, maka perlu menambah pesan dalam berkas surat pengantar Android, yang disebut **AndroidManifest.xml** (hal yang sama juga dituntut di iOS). Logikanya mirip kalau kita mengirim paket/parsel melalui jasa spedisi. Kita harus mendeklarasikan isi dari parsel tsb. sehingga petugas transportasi tahu dan membiarkan lewat.

Berkas AndroidManifest.xml tsb. ada di **android/app/src/main**. Silakan mengikuti contoh mendeklarasikan hal-hal yang kita mau dibuat oleh sistem Android (membuka URL, aplikasi telpon dan email) di [https://pub.dev/packages/url_launcher](https://pub.dev/packages/url_launcher)


## Menggunakan widget Row dengan ListTile

Menggunakan widget **ListTile** kadang lebih elegan daripada **Row** karena memiliki kemungkinan parameter yang lebih.

1. Melalui fungsi bola lampu, ganti widget **Row** menjadi **ListTile**.
2. Kita akan menyediakan dua parameter **ListTile** yakni *leading* (di mana kita menempatkan icon) dan *title* (di mana kita menempatkan teks). Kita tidak perlu mengubah icon dan teks tsb. tinggal mengambilalih yang sudah ada.
3. Nikmati!

Perhatikan bahwa sekarang kita tidak perlu menggunakan widget **SizedBox** untuk menciptakan spasi antara icon dan teks! **ListTile** mengatur hal itu secara otomatis!

Widget **ListTile** sering sekali digunakan terutama dalam membuat daftar. Coba perhatikan daftar pesan di Telegram, WhatsApp atau Gmail. Daftar tsb. menggunakan **ListTile**! Berarti Anda tinggal selangkah lagi untuk membuat klon tampilan aplikasi seperti Telegram, WhatsApp atau Gmail!


## Menggunakan widget Card

Pasti Anda pernah melihat tampilan kartu dengan menggunakan widget **Card** ini, hanya Anda mungkin tidak sadar. Bersama dengan **ListTile** widget **Card** sering digunakan baik untuk menampilkan daftar maupun untuk menampilkan potongan teks tertentu yang memberi kesan bagaikan sebuah kartu baik yang tampil sederhana, sehingga tidak begitu jelas, maupun tampil seperti melayang tiga dimensi.

1. Melalui fungsi bola lampu, apit **ListTile** dengan **widget** (baris pertama).
2. Ganti nama widget menjadi **Card**. Widget **Card** mempunyai satu anak(*child*), maka jadikan **ListTile** tadi menjadi anak dari **Card**.
3. Ada banyak parameter yang bisa digunakan untuk **Card**. Kita menggunakan dua saja, yakni *elevation* dan *margin*. Paramater *elevation* menerima angka, seperti 4.0. Semakin besar angka tsb. semakin melayang *Card* itu dari latarbelakang. Coba bereksperimen dengan memasukkan angka 4.0, kemudian angka 16.0 untuk melihat bedanya. Semakin melayang kartu tsb. semakin tampak bayangan di bawahnya, yang membuat efek melayang itu.
4. Parameter *margin* menerima widget **EdgeInsets**. Dalam contoh ini kita menggunakan simetris artinya angka yang sama digunakan untuk atas/bawah kalau vertikal dan kiri/kanan kalau horizonontal. Coba bereksperimen dengan angka-angka tsb. untuk melihat efeknya.
5. Selesai. Nikmati hasil karya Anda! Untuk pertama kalinya Anda telah menciptakan aplikasi yang tampil profesional dan dibuat profesional!


## Menggunakan Google Fonts (*kalau ada waktu*)

Google Fonts tersedia sebagai paket tambahan untuk Flutter di [https://pub.dev/packages/google_fonts](https://pub.dev/packages/google_fonts)

1. Tambahkan paket tsb. entah dengan mengedit langsung berkas pubspec.yaml seperti ditulis dalam cara menginstalasi di alamat tsb. di atas, atau menggunakan jalan pintas berikut di terminal Android Studio:
```
flutter pub add google_fonts 
```

2. Impor paket tsb. dengan menambahkan baris berikut di atas isi dari berkas main.dart
```
import 'package:google_fonts/google_fonts.dart';
```

3. Aplikasikan penggunakan google fonts di dalam kode. Perhatikan bagaimana penulisan parameter **style** dari widget **Text**, contoh baris tentang pekerjaan.
```
          Text(
            _pekerjaan,
            style: TextStyle(
              fontSize: 14.0,
              letterSpacing: 2.5,
              fontWeight: FontWeight.bold,
              color: Colors.white,
            ),
          ),
```

Nah menurut dokumentasi dari Google Fonts cara penggunaan paket ini di dalam teks adalah dengan mengubah seluruh nilai parameter **TextStyle** menjadi **GoogleFonts.[NAMA_FONTS]** mis. dalam contoh di bawah ini menggunakan huruf bernama *lato*.

```
          Text(
            _pekerjaan,
            style: GoogleFonts.lato(
              textStyle: TextStyle(
                  fontSize: 14.0, 
                  letterSpacing: 2.5, 
                  fontWeight: FontWeight.bold, 
                  color: Colors.white),
            ),
          ),
```

Selesai! Dengan kode sederhana ini Anda tak perlu membeli huruf profesional yang harganya ratusan dollar. Google telah menyediakannya bebas untuk Anda dan Anda bisa menggunakannya secara komersil tanpa harus membayar apa-apa!


## Referensi

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

