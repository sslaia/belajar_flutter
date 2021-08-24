# Belajar Bersama Flutter

Pertemuan 6, 26 Agustus 2021


## Merangkum kembali apa yang telah dipelajari kali lalu

Pada pertemuan-pertemuan sebelumnya kita telah belajar beberapa widget dasar sambil mempraktekkan pneggunaannya dalam pembuatan aplikasi Kartu Nama. Kode akhir yang tampak profesional bisa dilihat di [Kartu Nama](https://github.com/sslaia/kartu_nama/blob/pertemuan-5/lib/main.dart).

Pada pertemuan ini kita maju selangkah lagi, belajar bagaimana membuat supaya pengguna dapat berinteraksi dengan aplikasi kita atau yang umum disebut *interaktif*. Untuk itu kita belajar widget baru yang memungkinkan interaksi tsb. yakni **StatefulWidget** dan kedua menggunakan widget **FloatingActionButton**, **ElevatedButton** dan **GestureDetector**. Kemudian kita belajar menggunakan variable dan menciptakan satu fungsi yang bisa melaksanakan perintah tertentu.

Sebagai sarana untuk belajar berbagai widget ini kita akan membangun aplikasi Dadu. Sebagai basis kita gunakan templat aplikasi dari **Android Studio** (sebelah kiri dalam gambar di bawah ini) lalu langkah demi langkah kita membongkar pasang berbagai widget sehingga mencapai aplikasi Dadu yang kita inginkan (gambar sebelah kanan).

![Aplikasi Dadu](./dadu_app/dadu_app.jpg?raw=true)

## Langkah 1: Menciptakan aplikasi dadu_app

1. File > New > New Flutter project
2. Tekan tombol **Next**
3. Di **Project name** isikan: **dadu_app**
4. Biarkan nama folder di mana aplikasi di simpan (standar di **StudioProjects**)
5. Biarkan semua yang lain, toh ini hanya untuk sekedar latihan. Tetapi bila Anda menulis aplikasi sungguhan, Anda harus setidaknya harus memasukkan deskripsi dan organisasi.
6. Tekan tombol **Finish**

Kini Anda berada dalam kode aplikasi yang akan kita sulap menjadi aplikasi **Dadu**, seperti bisa dilihat di sini: [Titik tolak Aplikasi Dadu](https://github.com/sslaia/dadu_app/blob/main/lib/main.dart)


## Langkah 2: Mempersiapkan gambar dadu

Untuk aplikasi dadu kita membutuhkan beberapa gambar dadu, yang akan kita tempatkan dalam folder *images* dalam aplikasi dadu.

1. Buat folder images di folder utama aplikasi dadu dalam **Android Studio**.
2. Klik [di sini](./dadu_app/dadu.zip) lalu tekan tombol download untuk mengunduh gambar tsb. Setelah didownload, buka berkas tsb. dan kopi semua gambar di dalamnya ke folder *images* yang baru dibuat tadi di dalam **Android Studio**.
3. Buka berkas **pubspec.yaml** dan tambahkan kode berikut setelah baris berbunyi **uses-maerial-design: true** (baris ke-45)
```
  assets:
    - images/
```
- Pastikan huruf a dari kata assets sejajar dengan huruf u dalam uses-material-design, lalu permulaan baris berikutnya (tanda **-**) mulai setelah dua spasi dari posisi a tadi, jadi di bawah s yang kedua (perhatikan kode itu baik-baik).

4. Tekan pada *pub get* yang tertera di baris atas berkas pubspec.yaml atau buka terminal dan jalankan perintah `flutter pub get`. Setiap kali ada perubahan di berkas pubspec.yaml, perintah ini harus dijalankan supaya perubahan tsb. diregister di dalam aplikasi.


## Langkah 3: Mengenal StatefulWidget

Dalam aplikasi Kartu Nama kita telah menggunakan **StatelessWidget** dan dalam templat yang secara otomatis disediakan **Android Studio**, kita melihat **StatelessWidget** masih ada seperti kita temukan di aplikasi Kartu Nama.

Namun **StatelessWidget** tidak memungkinkan ada perubahan nilai atau isi dari widget di layar. Dalam Kartu Nama itu semua elemen di layar itu ditampilkan waktu aplikasi dijalankan dan selesai. Nomor telepon telepon atau gambar atau elemen lainnya tidak akan berubah lagi setelah ditampilkan. Kendati kita telah berkenalan juga dengan widget **Linkable**, yang sekurang-kurangnya membuat link bisa diklik dan membuka aplikasi lainnya. Namun pada dasarnya konten di layar tidak berubah.

Tetapi hari ini kita belajar hal baru. Kita ingin bahwa pengguna bisa berinteraksi dengan aplikasi Dadu. Artinya bila pengguna menyentuh dadu atau tombol tertentu, gambar dadu juga berubah sesuai dengan angka yang diperoleh waktu melempar dadu.

Untuk memungkinkan hal ini kita membutuhkan **StatefulWidget**. Pada prinsipnya **StatefulWidget** terus menerus mengamati perubahan yang terjadi di dalam berbagai widget yang ada di bawahnya. Secepat terdapat perubahan maka StatefulWidget akan menghapus elemen-elemen yang tampak di layar dan menampilkannya secara ulang (kendati pun gambar atau teksnya masih sama).

Ini berarti bahwa aplikasi kita akan menggunakan lebih banyak *resource* smartphone. Karena itu kalau fungsi *interaktivitas* ini tidak dibutuhkan oleh aplikasi kita, maka seyogyanya kita menggunakan **StatelessWidget**.

Mari mengamati struktur **StatefulWidget** ini secara sekilas.

```
class Dadu extends StatefulWidget {
  const Dadu({Key? key}) : super(key: key);

  @override
  _DaduState createState() => _DaduState();
}

class _DaduState extends State<Dadu> {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

Tampak rumit kalau pertama kali melihatnya. Namun pada kenyataannya kita tidak perlu mengutak atik konstruksi tsb. Itu adalah yang namanya *sintaks* artinya demikianlah cara penulisan kode **StatefulWidget**, jadi untuk bisa *fluent* berbicara bahasa *Flutter* kita mengikuti saja tatabahasa seperti itu.

Satu-satunya yang kita perlu sesuaikan dalam pembentukan kode itu adalah nama aplikasi kita, yakni **Dadu**, seperti bisa dilihat dalam contoh potongan kode di atas.

Lalu di manakah kita menempatkan kode-kode kita sendiri? Pada **class** yang kedua! Dan itu pulalah yang kita lakukan sekarang.


## Langkah 4: Mendefinisikan variable yang dibutuhkan untuk aplikasi Dadu

Coba dulu berhenti sejenak dan memikirkan kita membutuhkan variable apa untuk melemparkan dadu.

Tentu saja kita membutuhkan satu variable, yang memungkinkan kita menyimpan angka yang didapatkan setiap kali kita melempar dadu. Dan kita juga tahu bahwa angka tsb. pasti *integer*, artinya angka bulat dari 1 sampai 6.

Karena itu kita bisa memberi nama variablenya misalnya `int nomorDadu = 1`. Waktu pertama kali aplikasi dijalankan kita tampilkan angka 1 (angka lain juga bisa).

Kemudian kita perlu satu variable teks yang bertipe *String*, yang bunyinya berubah tergantung entah angka yang didapat merupakan angka keberuntungan atau tidak. Jadi kita mendefinisikan variable `String teks = ""`. Waktu pertama kali kita jalankan aplikasi dan dadu belum dikocok, tentu saja kita belum menunjukkan teks apa-apa, karena itu variablenya kita deklarasikan kosong ("").

Variable yang telah ada (*int _counter = 0;*) dihapus saja, karena tidak relevan untuk aplikasi dadu.

**Catatan:** Mereka yang belajar python, perhatikan bahwa tipe data string di Flutter ditulis **String** (lengkap dengan huruf besar di awal), sedangkan di Python penulisannya disingkat menjadi **str**! 


## Langkah 5: Membuat fungsi yang memicu penampilan ulang semua widget di bawah StatefulWidget

Kita ingin bahwa setiap kali kita menyentuh satu tombol atau gambar dadu, aplikasi memulai proses melempar dadu dan memberi tahu pemicu bahwa status aplikasi kita telah berubah dan elemen-elemen di layar perlu dimuat ulang (*refresh*).

Untuk itu kita membuat satu fungsi yang nampak seperti berikut:

```
  void _kocokDadu() {
    setState(() {
      nomorDadu = Random().nextInt(6) + 1;
      _pesanTeks();
    });
  }
```
Kita beri satu **nama** kepada fungsi tsb. (mis **_kocokDadu()**) supaya kita bisa memanggilnya nanti kalau diperlukan di tempat lain dalam kode kita. Di depannya ditempatkan kata **void**. Ini memberitahu komputer bahwa kita *tidak mengharapkan* kode yang ada di dalam fungsi tsb. memberi balik (*return*) satu nilai. Jadi komputer tinggal menjalankan kode tsb. dan melupakannya. Pada pertemuan lain kita akan berkenalan dengan fungsi yang memberi kepada kita nilai tertentu (*return*) setelah mengeksekusi kode.

Lalu kini menyusul pemicu yang disebut diatas: **setState**, artinya mengubah status keseluruhan rangkaian widget di layar. Dalam aplikasi kita yang berubah itu adalah nomor dadu sesuai dengan nomor setelah dikocok.

Perhatikan:
1. Kita menggunakan modul **random**, yang perlu diimpor dengan `import 'dart:math';`.
2. Coba renungkan sejenak, mengapa untuk menghasilkan nomor dadu kode tsb. menggunakan `nextInt(6) + 1`? *nextInt* berarti pastikan angka berikutnya yang dihasilkan dalam bentuk bilangan bulat (*integer*). Tetapi mengapa 6 dan ada lagi + 1?

**Catatan:** Mohon perhatikan bahwa setiap pernyataan di Flutter diakhiri dengan tanda titik koma (**;**) sedangkan di python tidak!

Kini hapus keseluruhan blok kode fungsi *_incrementCounter()* dari templat, yang kita tidak butuhkan untuk aplikasi dadu.


## Langkah 6: Membuat fungsi yang mengganti teks tergantung apakah pengguna beruntung atau tidak

Seperti fungsi di atas, untuk fungsi teks kita juga tidak membutuhkan nilai balik (*return*). Karena itu kita menandainya **void**. Kita memberi nama variablenya **_pesanTeks()** lalu dalam badan fungsi tsb. kita memasang persyaratan kondisional logis, yang mirip dengan apa yang kita pelajari di Python.

Perhatikan bahwa, agar teks tertentu digunakan setiap kali dadu dikocok, maka kita mengaitkan nama fungsi ini di dalam badan setState!

**Perhatian:** mereka yang belajar python mohon memperhatikan perbedaan penulisan persyaratan kondisional ini. Apakah yang sama dan apa pula yang berbeda?

Kini kita siap membangun kerangka aplikasi (**Scaffold**) dan berbagai widget di dalamnya.


## Langkah 7: Membangun kerangka aplikasi

Silakan memperhatikan berbagai widget dalam templat yang kita jadikan basis aplikasi dadu ini, mulai dari Scaffold, AppBar dst. Nampaknya kita bisa mengambilalih hampir semuanya.

Perhatikan juga gambar tampilan aplikasi dadu, yang akan kita bangun.

Dari gambar itu nampak bahwa kita membutuhkan satu widget Text, satu widget Image dan dua widget Button, satu tombol biasa berisi kata "Kocok dadu!" dan satu lagi tombol yang seakan melayang di sudut kanan bawah, yang disebut  **FloatingActionButton**.


## Langkah 8: Memasang widget Text

Amati sekali lagi kode templat. Kita hanya membutuhkan satu widget Text, berati widget Text yang satu lagi bisa dihapus.

Sekarang daripada menulis langsung string dari widget Text tsb. kita menggunakan variable yang setiap kali berubah tergantung dari hasil pengocokan dadu. Kodenya menjadi demikian:
```
            Text(
              teks,
              textAlign: TextAlign.center,
              style: TextStyle(fontSize: 24.0,),
            )
```
Kita telah menggunakan widget **Text** beberapa kali dan telah mulai akrab dengan berbagai parameternya. Di dalam kode ini ada parameter baru, yakni *textAlign* untuk mengatur letak teks di layar (kiri, tengah, kanan). Dalam kode ini kita ingin meluruskannya di tengah, jadi `textAlign: TextAlign.center`.


## Langkah 9: Memasang widget Image

Kini kita tinggal menyisipkan widget **Image**, yang kita pelajari kali lalu, di bawah widget **Text** yang telah ada. Di sinilah nanti gambar-gambar dadu ditampilkan sesuai dengan angka yang didapatkan setelah dadu dikocok. Masih ingat bagaimana memasang widget **Image**?
```
              Image.asset(
                'images/dadu$nomorDadu.png',
                width: 120.0,
              ),
```

Perhatikan nama berkas gambar tsb. Kita menggunakan variable **$nomorDadu**, yang didapat setiap kali dadu dikocok, supaya gambar yang ditampilkan sesuai dengan nomor dadu yang baru didapat setelah dikocok.


## Langkah 10: Memasang widget ElevatedButton

Di bawah widget **Image** kita memasang satu widget tombol. Ada beberapa pilihan, namun kita memilih widget yang namanya **ElevatedButton**. Widget ini menerima satu anak, dan kita memberi anaknya satu widget **Text** berlabel "Kocok dadu!".

Tetapi ada keistimewaan widget tombol. Tombol menerima isyarat kalau ditekan dan menjalankan perintah apa saja yang kita tulis dalam badan parameter **onPressed**. Dalam aplikasi dadu, kita menginginkan bahwa setiap kali kita menekan tombol ini, komputer akan menjalankan fungsi **_kocokDadu()**.

Untuk itu kita menyisipkan widget **ElevatedButton** di bawah widget **Image** sbb.:
```
            ElevatedButton(
              onPressed: () {
                _kocokDadu();
              },
              child: Text(
                'Kocok dadu!',
              ),
            ),
```


## Langkah 11: Memasang jarak antar widget: SizedBox()

Untuk membuat adanya jarak antara widget **Text** dan **Image** sisipkan widget `SizedBox(height: 50.0)` di antara keduanya. Demikian juga di antara widget **Image** dan widget **ElevatedButton**.

Pastikan juga bahwa setiap widget dipisahkan dari widget lainnya yang sesama *children* dengan tanda koma!


## Langkah 12: Menyesuaikan kode FloatingActionButton()

Perhatikan widget **FloatingActionButton()**. Kita perlu menyesuaikan apa yang harus dibuat oleh komputer kalau kita menekan tombol tsb. Dalam aplikasi dadu, kita menginginkan supaya setiap kali kita menekan tombol tsb. fungsi **_kocokDadu** akan dieksekusi. Maka kita memasukkan nama fungsi tsb. di baris **onPressed:**.


## Langkah 13: Membuat supaya dadu juga dikocok kalau disentuh

Kita juga menginginkan bahwa kalau pengguna menekan gambar dadu (persisnya widget **Image**), dadu tsb. dikocok ulang, sehingga angka baru didapatkan.

Untuk itu melalui fungsi bola lampu, apitlah widget **Image** dengan satu widget baru (*wrap this widget*). Tukar namanya menjadi **GestureDetector**. Widget ini berfungsi untuk mendeteksi sentuhan atas widget yang jadi anaknya, yakni widget **Image**.

Widget **GestureDetector** menerima satu parameter **onTap** artinya apa yang harus terjadi kalau daerah GestureDetector itu disentuh (yang dalam hal ini berarti semua daerah di mana widget **Image** berada). Dalam hal aplikasi dadu, kita menginginkan supaya fungsi mengocok dadu **_kocokDadu()** dijalankan. Maka tambahkanlah sekarang kode tsb. di dalam badan onTap itu. Keseluruhannya menjadi sbb:

```
            GestureDetector(
              onTap: () {
                _kocokDadu();
              },
              child: Image.asset(
                'images/dadu$nomorDadu.png',
                width: 120.0,
              ),
            ),
```

Kini aplikasi Dadu telah selesai. Klik "Run" supaya dikompilasi dan ditampilkan di android emulator atau di smartphone yang terhubung ke laptop Anda!

Selesai! Dengan kode-kode ini Anda telah membangun aplikasi interaktif pertama Anda! Pada pandangan pertama kode-kode itu terkesan rumit. Namun setelah dipilah-pilah, rupanya tidak serumit yang disangka!

Sengaja saya memberi tiga kemungkinan interaksi (melalui dua tombol dan satu GestureDetector), supaya Anda memiliki beberapa pilihan yang Anda bisa pilih salah satu di aplikasi yang Anda tulis nanti.

Selain itu sambil lalu Anda telah belajar juga bagaimana memanipulasi teks di layar berdasarkan sentuhan di daerah tertentu di layar.

**Pertanyaan:** Hal apa saja menurut Anda membutuhkan interaksi seperti ini?

Klik di [Aplikasi Dadu](https://github.com/sslaia/dadu_app/blob/pertemuan-6/lib/main.dart) kalau Anda ingin membandingkan kode yang Anda tulis dengan kode yang saya persiapkan untuk pertemuan ini.


## Referensi

Kita bisa melihat daftar icon serta namanya, yang kita bisa gunakan dalam kode kita, di [Google Fonts[(https://fonts.google.com/icons) dan pilih icons. Di situ juga terdapat ratusan huruf yang kita bisa gunakan secara bebas, termasuk huruf profesional, yang berharga ratusan dollar. 

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Berbagai dokumentasi, contoh, tutorial dlsb. ada di [https://flutter.dev/docs](https://flutter.dev/docs)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

