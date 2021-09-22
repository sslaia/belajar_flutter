# Belajar Bersama Flutter

Pertemuan 9, 23 September 2021


## Merangkum kembali apa yang telah dipelajari kali lalu

Dalam dua pertemuan terakhir kita telah mengenal cara mengakses data dari Internet melalui satu koneksi standar yang disebut API (_application programming interface_).

Pertama kita mencoba hal ini melalui aplikasi foto bernama [Gogowaya](https://github.com/sslaia/gogowaya) dan kemudian melalui aplikasi sejenis berita [Towi-Towi](https://github.com/sslaia/towi).

Melalui dua aplikasi tsb. kita telah berkenalan dengan berbagai perangkat dasar untuk mengakses data dari berbagai website mis. foto (flickr.com, unsplash.com, pexels.com dst), berita (detik.com, thejakartapost.com, dst.), berbagai data lainnya (bps.go.id, bmkg.co.id, dst.)

Minggu ini kita meneruskan eksplorasi kita dengan mencari tahu bagaimana menciptakan layar baru di dalam aplikasi dan bagaimana mengirim data ke layar tsb.

## Navigasi ke layar baru di Flutter

Sampai sekarang aplikasi kita hanya memiliki satu layar saja. Aplikasi [Kartu](https://github.com/sslaia/kartu_nama/tree/pertemuan-5a) hanya menampilkan satu  layar di mana tertera nama, nomor telepon dan alamat. Demikian juga aplikasi [Dadu](https://github.com/sslaia/dadu_app/blob/pertemuan-6/lib/main.dart) serta aplikasi [Burung Nias](https://github.com/sslaia/burung_nias/blob/pertemuan-7/lib/main.dart) dan tentu saja aplikasi Gogowaya dan Towi-Towi di atas.

Namun dalam hidup nyata selalu ada saja skenario di mana kita perlu membuka layar baru untuk menampilkan konten yang berbeda dari layar sebelumnya. Dan kenyataannya hampir semua aplikasi menggunakan sekurang-kurangnya dua layar, kalau tidak lebih.

Untuk belajar mekanisme pembuatan layar berbeda ini, kita menggunakan panduan dari Google berjudul [Navigate to a new screen and back](https://flutter.dev/docs/cookbook/navigation/navigation-basics) dan menggunakan pengetahuan itu untuk memodifikasi aplikasi [Gogowaya](https://github.com/sslaia/gogowaya) sehingga dengan mengetuk satu item, detail dari item tsb. ditampilkan di layar baru.

Pada akhir sesi kita hari ini, demikian nanti hasil akhir aplikasi ![Aplikasi Gogowaya](./gogowaya/gogowaya2.jpg?raw=true)


## Langkah 1: Membuat aplikasi baru
1. Buat aplikasi baru dengan **File** > **New** > **New Flutter project**
2. Biarkan saja nama yang ada dan tekan tombol **Finish**


## Langkah 2: Kosongkan berkas main.dart

1. Buka berkas **main.dart**
2. Hapus baris 32 sampai habis (baris 116), sehingga tinggal baris 1-31.
3. Ganti argumen title di baris 14 menjadi: 'Navigasi ke layar lain' (jangan lupa mengapit _string_ ini dalam tanda petik!)
4. Ubah baris 27 menjadi seperti berikut:
```
      home: LayarPertama(),
    );
  }
}

```

Untuk sementara abaikan tanda kesalahan (_error_) di LayarPertama() tsb, karena memang kelas LayarPertama() masih harus diciptakan.

## Langkah 3: Menyisipkan kode contoh

1. Kopi kode yang telah dipersiapkan berikut dengan menekan tombol ikon kopi di sebelah kanan atas blok kode berikut:
```
class LayarPertama extends StatelessWidget {
  const LayarPertama({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Layar pertama'),
      ),
      body: Center(
        child: ElevatedButton(
          child: const Text('Buka layar kedua!'),
          onPressed: () {
            // Tulis di sini kode untuk pergi ke layar kedua
            // bila tombol "Buka layar kedua!" ditekan
          },
        ),
      ),
    );
  }
}

class LayarKedua extends StatelessWidget {
  const LayarKedua({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Layar kedua"),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Tulis di sini kode untuk pergi ke layar pertama
            // bila tombol "Kembali ke layar pertama!" ditekan
          },
          child: const Text('Kembali ke layar pertama!'),
        ),
      ),
    );
  }
}
```

## Langkah 4: Mengamati kode

Mari mengamati kode yang baru kita sisipkan tsb. Kita melihat ada dua klas, LayarPertama dan LayarKedua. Keduanya merupakan StatelessWidget. Demikian juga badan (_body_) kedua kelas itu menggunakan pola yang telah kita kenal: menggunakan widget Center(), kemudian tombol widget ElevatedButton(). Di sini widget tombol digunakan, untuk memungkinkan interaksi, sehingga bila kita menekan tombol tsb. aksi tertentu bisa dijalankan (kode yang ada di dalam badan onPressed).

Tetapi ada perbedaan yang bisa gampang terlewati, yakni keduanya menggunakan widget **Scaffold** dan **AppBar**. Dan kita tahu bahwa widget Scaffold merupakan kerangka bangunan satu aplikasi dan karena itu kita merasa wajar kelas **LayarPertama** memiliki widget ini.

Namun mengapa LayarKedua juga memiliki widget Scaffold? Bukan hanya itu kelas ini juga memiliki widget baris judul AppBar sendiri! Nah ini tanda bahwa LayarKedua membangun kerangka sendiri, seolah merupakan aplikasi baru, namun dalam konteks ini hanya merupakan layar kedua dalam aplikasi yang sama.

Pertanyaannya sekarang, bagaimana bergerak dari LayarPertama ke LayarKedua tsb. Soalnya LayarKedua itu telah merupakan layar independen dari LayarPertama. Di Flutter gerakan ini dinamakan _navigation_ dan rutenya disebut _route_.

## Langkah 5: Mengenal navigasi di Flutter

Jadi sebenarnya yang terjadi adalah, dengan membuat kelas LayarPertama dan LayarKedua tsb. kita telah menciptakan rute pergerakan.

Nah untuk melompat ke rute baru, Flutter menggunakan metode **Navigator.push()**. Navigator itu bertugas mengelola berbagai rute yang ada. Kita bisa menambah rute baru dengan menjalankan metode push() di Navigator tsb.

Mari mengintegrasikan hal ini dalam kode kita tadi. Kita mau bahwa setiap kali pengguna mengetuk tombol **Buka layar kedua!**, kita menambahkan satu rute baru menuju ke LayarKedua. Karena itu kita sisipkan perintah berikut di baris 46 (badan onPressed()). Pastikan untuk tidak menghapus tanda } di baris 47!
```
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => LayarKedua()),
            );

```

Aplikasi ini telah berfungsi. Anda bisa mencoba pergerakan dari layar pertama ke layar kedua dan sebaliknya dengan menjalankan aplikasi. Jadi silakan menjalankan aplikasi tsb.

Nanti secepat pengguna mengklik tombol tsb. LayarKedua terbuka, seperti bisa dilihat dalam gambar berikut.

![Layar kedua](./pertemuan9/layarkedua.jpg?raw=true)
 
Perhatikan bahwa secara otomatis Navigator telah menolong kita meletakkan ikon tanda panah ke kiri (nomor 1) untuk memungkinkan pengguna kembali ke layar sebelumnya.

Mungkin Anda perhatikan bahwa tombol "Kembali ke layar pertama!" tidak menghasilkan apa-apa. Yah, selain tombol ini panah balik di baris judul, kita bisa juga bergerak balik ke layar sebelumnya secara programatis, artinya dengan menuliskan kodenya dalam salah satu widget di dalam tubuh aplikasi, mis dalam aplikasi ini dalam tombol ElevatedButton Kembali ke layar pertama. Maka marilah menambahkan kode tsb.

Cari bagian onPressed di kelas LayarKedua (di baris 69) dan sisipkan kode berikut setelah baris 71 (perhatikan untuk tidak menghapus tanda } di baris 72!):
```
              Navigator.pop(context);
```

Wah, begitu sederhana, bukan? Kita tinggal menjalankan metode pop() di Navigator. Sekalian kita sertakan parameternya context, artinya masih dalam konteks navigasi dari LayarPertama ke LayarKedua tadi! Ini penting sekali, kalau tidak metode pop() tidak tahu yang mana.

Sekarang jalankan aplikasi tsb. dan Anda akan melihat bahwa tombol itu kini berfungsi dan bila kita menekannya Navigator akan membawa kita ke layar pertama.

**Bonus:** secara otomatis Flutter menyediakan animasi gerakan dari layar pertama dan layar kedua serta animasi tombol. Coba tekan dan tahan tombol tsb. maka Anda akan melihat riak kecil bagaikan gelombang ombak menyebar ke segala arah.
Demikian juga peralihan antar layar, seperti sebuah animasi slide presentasi!

## Memodifikasi aplikasi Gogowaya untuk membuka layar kedua

Nah, mari menerapkan pengetahuan yang baru kita pelajari ini di aplikasi Gogowaya yang kita buat kali lalu (dan hal yang sama bisa diterapkan pada aplikasi Towi-Towi yang kita buat minggu lalu).

Sekarang kita ingin supaya bila kita mengklik satu item di dalam aplikasi Gogowaya, layar kedua akan dibuka di mana kita menampilkan detil dari item tsb.

## Langkah 1: Buka aplikasi Gogowaya

1. Buka aplikasi Gogowaya entah melalui **File > Open** atau melalui **File > Open recent > Gogowaya**
2.  Pastikan supaya baris 14 tidak menjadi komentar (tak ada tanda // di depannya), sedangkan baris 15 menjadi komentar (ada tanda // di depannya).
3. Jalankan aplikasi untuk memastikan bahwa semua berjalan baik.

## Langkah 2: Ciptakan kelas layar kedua

1. Buka aplikasi yang tadi kita buat dan kopi semua kode mulai dari baris 58 berisi kelas LayarKedua.
2. Kembali ke berkas main.dart dari aplikasi Gogowaya, pergi ke akhir berkas, dan klik untuk meletakkan penunjuk mouse di baris paling akhir. Tekan Enter beberapa kali.
3. Di baris 126 sisipkan blok kode LayarKedua, yang kita kopi dari aplikasi sebelumnya.

## Langkah 3: Buat rute di daftar foto Gogowaya

Kita tahu bahwa di halaman utama Gogowaya kita melihat satu daftar panjang. Setiap item ditampilkan dalam sebuah kartu. Kita ingin supaya setiap kali kita mengklik salah satu item tsb. halaman rincian dari item itu terbuka di layar baru.

Cobalah mengidentifikasi di mana kode untuk menampilkan item-item tsb. berada. Kita melihat bahwa kali lalu kita menggunakan widget **ListTile** untuk menampilkan item-item foto (baris 116-119).

Widget **ListTile** memiliki fungsi untuk meregister entah kita menekan salah satu item di dalam daftar yang ditampilkannya. Kali lalu kita belum memanfaatkan kemungkinan ini. Marilah sekarang memanfaatkannya:

1. Klik di akhir baris 119 (baris _subtitle_, kalau di tempat Anda hal ini berada di baris lain silakan menyesuaikannya) lalu buat garis baru dengan menekan Enter.
2. Silakan mulai mengetik **on** dan dalam jendela yang terbuka Anda melihat beberapa opsi, pilihlah **onTap**.
3. Dari aplikasi yang kita buat tadi, kita tahu bahwa kita perlu menggunakan metode push di Navigator. Maka gantilah keseluruhan baris onTap tadi di baris 120 dengan kode berikut sehingga akan menjadi sbb:

```
              onTap: () {
                Navigator.push(
                    context,
                    MaterialPageRoute(builder: (context) => LayarKedua()));
              },

```
Singkatnya persis sama dengan baris kode yang kita gunakan dalam aplikasi sebelumnya.

4. Coba simpan dengan menekan tombol Ctrl+S dan cobalah sekarang menekan salah satu item di daftar foto tsb. Halaman layar kedua dibuka dan kita bisa kembali ke daftar itu lagi.

Bagus sekali. Kita sudah berhasil menciptakan rute ke layar baru! Sekarang tinggal menambah kode sehingga yang ditampilkan di layar kedua tsb. adalah rincian dari item yang kita tekan.

## Langkah 4: Memutuskan hal apa yang ditampilkan di layar kedua

Sekarang kita harus memutuskan detil apa saja dari item yang ditekan, yang akan ditampilkan di layar kedua. Untuk membuatnya sederhana, marilah menggunakan satu detil saja, artinya hanya menampilkan foto tsb. tanpa nama dan rincian lainnya.

Nah, kalau kita bernavigasi dari satu layar ke layar berikut kita bisa menyeretakan parameter dengan argumennya di dalam tanda kurung kelas tujuan. Karena kita hanya mau menampilkan foto itu saja, maka kita hanya perlu memasukkan parameter foto dan argumennya adalah alamat foto tsb.

Kita tahu dari aplikasi gogowaya bahwa kita telah menyimpan akses ke dalam setiap item di daftar foto di dalam variable photo di baris 111. Variable tsb. menyimpan informasi item mana yang sedang ditampilkan di indeks mana.

Yang akan kita buat adalah memberi nama satu parameter mis. foto, lalu argumen kita ambil dari variable photo tadi dengan mengakses alamat Internetnya (url).

1. Pergi ke baris 123 di mana kita tadi mendefinisikan navigasi ke layar kedua. 
2. Sisipkan parameter foto dengan argumen photo.url

Sekarang kita telah menyertakan informasi alamat foto ke layar kedua. Tetapi kita masih perlu memberitahu LayarKedua bahwa ada informasi yang disertakan dan nama parameternya adalah foto. Maka
3. Sisipkan kode ini di belakang key di baris 132: `required this.foto`
4. Sisipkan baris berikut misalnya di baris 134:
```
  final String foto;
```
Sekarang kita siap menggunakan alamat tsb. untuk menampilkan foto.
5. Ganti seluruh widget Text di baris 150 dengan widget Image.network dan masukkan foto, yang baru kita terima dari layar pertama tadi, sebagai argumennya. Keseluruhan baris 150 akan tampak sbb.:
```
          child: Image.network(foto),

```

Sekarang simpan berkas (dengan menekan tombol Ctrl+S) lalu cobalah seakrang menekan salah satu item di daftar foto itu, maka layar baru akan dibuka dimana foto tsb. ditampilkan.

Selesai! Bertepuk tanganlah. Anda telah banyak mencapai hal hari ini!



Tambahan kalau ada waktu.

## Memasang icon/launcher untuk aplikasi

Mungkin Anda telah mengamati bahwa setiap aplikasi yang kita buat selama ini selalu tampil dengan icon yang sama di dalam smartphone/emulator, yakni logo Flutter. Bagaimana memasang satu logo yang kita buat sendiri mis. untuk aplikasi Gogowaya? 

Sebagai latihan pilihlah salah satu foto, yang ukurannya 512x512 pixel. Bila Anda belum punya foto yang cocok, Anda bisa menggunakan gambar contoh yang ada di  folder [Gogowaya](https://github.com/sslaia/belajar_flutter/tree/main/gogowaya) (namanya gogowaya.png)

Setelah memiliki foto yang bisa kita gunakan sebagai logo, silakan mengikuti langkah-langkah berikut:

1. Kunjungi situs [Android Asset Studio](https://romannurik.github.io/AndroidAssetStudio/index.html)
2. Klik di **Launcher icon generator**
3. Di sebelah kiri atas ada bagian **Foreground**. Klik di **Image**
4. Di jendela Explorer yang terbuka, pilihlah foto (gogowaya.png) atau logo yang telah dipersiapkan tadi.
5. Lihat bagian Padding dan atur besar foto sedemikian sehingga memuaskan. Saya misalnya memasang 0% padding.
6. Tekan icon download di sudut kanan atas, beri nama mis. gogowaya.zip dan simpan di tempat yang Anda bisa temukan nanti, misalnya di folder Downloads
7. Buka berkas gogowaya.zip tsb.
8. Buka folder res di dalamnya
9. Blok semua isinya dan kopi (melalui tombol kanan mouse)

Sekarang pastikan aplikasi Gogowaya telah terbuka di Android Studio

1. Di bagian Project, buka folder android > app > src > main > res
2. Klik di folder res tsb dan sisipkan ke dalam femua foto dari berkas gogowaya.zip yang kita kopi tadi (dengan menekan tombol kanan mouse akan muncul berbagai menu, termasuk paste). Iyakan untuk menindih semua berkas yang telah ada.
3. Selesai!


## Referensi

- [Navigate to a new screen and back](https://flutter.dev/docs/cookbook/navigation/navigation-basics) 
- Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)
- Berbagai dokumentasi, contoh, tutorial dlsb. ada di [https://flutter.dev/docs](https://flutter.dev/docs)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

