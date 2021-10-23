# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Membuat formulir memasukkan data

Ada dua widget yang dapat digunakan untuk membuat formulir di Flutter, yakni widget **TextField** dan **TextFormField**. Widget mana yang dipilih tergantung dari kebutuhan aplikasi. Formulir tertentu hanya membutuhkan sarana meng-input data dan karena itu cukup menggunakan widget **TextField**, sedangkan formulir lain yang menuntut validasi membutuhkan widget **TextFormField**, yang memiliki fungsi validasi tsb.

Kode untuk membuat formulir ini akan diletakkan dalam berkas baru bernama **homepage.dart**, sehingga berkas main.dart tidak bertambah ramai, sementara di berkas baru kita bisa mengamati perkembangan penulisan kode langkah demi langkah.

## Langkah 1: Membuat berkas baru

1. Buka **alasa_app** di **AS** (Android Studio).
2. Buat berkas baru bernama **home_page.dart** di dalam folder **lib** dengan mengklik folder lib, lalu dengan menekan tombol kanan mouse, pilih dari jendela yang terbuka **New**, lalu **Dart file**.
3. Masukkan nama berkas: home_page.dart dan tekan tombol Enter. Satu berkas kosong akan terbuka di hadapan kita.

## Langkah 2: Membuat widget StatefulWidget

1. Dalam berkas home_page.dart mulailah ketik **st**. Tidak lama kemudian muncul jendela kecil di mana terdapat berbagai pilihan. Pilihlah **stful** yang akan menggenerasi kode StatefulWidget.
2. Langsung ketiklah **HomePage** dan **AS** membantu menyesuaikan berbagai nama yang diperlukan. Anda akan mendapatkan kode seperti berikut:

```
class HomePage extends StatefulWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

3. Klik sekali di tempat lain, sampai tanda blok mouse di tempat kata HomePage itu terlepas.
4. Letakkan **cursor** di kata **StatefulWidget** dan klik sekali. Lalu tekan tombol kanan mouse dan pilih **Show Context Actions** kemudian dari jendela kecil yang muncul pilih **import library 'package:flutter/material.dart'** Anda akan melihat `import library 'package:flutter/material.dart'` disisipkan di baris pertama. Di sini kita mengimpor pustaka material.dart, yang mengandung berbagai standar desain aplikasi, sehingga aplikasi yang kita tulis nanti tampil _nativ_ di smartphone dan tidak terasa aneh. 

Dengan demikian widget StatefulWidget, yang selalu terdiri dari sepasang kelas, telah disisipkan di dalam berkas. Kelas pertama tak perlu disentuh dan kita tidak akan menulis kode apa pun di situ. Semua kode yang kita tulis akan masuk di kelas kedua, di baris setelah `class _HomePageState extends State<HomePage> {` (pada baris 10 di berkas saya).

## Langkah 3: Membuat kontroler

Untuk bisa merekam apa yang dimasukkan pengguna dalam tempat isian di formulir nanti, kita menggunakan layanan kontroler (namanya **TextEditingController**), yang selalu siap merekam data apa yang dimasukkan. Kita membutuhkan kontroler untuk masing-masing tempat isian. Untuk itu pertama-tama kita mendefinisikan berbagai variable yang sesuai. Sisipkanlah baris-baris berikut setelah baris 10 di atas.
```
  final namaController = TextEditingController();
  final margaController = TextEditingController();
  final emailController = TextEditingController();
  final teleponController = TextEditingController();
  final pendidikanController = TextEditingController();
  final tanggalLahirController = TextEditingController();
```

Karena kontroler ini selalu aktif memonitor tempat isian di formulir, itu berarti dia juga selalu memblok satu tempat di memory smartphone. Karena itu supaya memory smartphone senantiasa dibebaskan secepat satu operasi berjalan, maka kontroler di atas perlu dibuang/dihentikan. Untuk itu sisipkan baris-baris kode berikut setelah kode-kode di atas:
```
  @override
  void dispose() {
    namaController.dispose();
    margaController.dispose();
    emailController.dispose();
    teleponController.dispose();
    pendidikanController.dispose();
    tanggalLahirController.dispose();
    super.dispose();
  }
```

Sekarang kita siap membuat formulir. Namun sebelum itu kita perlu meletakkan fondasi pohon widget, di atasnya kita membuat formulir.

## Langkah 4: Menyiapkan fondasi

Pergi ke baris 31 di baris kode `return Container();` Baris ini otomatis dibuat waktu generasi StatefulWidget sebagai _placeholder_, tempat untuk memasukkan widget baru.

1. Ganti `Container();` dengan `Scaffold();` Kini kita siap membangun pohon widget, setelah fondasi, menyusul `appBar` dan `body`.
2. Letakkan cursor di antara tanda kurung dari Scaffold() dan tekan Enter (pastikan untuk tidak menghapus tanda kurung penutup dan titik koma di akhir.
3. Tulis kode untuk memasang baris judul aplikasi dengan `appBar: AppBar(title: const Text('Formulir memasukkan data'),),` Sekarang kita siap mem-populasi badan aplikasi (_body_) dengan kode.


## Langkah 5: Membuat formulir

Seperti dikatakan sebelumnya, untuk membuat formulir kita menggunakan widget **TextField**.

1. Sisipkan baris kosong setelah baris kode dari no. 3 di atas, lalu tulis `body: TextField(),` Widget **TextField** memiliki dua parameter dasar yang bisa digunakan, yakni _controller_ dan _decoration_. Yang pertama memberitahu kontroler mana digunakan untuk merekam data yang dimasukkan di tempat masukkan formulir. Yang kedua sekadar dekorasi, untuk membuat supaya tempat masukkan tsb. lebih menarik.
2. Letakkan cursor di dalam tanda kurung di TextField lalu tekan Enter sekali. Kini kita siap memasukkan argumen untuk kedua parameter tsb. tadi.
3. Sisipkan baris kode kontroler berikut `controller: namaController,` tekan Enter.
4. Sisipkan baris kode dekorasi berikut
```
        decoration: InputDecoration(
            hintText: "Nama Anda",
            hintStyle: const TextStyle(color: Colors.black26),
            border: OutlineInputBorder(
                borderRadius: BorderRadius.circular(8))),
```

Dari kode dekorasi tsb. kita bisa segera tahu, hintText pastilah teks yang tampil di dalam tempat masukkan untuk memberi indikasi kepada pengguna apa yang harus dimasukkan di tempat tsb.

Sedangkan baris kode berikutnya hanyalah sekadar stil warna dan stil garis sekeliling tempat masukkan.

Sebelum kita maju, kita mau melihat bagaimana formulir ini tampil di layar smartphone. Karena itu simpanlah perubahan ini dengan menekan secara bersama tombol **Ctrl+S** atau dari File > Save all.

## Langkah 6: Melihat formulir

1. Buka berkas **main.dart** dan pergi ke baris 28 di mana tertulis "home: const MyHomePage(title: 'Aplikasi Alasa'),"
2. Ganti keseluruhan baris itu sehingga menjadi: `home: const HomePage(),` Anda akan melihat bahwa kata HomePage digarisbawahi merah.
3. Letakkan cursor di kata HomePage tsb lalu tekan sekaligus tombol Alt+Enter.
4. Di jendela kecil akan muncul pilih "import library 'package:alasa_app/home_page.dart'"
5. Pastikan emulator telah jalan. Kalau tidak pilihlah emulator yang ada (kemungkinan besar Pixel 2). Tunggu sampai emulator siap. **Catatan**: Anda tak perlu melakukan hal ini bila Anda langsung menggunakan smartphone Anda.
5. Tekan tombol **Run** (tombol tanda panah hijau di baris atas) untuk menjalankan aplikasi ini. Tunggu sampai proses kompilasi (_assemble_) selesai. Nanti Anda akan melihat formulir tampil di layar emulator.


## Langkah 7: Meneruskan pembuatan formulir

Sebelum kita teruskan, kita perlu memikirkan beberapa hal, karena akan menentukan bagaimana kita menampilkan keseluruhan formulir di layar.

Pertama, seperti kita bisa lihat di layar emulator, tempat isian tsb. memenuhi seluruh layar dari kiri ke kanan. Hal ini tentu saja tidak menarik. Oleh karena itu dibutuhkan sedikit spasi baik di sebelah kiri maupun di sebelah kanan. Itu berarti kita akan menggunakan widget **Padding** untuk itu.

Kedua, tempat isian lebih dari satu. Itu berarti kita butuh satu widget yang bisa menjajarkan tempat isian tsb. dari atas ke bawah. Untuk itu kita akan menggunakan widget **Column**.

Ketiga, tempat isian lumayan banyak, sehingga semuanya tidak akan muat sekaligus di layar. Karena itu harus ada kemungkinan untuk menggeser isi ke atas dan ke bawah (bahasa Inggris, _scroll_). Untuk itu kita akan menggunakan widget **SingleChildScrollView**, yang memungkinkan _scrolling_ konten.

Keempat, supaya ada sedikit jarak antara tempat isian yang satu dengan yang lain, perlu menggunakan widget **SizedBox**. 

Dengan berbekal berbagai hal kita siap merampungkan formulir kita.

1. Letakkan cursor dan klik sekali di **TextField**. Klik di bola lampu, yang muncul di sebelah kiri, lalu pilih `Wrap with Column` (poin kedua di atas)
2. Letakkan cursor dan klik sekali di **Column**. Klik di bola lampu, yang muncul di sebelah kiri, lalu pilih `Wrap 
with Widget`
3. Ganti kata widget yang otomatis disisipkan menjadi **SingleChildScrollView** (poin ketiga di atas)
4. Letakkan cursor dan klik sekali di **SingleChildScrollView**. Klik di bola lampu, yang muncul di sebelah kiri, lalu pilih `Wrap 
with Padding` (poin pertama di atas)
5. Ganti nilai 8.0 yang otomatis disisipkan di situ, menjadi 32.0.
6. Sekarang pergi ke akhir baris 45 (di akhir ada tanda kurung dan koma, jadi merupakan penutup dari TextField) tekan sekali Enter lalu sisipkan kode berikut: `SizedBox(height: 8.0),` (jangan lupa tanda koma di belakangnya).


Karena kita tahu bahwa kode setiap tempat isian (TextField) pasti sama, hanya _hintText_ dan nama kontroller yang beda, maka untuk mempermudah, kita tinggal meng-kopi keseluruhan kode **TextField(),** dan sekalian **SizedBox()** lalu menggandakannya sebanyak tempat isian yang kita butuhkan (dalam hal ini lima kali).

7. Kopi keseluruhan **TextField** termasuk **SizedBox** (artinya dari baris 38 s/d 46, termasuk juga tanda koma!) dan sisipkan sebanyak lima kali setelah baris 46.
8. Sesuaikan nama kontroller dan hintText. Nama kontroller tempat isian kedua misalnya adalah margaController dan hintText-nya "Marga Anda". Teruskan dengan keempat tempat isian lainnya.

Bila Anda menyimpan apa yang telah Anda kode, maka keseluruhan formulir tsb kini telah bisa tampil di emulator.

Tinggal satu tahap lagi yang perlu, yakni membuat tombol "Kirim", yang akan mengirim data yang dimasukkan ke database. Untuk itu kita menggunakan widget **ElevatedButton**

9. Setelah **SizedBox** terakhir (baris 91) sisipkan satu baris kosong (perhatikan supaya tanda koma di akhir baris 82 tidak terhapus! Masukkan kode berikut:
```
              ElevatedButton(
                onPressed: () {
                  print('Data telah dikirim');
                },
                child: Text('Kirim'),
              ),
```

Dalam kode itu ada bagian onPressed, yang mengatakan, bila pengguna menekan tombol "Kirim" maka cetaklah kalimat "Data telah dikirim". Tentu saja nanti kalau kita telah membuat database, kode yang akan ditempatkan di situ adalah kode untuk mengirim data yang telah dimasukkan dalam formulir ke database.

Keseluruhan kode bagian formulir ini nampak sbb.:

```
      body: Padding(
        padding: const EdgeInsets.all(32.0),
        child: SingleChildScrollView(
          child: Column(
            children: [
              TextField(
                controller: namaController,
                decoration: InputDecoration(
                    hintText: "Nama Anda",
                    hintStyle: const TextStyle(color: Colors.black26),
                    border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8))),
              ),
              SizedBox(height: 8.0),
              TextField(
                controller: margaController,
                decoration: InputDecoration(
                    hintText: "Marga Anda",
                    hintStyle: const TextStyle(color: Colors.black26),
                    border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8))),
              ),
              SizedBox(height: 8.0),
              TextField(
                controller: emailController,
                decoration: InputDecoration(
                    hintText: "Email Anda",
                    hintStyle: const TextStyle(color: Colors.black26),
                    border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8))),
              ),
              SizedBox(height: 8.0),
              TextField(
                controller: teleponController,
                decoration: InputDecoration(
                    hintText: "Telepon Anda",
                    hintStyle: const TextStyle(color: Colors.black26),
                    border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8))),
              ),
              SizedBox(height: 8.0),
              TextField(
                controller: pendidikanController,
                decoration: InputDecoration(
                    hintText: "Pendidikan terakhir Anda",
                    hintStyle: const TextStyle(color: Colors.black26),
                    border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8))),
              ),
              SizedBox(height: 8.0),
              TextField(
                controller: tanggalLahirController,
                decoration: InputDecoration(
                    hintText: "Tanggal lahir Anda",
                    hintStyle: const TextStyle(color: Colors.black26),
                    border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(8))),
              ),
              SizedBox(height: 8.0),
              ElevatedButton(
                onPressed: () {
                  print('Data telah dikirim');
                },
                child: Text('Kirim'),
              ),
            ],
          ),
        ),
      ),

```

Keseluruhan kodenya bisa dilihat di [Aplikasi Alasa](https://github.com/sslaia/alasa_app/tree/membuat_formulir2). Silakan bandingkan kode Anda dengan kode di sana.


Selesai!


[Kembali ke Menu Utama](./alasa_app.md)
