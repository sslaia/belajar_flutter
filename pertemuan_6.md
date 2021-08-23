# Belajar Bersama Flutter

Pertemuan 6, 26 Agustus 2021


## Merangkum kembali apa yang telah dipelajari kali lalu

Pada pertemuan-pertemuan sebelumnya kita telah belajar beberapa widget dasar sambil mempraktekkannya dalam pembuatan aplikasi Kartu Nama. Kode akhir yang tampak profesional bisa dilihat di [Kartu Nama](https://github.com/sslaia/kartu_nama/blob/pertemuan-5/lib/main.dart).

Pada pertemuan ini kita maju selangkah lagi, belajar bagaimana membuat supaya pengguna dapat berinteraksi dengan aplikasi kita atau yang umum disebut *interaktif*. Untuk itu kita belajar widget baru yang memungkinkan interaksi tsb. yakni **StatefulWidget** dan kedua menggunakan widget **FloatingActionButton**. **ElevatedButton** dan **GestureDetector**. Kemudian kita belajar menggunakan variable dan menciptakan satu fungsi yang bisa melaksanakan perintah tertentu.

Sebagai sarana untuk belajar berbagai widget ini kita akan membangun aplikasi Dadu. Sebagai basis kita gunakan templat aplikasi dari Android Studio (sebelah kiri dalam gambar di bawah ini) lalu langkah demi langkah kita membongkar pasang berbagai widget sehingga mencapai aplikasi Dadu yang kita inginkan (gambar sebelah kanan).

![Aplikasi Dadu](./dadu_app/dadu_app.jpg?raw=true)

## Persiapan

Untuk aplikasi dadu kita membutuhkan beberapa gambar dadu, yang akan kita tempatkan dalam folder *images* dalam aplikasi dadu.

1. Buat folder images di folder utama aplikasi dadu.
2. Klik [di sini](./dadu_app/dadu.zip) untuk mendownload gambar tsb. Setelah didownload, buka berkas tsb. dan kopi semua gambar di dalamnya ke folder *images* yang baru dibuat tadi.
3. Buka berkas pubspec.yaml dan tambahkan kode berikut (info folder images) setelah baris berbunyi **uses-maerial-design: true** (baris ke-45)
```
  assets:
    - images/
```
: Pastikan huruf a dari kata assets sejajar dengan huruf u dalam uses-material-design, lalu permulaan baris berikutnya (tanda **-**) mulai setelah dua spasi dari posisi a tadi, jadi di bawah s yang kedua (perhatikan kode itu baik-baik).
4. Tekan pada *pub get* yang tertera di baris atas berkas pubspec.yaml atau buka terminal dan jalankan perintah `flutter pub get`. Setiap kali ada perubahan di berkas pubspec.yaml, perintah ini harus dijalankan supaya perubahan tsb. diregister di dalam aplikasi.


## Langkah 1: Menciptakan aplikasi dadu_app

1. File > New > New Flutter project
2. Tekan tombol **Next**
3. Di **Project name** isikan: **dadu_app**
4. Biarkan nama folder di mana aplikasi di simpan (standar di **StudioProjects**)
5. Biarkan semua yang lain, toh ini hanya untuk sekedar latihan. Tetapi bila Anda menulis aplikasi sungguhan, Anda harus setidaknya harus memasukkan deskripsi dan organisasi.
6. Tekan tombol **Finish**

Kini Anda berada dalam kode aplikasi **Dadu**, seperti bisa dilihat di sini: [Titik tolak Aplikasi Dadu](https://github.com/sslaia/dadu_app)

## Langkah 2: Mengenal StatefulWidget

Dalam aplikasi Kartu Nama kita telah menggunakan **StatelessWidget** dan dalam templat yang secara otomatis disediakan Android Studio, kita melihat StatelessWidget masih ada seperti kita temukan di aplikasi Kartu Nama.

Namun StatelessWidget tidak memungkinkan ada perubahan nilai atau isi dari widget di layar. Dalam Kartu Nama itu semua elemen di layar itu ditampilkan waktu aplikasi dijalankan dan selesai. Nomor telepon atau gambar atau yang lain tidak akan berubah lagi setelah ditampilkan. Kendati kita telah berkenalan juga dengan widget **Linkable**, yang sekurang-kurangnya membuat link bisa diklik sehingga aplikasi lain bisa dipanggil. Namun tak interaksi. Sentuhan pada nomor telepon tidak mengubah konten apa pun di layar.

Tetapi hari ini kita belajar hal baru. Kita ingin bahwa pengguna bisa berinteraksi dengan aplikasi Dadu. Kini gambar dan tombol tertentu bereaksi kalau disentuh oleh pengguna.

Untuk memungkinkan hal ini kita membutuhkan **StatefulWidget**. Pada prinsipnya StatefulWidget terus menerus mengamati perubahan yang terjadi di dalam berbagai widget yang ada di bawahnya. Secepat terdapat perubahan maka StatefulWidget akan menghapus elemen-elemen yang tampak di layar dan menampilkannya secara ulang (kendati pun gambar atau teksnya masih sama).

Ini berarti bahwa aplikasi kita akan menggunakan lebih banyak *resource* smartphone. Karena itu kalau fungsi *interaktivitas* tidak dibutuhkan kita seyogyanya menggunakan **StatelessWidget**.

Mari mengamati struktur StatefulWidget ini secara sekilas.

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

Tampak rumit kalau dilihat. Namun pada kenyataannya kita tidak perlu mengutak atik konstruksi tsb. Itu adalah sintaks artinya cara penulisan kode StatefulWidget, jadi kita ikuti saja seperti itu. Satu-satunya yang kita sesuaikan adalah nama aplikasi kita, seperti dalam contoh di atas ini Dadu.

Lalu di manakah kita menempatkan kode-kode kita? Pada class yang kedua! Dan itu pulalah yang kita lakukan sekarang.

## Langkah 3: Mendefinisikan variable yang ditubuhkan untuk aplikasi Dadu

Coba berhenti sejenak dan pikirkan variable mana kita butuhkan untuk melemparkan dadu. Tentu saja yang paling penting adalah variable untuk menyimpan angka yang didapatkan setelah melempar dadu. Dan kita tahu angka tsb. adalah integer, artinya angka bulat dari 1 sampai 6. Karena itu nama variablenya bisa misalnya `int nomorDadu = 1`. Waktu pertama kali aplikasi dijalankan kita tampilkan angka 1 (angka lain juga bisa).

Kemudian kita perlu variable teks yang bertipe String, yang berubah tergantung entah angka yang didapat merupakan angka keberuntungan atau tidak. Jadi `String teks = ""`. Waktu pertama kali kita jalankan aplikasi dan dadu belum dikocok, tentu saja tak ada teks yang ditampilkan, karena itu kosong ("").

Variable yang telah ada (*int _counter = 0;*) dihapus saja, karena tidak relevan untuk aplikasi dadu.

**Catatan:** Mereka yang belajar python, perhatikan bahwa di sini string ditulis **String** (lengkap dengan huruf besar di awal), sedangkan di python disingkat menjadi **str**. 


## Langkah 3: Membuat fungsi yang memicu penampilan ulang semua widget di bawah StatefulWidget

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
Kita beri satu nama kepada fungsi tsb. (mis **_kocokDadu()**) supaya kita bisa memanggilnya nanti kalau diperlukan di tempat lain dalam kode kita. Di depannya ditempatkan kata **void**. Ini memberitahu komputer bahwa kita tidak menginginkan ada nilai yang kita harapkan. Jadi komputer tinggal menjalankan kode tsb. dan melupakannya. Pada pertemuan lain kita akan berkenalan dengan fungsi yang memberi kepada kita nilai tertentu setelah mengeksekusi kode.

Lalu kini menyusul pemicu yang disebut diatas: **setState**, artinya mengubah status keseluruhan rangkaian widget di layar. Dalam aplikasi kita yang berubah itu adalah nomor dadu sesuai dengan nomor setelah dikocok.

Perhatikan:
1. kita menggunakan modul random, yang sudah *built-in*, jadi tak perlu diimpor seperti di python.
2. Coba renungkan sejenak, mengapa untuk menghasilkan nomor dadu kode tsb. menggunakan nextInt(6) + 1?

**Catatan:** Mohon perhatikan bahwa setiap pernyataan diakhiri dengan tanda titik koma (**;**) sedangkan di python tidak.

Kini hapus keseluruhan blok kode fungsi *_incrementCounter()* yang tidak kita butuhkan untuk aplikasi dadu.


## Langkah 4: Membuat fungsi yang mengganti teks tergantung apakah pengguna beruntung atau tidak

Seperti fungsi di atas kita juga tidak butuh nilai balik. Jadi digunakan saja **void**. Kita beri saja nama variablenya **_pesanTeks()** lalu dalama badan fungsi tsb. kita pasang persyaratan kondisional logis, yang mirip.

Perhatikan bahwa, agar teks tertentu digunakan setiap kali dadu dikocok, maka kita kaitkan nama fungsi ini di dalam badan setState!

**Perhatian:** mereka yang belajar python mohon memperhatikan perbedaan penulisan persyaratan kondisional ini. Di mana sama dan di mana berbeda?

Kini kita siap membangun kerangka aplikasi dan berbagai widget di dalamnya.


## Langkah 5: Membangun kerangka aplikasi

Coba memperhatikan berbagai widget dalam templat yang kita jadikan basis aplikasi dadu, mulai dari Scaffold, AppBar dst. Nampaknya kita bisa mengambilalih hampir semuanya. Perhatikan gambar tampilan aplikasi dadu, yang akan kita bangun.

Dari gambar itu nampak bahwa kita membutuhkan satu widget Text, satu widget Image dan dua widget Button, satu tombol biasa berisi kata "Kocok dadu!" dan satu lagi tombol yang seakan melayang di sudut kanan bawah, yang disebut  **FloatingActionButton**.

## Langkah 6: Memasang widget Text

Lihat kode templat. Kita hanya butuh satu widget Text, berati yang satu lagi bisa dihapus.

Sekarang daripada menulis langsung string dari widget Text tsb. kita menggunakan variable yang setiap kali berubah tergantung dari hasil pengocokan dadu.
```
            Text(
              teks,
              textAlign: TextAlign.center,
              style: TextStyle(fontSize: 24.0,),
            )
```


## Langkah 7: Memasang widget Image

Kini kita tinggal menyisipkan widget **Image** yang kita pelajari kali lalu di bawah widget **Text**. Di sinilah nanti gambar-gambar dadu sesuai dengan angka setelah dikocok ditampilkan. Masih ingat bagaimana memasang widget Image?
```
              Image.asset(
                'images/dadu$nomorDadu.png',
                width: 120.0,
              ),
```

Perhatikan nama berkas gambar tsb. Kita menggunakan variable **$nomorDadu**, yang didapat setiap kali dadu dikocok, supaya gambar yang ditampilkan sesuai dengan nomor dadu yang baru didapat.


## Langkah 8: Memasang widget ElevatedButton

Di bawah widget **Image** kita memasang satu widget tombol. Ada beberapa pilihan, namun kita pilih widget yang namanya **ElevatedButton**. Widget ini menerima satu anak, dan kita memberi anaknya satu widget **Text** berlabel "Kocok dadu!".

Tetapi ada keistimewaan widget tombol. Tombol menerima isyarat kalau ditekan dan menjalankan perintah apa saja yang kita tulis dalam badan parameter **onPressed**. Kita ingin bahwa setiap kali tombol ini ditekan, fungsi **_kocokDadu()** dijalankan.

Sisipkan widget **ElevatedButton** di bawah widget **Image** sbb:
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


## Langkah 9: Memasang jarak antar widget: SizedBox()

Untuk membuat adanya jarak antara widget Text dan Image sisipkan widget `SizedBox(height: 50.0)` di antaranya. Demikian juga di antara widget **Image** dan widget **ElevatedButton**. Pastikan setiap widget dipisahkan dari widget lainnya yang sesama *children* dengan koma!


## Langkah 9: Menyesuaikan kode FloatingActionButton()

Perhatikan widget **FloatingActionButton()**. Kita perlu menyesuaikan apa yang harus dibuat kalau tombol tsb. ditekan. Dalam aplikasi dadu, kita ingin supaya setiap kali tombol tsb. ditekan, fungsi **_kocokDadu** dijalankan. Maka kita masukkan nama fungsi tsb. di baris **onPressed:**.


## Langkah 10: Membuat supaya dadu juga dikocok kalau disentuh

Kita ingin bahwa bukan hanya dengan menekan tombol, tetapi juga kalau pengguna menekan gambar dadu (persisnya widget **Image**), dadu tsb. dikocok ulang, sehingga mendapatkan angka baru.

Untuk itu melalui fungsi bola lampu, apit widget **Image** dengan satu widget baru. Tukar namanya menjadi **GestureDetector**. Widget ini berfungsi untuk mendeteksi sentuhan atas widget yang jadi anaknya, yakni widget **Image**.

Widget **GestureDetector** menerima satu parameter **onTap** artinya apa yang harus terjadi kalau daerah GestureDetector itu disentuh. Dalam hal aplikasi dadu, kita ingin supaya fungsi mengocok dadu dijalankan, yakni **_kocokDadu()**. Maka tambahkanlah kode tsb. di dalam badan onTap. Keseluruhannya menjadi sbb:

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


## Referensi

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Berbagai dokumentasi, contoh, tutorial dlsb. ada di [https://flutter.dev/docs](https://flutter.dev/docs)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

