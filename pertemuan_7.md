# Belajar Bersama Flutter

Pertemuan 7, 2 September 2021


## Merangkum kembali apa yang telah dipelajari kali lalu

Kali lalu kita telah membuat aplikasi dadu dengan mengelaborasi widget Button serta GestureDector, yang memungkinkan interaksi dengan aplikasi.

Hari ini kita memperluas interaksi ini dengan menggunakan daftar. Untuk itu kita akan menciptakan aplikasi [Burung Nias](https://github.com/sslaia/burung_nias/blob/main/lib/main.dart).
 

## Langkah 1: Membuat aplikasi baru
1. Buat aplikasi baru dengan File > New > New Flutter project
2. Beri nama burung_nias dan tekan tombol Finish

## Langkah 2: Hapus semua komentar

1. Buka berkas main.dart
2. Hapus semua baris yang dimulai dengan tanda //. Perhatian: Jangan hapus baris yang komentarnya (//) di tulis di belakang baris!

## Langkah 3: Pastikan aplikasi jalan

1. Jalankan aplikasi dengan menekan tombol Run (icon tanda panah hijau)

## Langkah 4: Mengerti logika counter dalam aplikasi ini

Aplikasi ini merekam berapa kali pengguna menekan tombol berlabel tambah dan menampilkan angka tsb. di widget Text.

Bagaimana aplikasi mengetahui bahwa pengguna telah tombol tambah? Itu fungsi built-in dari berbagai Button seperti FloatingActionButton dalam contoh ini.

Bagaimana membuat bahwa setiap pengguna menekan tombol tsb. angka bertambah satu?

Untuk itu dibutuhkan satu fungsi, yakni `_incrementCounter()`. Dengan menggunakan variable `_counter` kita menyimpan nilai yang telah ditambahkan berdasarkan berapa kali pengguna telah menekan tombol. Variable ini pertama diberi nilai 0, lalu bertambah satu setiap kali tombol ditekan, dan itu dibuat dengan menggunakan kalkulasi `_counter++` (sama dengan `_counter = counter + 1`).

Setelah mendapatkan nilai `_counter` tsb aplikasi menampilkannya di layar di widget `Text('$_counter')`

## Langkah 5: Membuat supaya burung Nias ditampilkan

Sekarang kita memanfaatkan `_counter` ini untuk menampilkan nama burung Nias. Untuk itu kita membutuhkan satu daftar (list) yang berisikan nama-nama burung Nias.

1. Buat satu daftar dengan nama 10 burung Nias
```
List<String> _burungNias = ["Beo", "Buru'u", "Magio", "Nagoyomanase", "Towi-towi", "Nazese", "Gogowaya", "Miti-miti", "Siliŵi", "Boroa"];
```
2. Buat satu variable menyimpan nama burung pilihan tergantung angka dari `_counter`. Untuk tampilan awal saat aplikasi pertama kali dijalankan tampakkan burung dalam posisi indeks 0
```
String _burungPilihan = "Beo";
```
3. Ganti isi widget Text `'You have pushed...'` menjadi seperti di bawah ini, simpan dan jalankan aplikasi untuk melihat hasilnya di layar.
```
            Text(
              'Burung pilihan Anda: $_burungPilihan',
            ),
```

Seperti Anda lihat nama burung belum tampil. Bagaimana membuat supaya nilai `_counter` itu berpadanan dengan nomor indeks dalam daftar burung Nias? Misalnya angka 2, berarti menampilkan nama burung dari daftar dalam posisi 1 (ingat cara komputer menghitung dari 0!)

Kita tahu angka saat ini disimpan dalam variable `_counter` dan daftar dalam variable `_burungNias`. Maka kita bisa mengakses nama burung dalam daftar tsb dengan cara `_burungNias[_counter]`!

Untuk menyimpan nama burung aktual sesuai dengan angka `_counter` kita butuh variable yang bisa kita beri nama `_burungPilihan`. Kodenya menjadi seperti di bawah ini dan kita tempatkan dalam badan `setState()` supaya nilai baru tsb diregister dalam seluruh aplikasi.
```
    setState(() {
      _counter++;
      _burungPilihan = _burungNias[_counter];
    });
```
Pastikan variable `_burungPilihan` berada setelah `_counter` mendapatkan nilai baru!

Sekarang jalankan aplikasi dan lihat hasilnya di layar. Kini nama burung dari daftar telah tampil di layar.

## Langkah 6: Membuat supaya daftar kembali ke awal

Bila Anda meneruskan menekan tombol tambah, pada suatu saat aplikasi _crashed_, karena nilai `_counter` telah melebihi jumlah item di dalam daftar.

Bagaimana membuat supaya setelah mencapai angka maksimum jumlah item dalam daftar mulai lagi dari nol?

Untuk itu kita harus menciptakan satu kondisi, yang bunyinya kira-kira sebagai berikut: jika angka `_counter` lebih kecil dari angka maksimum jumlah item di dalam daftar maka tampilkan item di posisi indeks angka. Namun bila lebih dari situ, buat nilai `_counter` nol.

Bagaimana menerjemahkan hal ini dalam kode Dart/Flutter? Kita bisa menerjemahkannya sbb.:
```
      if (_counter < _burungNias.length) {
        _burungPilihan = _burungNias[_counter];
      }
      else {
        _counter = 0;
        _burungPilihan = _burungNias[_counter];
      }
```

**Catatan:** di Python kita mendapat jumlah item dalam daftar melalui fungsi len(). Di Dart/Flutter dengan menggunakan metode length yang digandengkan pada nama variable daftar.

Jalankan kembali aplikasi tsb. dan lihat hasilnya.
 
## Langkah 7: Menampilkan nama burung di tempat angka

Ini cukup mudah, tinggal memindahkan variable `$_burungPilihan` ke widget Text yang kedua, sehingga menjadi:
```
            Text(
              'Burung pilihan Anda:',
            ),
            Text(
              '$_burungPilihan',
              style: Theme.of(context).textTheme.headline4,
            ),
```


## Langkah 8: Membuat supaya ada tombol maju atau mundur dalam daftar

Kali lalu kita telah menggunakan tombol yang mirip untuk ini, yakni **ElevatedButton**. Karena itu di bawah widget **Text** sisipkan widget **ElevatedButton**.

Anda akan melihat bahwa secepat Anda mengetik ElevatedB muncul di jendela kecil ElevatedButton. Jadi tinggal menekan Enter dan otomatis ElevatedButton lengkap dengan parameternya disisipkan di letak di mana kursor mouse berada. Masukkan `_incrementCounter` sebagai nilai parameter `onPressed` dan sebagai `child` masukkan `Text('<')

Kita membutuhkan dua tombol satu untuk maju dan satu untuk mundur. Jadi tinggal menggandakan widget ElevatedButton tadi.

Kodenya menjadi: 
```
            ElevatedButton(onPressed: _incrementCounter, child: Text('<'),),
            ElevatedButton(onPressed: _incrementCounter, child: Text('<'),),
```

Jalankan aplikasi untuk melihat hasilnya.

## Langkah 9: Membuat supaya kedua tombol sejajar kiri dan kanan

Ini gampang saja. Kita hanya perlu memasukkan keduannya ke dalam widget **Row**. Ada yang masih ingat bagaimana caranya?

Klik sekali di widget **ElevatedButton** yang pertama dan letakkan kursor di atasnya sampai fungsi bola lampu muncul. Pilih widget **Row**. Otomatis tombol tsb. diapit dan menjadi salah satu children dari widget Row.

Kini tinggal memindahkan widget ElevatedButton yang kedua menjadi anak widget Row juga.

Jalankan aplikasi. Masih ada yang perlu dilakukan bukan? Pertama membuat ruang di antara keduanya (bisa menggunakan widget SizedBox) dan kedua meluruskannya di tengah-tengah dengan menggunakan parameter _mainAxisAlignment_. Kodenya menjadi:
```
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                ElevatedButton(onPressed: _incrementCounter, child: Text('<'),),
                SizedBox(width: 50,),
                ElevatedButton(onPressed: _incrementCounter, child: Text('>'),),
              ],
            ),
```

Jalankan kembali aplikasi tsb. Kini tampilannya lebih bagus.

## Langkah 10: Membuat fungsi mundur (menghitung turun)

Sampai saat ini kedua tombol itu menghasilkan fungsi yang sama, yakni menghitung ke atas atau maju dalam daftar nama burung. Karena untuk kedua tombol kita menggunakan fungsi yang sama yakni `_incrementCounter`

Bagaimana membuatnya menghitung mundur? Gampang sekali. Tinggal mengkopi fungsi `_incrementCounter` dan mengubah penghitungan `_counter_` dari menghitung maju menjadi menghitung mundur. Kita memberi namanya `_decrementCounter`. Kodenya menjadi:
```
  void _decrementCounter() {
    setState(() {
      _counter--;

      if (_counter >= 0) {
        _burungPilihan = _burungNias[_counter];
      }
      else {
        _counter = _burungNias.length - 1;
        _burungPilihan = _burungNias[_counter];
      }
      // _counter--;
      // _burungPilihan = _burungNias[_counter];
    });
  }
```
Sekarang tinggal menukar parameter onPressed dari tombol ElevatedButton yang menghitung mundur menjadi `_decrementCounter`. Jalankan aplikasi dan semua berjalan baik sekarang.

## Langkah 11: (Opsional) Membuat jarak antara widget

Hal ini optional, hanya menyangkut pandangan optikal saja. Misalnya perlu memberi jarak antara kedua widget Text dan antara widget Text dan Row di mana ada kedua tombol. Gunakanlah widget SizedBox() untuk itu.


## Langkah 12: (Opsional) Membuat tombol sembarang (random)


Kita ingin bahwa setiap kali tombol **FloatingActionButton** ditekan, kita mendapatkan angka sembarang yang akan menjadi nomor indeks dari item di dalam daftar nama burung. Bagaimana mewujudkan hal ini?

Kali lalu kita telah menggunakan modul Random, jadi di sini pun kita bisa menggunakannya. Jadi

1. Kita membuat fungsinya misalnya dengan nama `_sembarangBurung`, selebihnya mirip fungsi `_incrementCounter`. Kodenya menjadi:
```
  void _sembarangBurung() {
    setState(() {
      _counter = Random().nextInt(9) + 1;
      _burungPilihan = _burungNias[_counter];
    });
  }
```
Lebih gampang daripada yang kita duga, bukan? Sekarang modul random tsb ditandai merah, karena masih harus diimpor. Klik sekali di kata Random tsb. lalu tekan bersamaan tombol Alt+Enter 
lalu pilih `import library 'dart:math'`
2. Tukar nilai parameter onPressed dari FloatingActionButton menjadi `_sembarangBurung`
3. (Opsional) Tukar icon tombol FloatingActionButton menjadi shuffle untuk menunjukkan tombol random. Kodenya menjadi:
```
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.shuffle),
      ), // This trailing comma makes auto-formatting nicer for build methods.
```

Simpan kode dengan menekan tombol Ctrl+S dan tombol sembarang tsb. telah berfungsi.


## Refleksi

1. Coba bayangkan aplikasi mana saja bisa kita buat dengan berbagai fitur ini?
2. Coba bereksperimen dengan berbagai widget ini dan kalau ada yang salah (_error_) bandingkan kode Anda dengan kode final yang saya persiapkan di [Burung Nias](https://github.com/sslaia/burung_nias/blob/pertemuan-7/lib/main.dart)


## Referensi

Kita bisa melihat daftar icon serta namanya, yang kita bisa gunakan dalam kode kita, di [Google Fonts](https://fonts.google.com/icons) dan pilih icons. Di situ juga terdapat ratusan huruf yang kita bisa gunakan secara bebas, termasuk huruf profesional, yang berharga ratusan dollar. 

Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)

Berbagai dokumentasi, contoh, tutorial dlsb. ada di [https://flutter.dev/docs](https://flutter.dev/docs)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)








