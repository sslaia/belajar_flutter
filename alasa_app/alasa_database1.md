# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Pengantar

Setelah selesai merancang formulir isian, kini kita mulai membuat database. Ada beberapa database yang bisa digunakan. Salah satu database yang paling sering digunakan di smartphone adalah **sqlite**, yang merupakan versi ringan dari SQL, yang banyak digunakan di dunia bisnis. Sqlite ini pulalah yang akan kita gunakan dalam aplikasi Alasa.

SQL merupakan satu bahasa pemrograman tersendiri dan kita yang hanya belajar _coding_ sebagai hobi, tidak punya waktu untuk belajar satu atau dua semester tentang sql. Karena itu kita harus menempuh strategi lain. Tujuan akhir kita adalah membangun satu database yang dapat menyimpan berbagai data dari kolom formulir, yang kali lalu telah kita rancang bersama. Tentu saja bagi mereka yang punya minat dan waktu, silakan belajar sendiri sqlite.

Dengan menggunakan patokan di atas, maka kita juga tak perlu belajar detail dari **sqlite**. Yang perlu kita tahu adalah bagaimana supaya data yang ingin kita simpan atas salah satu cara tersimpan di dalam database sqlite, tanpa harus bergulat dengan bahasa pemrograman sqlite sendiri.


## Persiapan

Dalam semangat saling menolong, yang telah menjadi umum di dunia _open source_, beberapa programmer membuat satu paket, yang menyederhanakan proses pembuatan database dengan sqlite dan berbagai operasi seputar itu (memasukkan, menambahkan, menghapus, mengosongkan data dlsb).

Nama paket tsb. adalah **moor**, yang merupakan penulisan terbalik dari **room**, satu paket yang membuat hal yang sama di bahasa pemrograman Java/Kotlin.

## Langkah 1: Mendaftarkan moor

1. Bukalah [aplikasi Alasa](https://github.com/sslaia/alasa_app/tree/membuat_formulir_validasi) di dalam **AS**
2. Bukalah berkas **pubspec.yaml**
3. Di baris 36 (setelah baris 35 di mana _cupertino_icons_ berada) sisipkanlah kode berikut:
```
  moor_flutter: ^4.0.0
  moor: ^4.6.1
```


## Langkah 2: Mendaftarkan paket tambahan

Untuk membuat paket moor berfungsi, perlu beberapa paket tambahan, yakni moor_generator dan build_runner. Seperti nampak dari nama, kedua paket tsb. merupakan generator. Seperti dikatakan di atas, yang digunakan di belakang layar adalah sqlite, tetapi yang kita tulis dalam kode adalah baris kode Dart. Moor dan kedua generator tsb. bekerja di belakang layar menerjemahkan kode kita.

1. Langsung di baris setelah baris paket moor sisipkan paket berikut (berarti di baris 38):
```
  provider: ^6.0.1
```

2. Pergi ke baris 50 (setelah baris 49 di mana flutter_lints berada) dan sisipkan kode berikut:

```
  moor_generator: ^1.4.0
  build_runner:
```

3. Simpan berkas dengan menekan **Ctrl+S**.
4. Klik tombol **Pub get** yang terpampang di pinggir atas jendela berkas pubspec.yaml, supaya paket yang telah kita cantumkan di sini, diregistrasi dalam aplikasi.
5. Tutup berkas puspec.yaml untuk menghindari perubahan yang tidak diinginkan dalam berkas tsb.


## Langkah 3: Menciptakan tabel database

Sekarang kita siap menulis kode untuk membuat database. Di dunia ilmu pembuatan database, setiap kelompok data disebut sebuah tabel, sedangkan setiap item di dalamnya disebut kolom. Kita mulai dengan menciptakan berkas di mana kode untuk ini disimpan.

1. Klik di folder **lib** dan dengan menekan tombol kanan mouse pilih **New**, lalu **Dart file**.
2. Beri nama berkas baru ini: **alasa_database.dart**
3. Di dalam berkas baru alasa_database.dart, sisipkan dua baris berikut di tempat paling atas berkas:
```
import 'package:moor_flutter/moor_flutter.dart';
part 'alasa_database.g.dart';

```

Seperti bisa dilihat di situ baris kedua tsb harus ditulis persis sama dengan nama berkas di mana kode ini berada plus **.g** di akhir nama berkas.

Untuk sementara baris ini ditandai merah, karena berkas tsb. belum ada, masih akan dibuat oleh generator.

Sekarang kita siap untuk menciptakan tabel. Mari memberi nama tabel ini **Anggotas**, karena kita akan memasukkan data tentang orang/anggota/kenalan dalam database tsb. Sayang generator otomatis berbicara bahasa Inggris dan akan menciptakan kelas data secara otomatis menjadi nama table minus s, sehingga kelas data akan menjadi Anggota. Karena itu kita menggunakan huruf s di belakang nama tabel anggota di sini.

Supaya Flutter tahu bahwa table Anggotas ini merupakan sebuah tabel dan mewarisi berbagai karakteristik satu kelas Tabel, maka kita tambahkan kata **extends Table**.

4. Sisipkan kode berikut di baris 4:
```
class Anggotas extends Table {
  
}
```

Sekarang kita mendefinisikan berbagai kolum, yang telah kita sepakati kali lalu, di dalam badan kelas Anggotas ini.

5. Di baris 5 sisipkan baris-baris kode berikut, sehingga keseluruhan kelas tsb. menjadi:
```
class Anggotas extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get nama => text().withLength(min: 1, max: 50)();
  TextColumn get marga => text().withLength(min: 1, max: 20)();
  TextColumn get email => text().withLength(min: 1, max: 20)();
  TextColumn get telepon => text().nullable()();
  TextColumn get pendidikan => text().nullable()();
  TextColumn get tanggalLahir => text().nullable()();
}
```

Dari berbagai nama tsb. menjadi jelas kita membuat kolom untuk setiap tempat isian, yang telah kita rancang.

Kecuali satu kolom tambahan, yakni id, yang akan otomatis diciptakan oleh database untuk bisa mengidentifikasi setiap orang di baris tabel database itu nanti.


## Langkah 4: Membuat kelas database

Setelah selesai membuat tabel, kita perlu memberi tahu sistem untuk mulai meng-inisialisasi database dan menyimpannya ke media penyimpan dengan nama tertentu.

Sisipkan di baris 14 dst. baris-baris kode berikut:
```
@UseMoor(tables: [Anggotas])
class AppDatabase extends _$AppDatabase {
  AppDatabase()
      : super((FlutterQueryExecutor.inDatabaseFolder(
          path: 'db_alasa.sqlite',
          logStatements: false,
        )));

  @override
  int get schemaVersion => 1;
}
```

Apa yang mau dikatakan dengan berbagai kode tsb.? Pertama adalah perintah kepada sistem untuk menggunakan tabel Anggotas. Menyusul perintah untuk mendefinisikan nama berkas database, yang akan disimpan di hard disk. Dan terakhir versi dari database itu. Bila terasa rumit, anggap saja inilah sintaks dari tatabahasa Dart untuk membuat database.


## Langkah 5: Menjalankan generator

1. Buka Terminal dengan mengklik Terminal di barisan tombol di pinggir bawah AS.
2. Ketik perintah berikut: `flutter packages pub run build_runner watch` dan tunggu sampai selesai. Lamanya bisa beberapa menit tergantung kecepatan komputer Anda.

Bila Anda melihat pesan seperti ini `[INFO] Succeeded after 11.4s with 2 outputs (9 actions)` dan melihat telah muncul berkas baru bernama `alasa_database.g.dart` di dalam folder lib, maka proses telah rampung.


## Langkah 6: Membuat DAO (Database Accessor)

Ini merupakan langkah ekstra untuk menciptakan kemungkinan mengakses database tidak secara langsung melainkan melalui satu kelas baru. Mengapa? Adalah merupakan praktek umum untuk memisahkan berbagai hal yang dilakukan ke dalam kelas berbeda, sehingga kode nampak lebih rapi.

Untuk ini sisipkan blok kode berikut di baris 27 (di bawah kelas AppDatabase):

```
@UseDao(tables: [Anggotas])
class AnggotaDao extends DatabaseAccessor<AppDatabase> with _$AnggotaDaoMixin {
  final AppDatabase db;

  AnggotaDao(this.db) : super(db);
}
```

Sekarang tambahkan informasi tentang _dao_ yang baru ini ke dalam kelas database di atas. Pergi ke baris 14 dan tambah kode `daos: [AnggotaDao]` sehingga keseluruhan baris itu sekarang menjadi:
```
@UseMoor(tables: [Anggotas], daos: [AnggotaDao])
```


## Langkah 7: Menulis kode operasi database

Ada beberapa operasi database yang sering kita gunakan, yakni menampilkan semua isi database, memasukkan item baru, meng-update satu item dan tentu saja mengosongkan database.

1. Pergi ke baris 31 di mana `AnggotaDao(this.db) : super(db);` berada lalu sisipkan baris baru sesudahnya.
2. Sisipkan baris-baris kode berikut di garis baru tsb.:
```

  // Ini fungsi untuk menarik data semua anggota dalam database
  Future<List<Anggota>> getSemuaAnggota() => select(anggotas).get();

  // Ini fungsi untuk menampilkan daftar urutan berdasarkan nama dan marga
  Stream<List<Anggota>> watchSemuaAnggota() {
    return (select(anggotas)
        ..orderBy(
            ([(t) => OrderingTerm(expression: t.nama, mode: OrderingMode.asc),
              (t) => OrderingTerm(expression: t.marga)])
        )
    ).watch();
  }
  // Ini fungsi untuk menampilkan daftar urutan berdasarkan pendidikan
  Stream<List<Anggota>> watchPendidikanAnggota() {
    return (select(anggotas)
      ..orderBy(
          ([(t) => OrderingTerm(expression: t.pendidikan, mode: OrderingMode.asc),
                (t) => OrderingTerm(expression: t.nama)])
      )
    ).watch();
  }

  // Ini fungsi untuk menambah item baru ke dalam database
  Future insertAnggota(Insertable<Anggota> anggota) => into(anggotas).insert(anggota);
  // Ini fungsi untuk mengubah item yang telah ada di dalam database
  Future updateAnggota(Insertable<Anggota> anggota) => update(anggotas).replace(anggota);
  // Ini fungsi untuk menghapus satu item dalam database
  Future deleteAnggota(Insertable<Anggota> anggota) => delete(anggotas).delete(anggota);
```

Dengan demikian kode database dan operasi database yang diperlukan telah selesai.


## Langkah 8: Membuat supaya database hanya sekali dijalankan

Kita tahu bahwa operasi terhadap database bisa berulang-ulang terjadi. Dengan demikian kita juga menjalankan database berkali-kali. Kalau hal ini tidak diperhatikan, bukan hanya database kita akan korup, tetapi berbagai database yang terbuka akan memakan memori smartphone dan akan membuatnya _crashed_.

Untuk menghindari hal ini, kita harus membuat supaya aplikasi mencek dulu apakah database telah terbuka, dan kalau belum terbuka, baru database tsb. dijalankan.

1. Buka berkas **main.dart**
2. Pergi ke baris 14 di mana tertera `return MaterialApp`
3. Klik sekali di MaterialApp tsb.
4. Dari bola lampu yang muncul di sebelah kiri, pilih `Wrap with widget` dan langsung hapus kata widget yang otomatis disisipkan menjadi Provider. Kata Provider ini akan ditandai merah
5. Klik sekali di Provider lalu dari jendela kecil yang terbuka pilih `import library 'package:provider/provider.dart'`
6. Buat baris kosong di baris setelah return Provider ini
7. Sisipkan baris kode berikut:
```
      create: (_) => AppDatabase(),
```

Keseluruhan potongan kode yang berubah ini menjadi:
```
    return Provider(
      create: (_) => AppDatabase().anggotaDao,
      child: MaterialApp(
      ...
```


## Langkah 9: Memodifikasi kode tombol Kirim

**Persiapan:**

Pastikan paket-paket berikut telah diimpor ke dalam berkas home_page.dart (diletakkan di baris paling atas):

```
import 'package:alasa_app/alasa_database.dart';
import 'package:flutter/material.dart';
import 'package:moor/moor.dart' as moor;
import 'package:provider/provider.dart';
```

Ketika kita membuat formulir, kita juga membuat tombol **Kirim**. Namun kita belum menulis kode untuk mengirim data yang telah dimasukkan ke database, sebab kita menunggu sampai kita membuat database.

Kini database telah siap, maka kita dapat menulis kode di bagian tombol **Kirim** tsb. untuk mengirim data yang telah dimasukkan pengguna.

Cari widget **ElevatedButton** (baris 126). Dan di dalam badan fungsi **onPressed** tulislah kode berikut:
```
                    final dao = Provider.of<AnggotaDao>(context);
                    // DateTime tanggal = DateTime.parse(tanggalLahirController.text)
```

Baris pertama membuat variable untuk menyimpan database. Baris kedua mengubah input yang berupa string ke dalam tipe data DateTime.

Kemudian di dalam badan kondisi `if (_formKey.currentState!.validate())` tambahkan kode berikut setelah baris `form?.save();`:
```
                      final anggota = AnggotasCompanion(
                        nama: moor.Value(namaController.text),
                        marga: moor.Value(margaController.text),
                        email: moor.Value(emailController.text),
                        pendidikan: moor.Value(pendidikanController.text),
                        tanggalLahir: moor.Value(tanggalLahirController.text)
                      );

                      dao.insertAnggota(anggota);

```

Keseluruhan kode tombol Kirim adalah sbb.:
```
                ElevatedButton(
                  onPressed: () {
                    final dao = Provider.of<AnggotaDao>(context, listen: false);
                    // DateTime tanggal = DateTime.parse(tanggalLahirController.text);

                    final form = _formKey.currentState;

                    if (_formKey.currentState!.validate()) {
                      form?.save();
                      final anggota = AnggotasCompanion(
                        nama: moor.Value(namaController.text),
                        marga: moor.Value(margaController.text),
                        email: moor.Value(emailController.text),
                        pendidikan: moor.Value(pendidikanController.text),
                        tanggalLahir: moor.Value(tanggalLahirController.text)
                      );

                      dao.insertAnggota(anggota);

                      ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(
                          content: Text('Data telah disimpan!'),
                          duration: Duration(seconds: 3),
                        ),
                      );
                    }
                  },
                  child: const Text('Kirim'),
                ),
```


## Langkah 10: Mengosongkan formulir

Setelah data dikirimkan ke database, tentu saja kita ingin mengosongkan formulir, supaya siap untuk memasukkan data baru. Untuk itu kita membuat satu fungsi baru sbb:

```

  void kosongkanFormulir() {
    // fungsi ini memuat ulang pohon widget dan mengosongkan formulir
    setState(() {
      namaController.clear();
      margaController.clear();
      emailController.clear();
      teleponController.clear();
      pendidikanController.clear();
      tanggalLahirController.clear();
    });
  }
```

Untuk itu

1. Pergi ke baris 161, yakni tanda } kedua sebelum yang terakhir.
2. Sisipkan garis baru
3. Di baris baru tsb. (baris 162) sisipkan kode di atas.

Kemudian perintah untuk menjalankan fungsi ini kita tempatkan di dalam badan tombol **Kirim** setelah data dimasukkan ke database.

1. Pergi ke baris 143 di mana `dao.insertAnggota(anggota)` berada.
2. Sisipkan baris baru
3. Di baris baru tsb. sisipkan baris kode berikut:

```

                      kosongkanFormulir();
```


Selesai!



**Navigasi**: [Menu Utama](./README.md) | [Anatomi aplikasi](./alasa_anatomi.md) | [Mendesain database](./alasa_design_database.md) | [Merancang formulir](./alasa_formulir1.md) | [Merancang formulir dengan validasi](./alasa_formulir2.md) | [Membuat database](./alasa_database2.md)
