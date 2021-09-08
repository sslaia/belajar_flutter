# Belajar Bersama Flutter

Pertemuan 8, 9 September 2021


## Merangkum kembali apa yang telah dipelajari kali lalu

Sampai sekarang kita telah mempelajari banyak widget, yang bisa menghasilkan aplikasi canggih seperti [Dadu](https://github.com/sslaia/dadu_app) dan [Burung Nias](https://github.com/sslaia/burung_nias), yang kita ciptakan minggu lalu.

Melalui pembuatan berbagai aplikasi tsb. kita semakin akrab dengan widget-widget yang sering digunakan dalam aplikasi android seperti **Text**, **Button**, **Image** dlsb.

Minggu lalu kita konsentrasi pada pembuatan daftar (_list_) sederhana. Kita membuat satu daftar berisi nama sepuluh burung Nias.

Kita juga belajar bagaimana mengakses tiap item di dalam daftar tsb., bagaimana membuat supaya kita menampilkan salah satu item berdasarkan berapa kali kita menekan tombol tertentu.

Kemudian kita mempelajari juga apa strategi supaya aplikasi jangan sampai _crash_ karena jumlah klik telah melebihi jumlah item di dalam daftar.

## Tentang apa yang akan kita pelajari hari ini

Hari ini kita mengembangkan lagi pengetahuan kita tentang daftar. Daftar yang kita gunakan dalam aplikasi Burung Nias, hanyalah sekedar daftar sederhana. Kenyataannya daftar yang banyak beredar dan digunakan dalam hidup nyata lebih kompleks (minggu lalu saya menggunakan istilah dua dimensi).

Hari ini kita maju selangkah lagi dalam pemrograman mobile. Kita mengakses daftar konten dari Internet, memprosesnya dan menampilkannya dalam aplikasi kita. Dengan menguasai hal ini, Anda nanti bisa menerapkan mekanisme yang sama untuk menarik konten (berita, foto, pos, dari situs internet, media sosial, dlsb.) dari Internet dan menampilkannya dalam aplikasi buatan Anda.

Untuk memungkinkan hal ini perlu satu mekanisme yang dinamakan API (_application programming interface_). Badan Pusat Statistik (BPS) misalnya menyediakan API, sehingga pengembang aplikasi (_developer_) bisa mengakses data dari BPS dan mengintegrasikannya dalam aplikasi yang mereka tulis (lihat [WebAPI BPS](https://webapi.bps.go.id/developer/)).

Yang disebut API tsb. terdiri dari kunci (API key), yang harus kita mohon dari badan/situs yang datanya ingin kita gunakan, mis. BPS dalam contoh di atas. Dan tentu saja mempelajari bagaimana mengakses data melalui API yang ditelah disusun oleh BPS.

Untuk hari ini kita menggunakan API sederhana, yang tidak membutuhkan kunci, tetapi proses mempelajari struktur data yang ditawarkan melalui APInya sama untuk semua.

Untuk latihan ini kita menggunakan panduan yang telah disusun oleh tim Flutter dari Google di [Parse JSON in the background](https://flutter.dev/docs/cookbook/networking/background-parsing)

Mengingat topik ini lebih kompleks, saya tidak akan memaksakan untuk menyelesaikan topik ini hari ini. Kita maju sejauh kita mampu, lalu sisanya kita teruskan minggu depan.

## Menarik data dari Internet dengan aplikasi Gogowaya

Sebagai sarana praktek untuk mempelajari bagaimana menarik data dari Internet dan memprosesnya, kita akan membuat aplikasi [Gogowaya](https://github.com/sslaia/gogowaya), yaitu satu aplikasi yang menarik foto-foto dari Internet. Nanti mekanisme yang sama bisa digunakan untuk menarik foto dari flicker.com, pexels.com, pixabay.com, unsplash.com dlsb.

Tetapi hal ini tidak hanya berlaku untuk foto, data yang ditarik bisa teks, berita, foto, dokumen, dlsb.

## Mengenal JSON

Untuk mengirim dan menerima data (yang kemungkinan besar terdiri dari daftar) melalui internet salah satu format yang paling umum digunakan adalah JSON.

Misalkan kita memiliki satu daftar 10 foto dengan variable `daftar_foto` dengan nama `foto1`, `foto2`, `foto3`, dst. Dari yang kita pelajari kali lalu kita dapat membuat daftar sbb: `daftar_foto = ['foto1', 'foto2', foto3']`

Namun bagaimana kalau setiap item itu masih memiliki apa yang dalam bahasa pemrograman disebut properti (_properties_) mis:

- `nama_album`
- `nomor_urut`
- `judul`
- `alamat_foto`

Nah, apakah properti ini? Satu daftar? Ternyata tidak! Dalam bahasa pemrograman namanya ini obyek (_object_). Jadi dalam kenyataanya daftar kita sebenarnya merupakan daftar obyek: `daftar_foto = [obyek1, obyek2, obyek2]` Lihat gambar berikut:

![daftar foto](./gogowaya/daftar_foto.png?raw=true)

Dan memang demikianlah kita akan menemukan berbagai data yang akan kita terima dari internet. Sebaliknya kalau nanti kita ingin mengirim data ke Internet kita harus menerjemahkannya ke dalam format seperti ini. Keseluruhannya daftar itu sendiri nanti menjadi satu obyek saja, sehingga bisa dikirim kemana-mana.

Cara penulisan satu obyek berbeda dengan daftar, yang ditandai dengan tanda kurung siku `[]`. Obyek ditandai dengan tanda kurung kurawal `{}`.

Sehingga daftar foto di atas pada kenyataannya dibungkus seperti berikut untuk bisa dikirim melalui internet:

`{"daftar_foto": [{nama_album}, {nomor_urut}, {judul}, {alamat_foto]}`

Format bungkusan seperti ini disebut format JSON. Kita akan menerima data dari internet dalam bentuk ini. Karena itu kita harus membongkar bungkusan itu, sehingga dia menjadi satu daftar kembali dengan berbagai propertinya.

Nah cara untuk bagaimana membongkar bungkusan tsb. akan kita pelajari dalam contoh aplikasi Gogowaya berikut. Begini nanti hasil akhir aplikasi yang kita buat:

![Aplikasi Gogowaya](./gogowaya/gogowaya.jpg?raw=true)

## Langkah 1: Membuat aplikasi baru
1. Buat aplikasi baru dengan **File** > **New** > **New Flutter project**
2. Beri nama **gogowaya** dan tekan tombol **Finish**


## Langkah 2: Kosongkan berkas main.dart

1. Buka berkas **main.dart**
2. Hapus semua isinya.

## Langkah 3: Menyisipkan kode yang telah dipersiapkan ke berkas main.dart

1. Buka kode yang telah dipersiapkan di [https://github.com/sslaia/gogowaya/blob/main/lib/main.dart](https://github.com/sslaia/gogowaya/blob/main/lib/main.dart)
4. Kopi semua kode di dalamnya (dari baris 1 sampai dengan 133).
5. Sisipkan ke dalam berkas main.dart, yang Anda kosongkan tadi di dalam Android Studio.

## Langkah 4: Mengamati kode

Mari mengamati kode aplikasi **Gogowaya**, melihat mana yang telah kita kenal dan mana yang baru.

Untuk sementara lompati dulu baris 1-52.

Kalau kita amati satu per satu, nampaknya semua kodenya familiar sampai baris 80.

Tetapi di baris 81 ada widget baru, yang belum pernah kita pelajari, yakni **FutureBuilder**, yang di dalamnya ada pernyataan kondisi **if**.

```
    return Scaffold(
      appBar: AppBar(
        title: Text(title),
      ),
      body: FutureBuilder<List<Photo>>(
        future: fetchPhotos(http.Client()),
        builder: (context, snapshot) {
          // di sini ada kondisi if
        },
      ),
    );
```

Seperti namanya **FutureBuilder** merupakan satu widget yang memungkinkan kita mengirim satu kode ke internet dan menunggu sampai hasilnya dikirim balik, yang bisa berlangsung beberapa saat di masa depan (_future_)!

Apa yang mau kita capai dengan widget **FutureBuilder**? Kita mau supaya kita mendapatkan daftar foto dari internet. Karena itu kita langsung menuliskannya juga di sini `FutureBuilder<List<Photo>>`.

Penggunaan FutureBuilder ini membedakan aplikasi **Gogowaya** dengan aplikasi yang pernah kita tulis sebelumnya (Dadu dan Burung Nias). Keseluruhan `body` aplikasi **Gogowaya** merupakan hal yang terjadi di masa depan. Praktisnya kita tidak tahu apa yang akan kita tampilkan ke layar smartphone, karena hal ini sangat tergantung dari hasil permintaan yang dikirim ke internet.

Widget **FutureBuilder** menuntut sekurangnya dua parameter, yakni `future`, yakni operasi yang menarik data dari internet, dan `builder`, yakni apa yang harus dibangun (_build_) setelah memproses data dari internet tsb.

Coba perhatikan kondisi **if** yang digunakan untuk menampilkan konten yang telah diperoleh dari internet.

```
          if (snapshot.hasError) {
            return const Center(
              child: Text('An error has occurred!'),
            );
          } else if (snapshot.hasData) {
            return PhotosList(photos: snapshot.data!);
          } else {
            return const Center(
              child: CircularProgressIndicator(),
            );
          }
```

1. Pertama fungsi menjaring _error_. Ini adalah praktek umum dan bahkan diharuskan, supaya pengguna smartphone tahu apa yang terjadi kalau konten tidak muncul-muncul juga di layar.
2. Bila proses menarik data kelamaan (misalnya koneksi internet yang lamban), maka harus ditunjukkan di layar, bahwa data sedang didownload, dengan menggunakan satu widget bernama **CircularProgressIndicator**.
3. Baru kalau semuanya berhasil, data yang telah diperoleh akan diproses (melalui fungsi **PhotosList** di baris 89).

## Langkah 5: Mengamati bagian menampilkan data

Dari baris 101 mulai bagian menampilkan data dari internet, yang telah diproses. Kode aplikasi hanya akan sampai ke sini bila tak ada _error_ dan proses download telah berhasil.

1. Pada baris 104 dibuat variable `photos`, yang isinya diambil dari satu daftar bernama Photo dengan menulis `final List<Photo> photos;` Kita tahu bahwa daftar tsb. ada isinya sekarang dan isinya berasal dari internet.
2. Sekarang kita menggunakan variable `photos` untuk menampilkan daftar foto dari internet.
3. Berdasarkan apa yang akan kita analisa **di bawah ini** kita tahu bahwa properti dari setiap foto yang kita simpan dalam variable `photos` mencakup _caption_ foto, yang disimpan dalam variable `title` dan alamat foto tsb. di internet, yang disimpan dalam variable `url`.
4. Sekarang dengan menggunakan widget **ListView.builder**, satu widget yang memungkinkan membuat pengulangan (_loop_) untuk menarik satu per satu item di dalam satu daftar, lalu menampilkannya di layar melalui widget **ListTile**. Dalam contoh ini widget **ListTile** diapit dengan widget **Card** untuk mendapatkan tampilan seperti kartu.

## Langkah 6: Mengirim perintah untuk menarik data dari internet

Sekarang mari melihat baris 82. Kita sudah singgung tadi bahwa widget **FutureBuilder** mengirim perintah ke internet melalui parameter `future`.

Nah apa nama fungsi yang menjalankan perintah tsb? Fungsi tsb. bernama `fetchPhotos()`, yang keseluruhannya nampak sbb.: `future: fetchPhotos(http.Client())` 

Rupanya fetchPhotos menyertakan nilai (atau _argument_ dalam bahasa pemrograman) yang bernama http.Client(). http sendiri merupakan sebuah paket eksternal, yang diimpor seperti bisa dilihat di baris 6. http dan tiga paket lainnya yang diimpor (baris 1 s/d 4) semua bahu membahu menarik data dari internet, membuka bungkusannya dan memprosesnya.

## Langkah 7: Membuat klas Photo, yang menampung properti obyek Photo

Dari mana kita tahu properti dari sebuah obyek data? Kita harus baca dari dokumentasi API penyedia data di internet. Jadi berbeda-beda dari satu website ke website lain. Jadi untuk mengetahui properti dari obyek yang dikirim oleh Badan Pusat Statistik yang disebut di atas kita harus pergi melihat dokumentasi yang mereka sediakan!

Untuk contoh digunakan dalam latihan ini, yakni https://jsonplaceholder.typicode.com, kita bisa membaca dokumentasi yang mereka sediakan. Misalnya untuk daftar foto, yang bisa diakses di https://jsonplaceholder.typicode.com/photos strukturnya sbb.:

```
[
  {
    "albumId": 1,
    "id": 1,
    "title": "accusamus beatae ad facilis cum similique qui sunt",
    "url": "https://via.placeholder.com/600/92c952",
    "thumbnailUrl": "https://via.placeholder.com/150/92c952"
  },
  {
    "albumId": 1,
    "id": 2,
    "title": "reprehenderit est deserunt velit ipsam",
    "url": "https://via.placeholder.com/600/771796",
    "thumbnailUrl": "https://via.placeholder.com/150/771796"
  }
]
```
Coba perhatikan daftar itu (tanda kurung siku dan tanda kurung kurawal), yang masih dalam format JSON. Berarti daftar foto tsb bisa sbb.:
```
foto = [foto1, foto2, foto3]
```
sedangkan obyeknya sbb.:
```
foto1 = {'albumId', 'id', 'title', 'url', 'thumbnailUrl'}
```
Untuk membuka bungkusan json dan menjadikannya daftar di smartphone lokal, kita harus menciptakan klas, yang dalam latihan ini disebut Photo. Keseluruhannya demikian:
```
class Photo {
  final int albumId;
  final int id;
  final String title;
  final String url;
  final String thumbnailUrl;

  const Photo({
    required this.albumId,
    required this.id,
    required this.title,
    required this.url,
    required this.thumbnailUrl,
  });

  factory Photo.fromJson(Map<String, dynamic> json) {
    return Photo(
      albumId: json['albumId'] as int,
      id: json['id'] as int,
      title: json['title'] as String,
      url: json['url'] as String,
      thumbnailUrl: json['thumbnailUrl'] as String,
    );
  }
}

```

## Langkah 8: Menarik data dari internet dan memasukkannya dalam daftar Photo

Sekarang kita lihat bagian terakhir kode aplikasi Gogowaya. Kita telah mendefinisikan klas foto, yang memberi struktur dari data yang diterima dan menampung properti dari setiap foto yang didownload dari internet.

Kodenya demikian:
```
Future<List<Photo>> fetchPhotos(http.Client client) async {
  final response = await client.get(
  // Uri.parse('https://my-json-server.typicode.com/sslaia/katawaena/photos'));
   Uri.parse('https://jsonplaceholder.typicode.com/photos'));

  // Use the compute function to run parsePhotos in a separate isolate.
  return compute(parsePhotos, response.body);
}

// A function that converts a response body into a List<Photo>.
List<Photo> parsePhotos(String responseBody) {
  final parsed = jsonDecode(responseBody).cast<Map<String, dynamic>>();

  return parsed.map<Photo>((json) => Photo.fromJson(json)).toList();
}
```

Pertama kita melihat ada fungsi `fetchPhotos()` yang kita tahu dipanggil dari baris 82 kode aplikasi tadi. Kemudian kita lihat tipe datanya adalah `List`, yang dalam hal ini daftar bernama `Photo`, sebagaimana didefinisikan dalam klas Photo di atas. Dan karena daftar ini baru akan dibuat di masa depan, daftar photo ini dibungkus dalam **Future**.

Selebihnya adalah menarik data dari internet, melalui `client.get()`, yang tentu saja kita dapat dalam format json. Hal ini disimpan dalam satu variable bernama `response`. Dalam `response` ini kita mendapat entah data yang kita inginkan atau pesan `error` kalau ada gangguan.

Data dalam response ini kemudian dibongkar melalui perintah `jsonDecode` dan disimpan dalam variable `parsed`. Kemudian data yang telah dibongkar ini dikonversi ke daftar (lihat bagian `.toList()`).

Sekarang kita siap menampilkan daftar foto tsb. di layar smartphone. Jalankan aplikasi dan lihat hasilnya.

## Langkah 9: Menarik data dari internet dengan foto sungguhan

Memang contoh ini tidak mengirim foto sungguhan. Supaya bisa melihat foto sunggguhan pasang tanda komentar di baris 15 dan hapus tanda komentar dari baris 14.

Jalan kembali aplikasi dan nikmati hasilnya!

![Gogowaya](./towi_towi/towi2.jpg?raw=true) (sebelah kiri)


## Refleksi

1. Coba bayangkan aplikasi mana saja yang kira-kira menggunakan mekanisme serupa untuk menarik data dari internet?
2. Apakah Anda berminat membuat aplikasi semacam ini dengan menarik foto-foto menarik dari pixabay.com, pexels.com atau unsplash.com misalnya?


## Referensi

Kita bisa melihat daftar icon serta namanya, yang kita bisa gunakan dalam kode kita, di [Google Fonts](https://fonts.google.com/icons) dan pilih icons. Di situ juga terdapat sekitar seribu huruf yang kita bisa gunakan secara bebas, termasuk huruf profesional, yang berharga ratusan dollar. 

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Berbagai dokumentasi, contoh, tutorial dlsb. ada di [https://flutter.dev/docs](https://flutter.dev/docs)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)








