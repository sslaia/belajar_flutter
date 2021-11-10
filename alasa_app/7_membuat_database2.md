# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Pengantar

Kali lalu kita telah membuat database dengan menggunakan paket moor. Ternyata menggunakan paket ini semakin sulit, karena pelbagai perubahan baik perubahan karena migrasi dari moor ke drift, maupun karena perubahan menyangkut _null safety_ di Flutter.

Untungnya kita memiliki alternatif, yakni paket **sqflite** (perhatikan huruf f di dalam nama sqlite itu). Dengan paket ini kita bisa mencapai hal yang sama.


## Langkah 1: Membuat berkas database

1. Pastikan telah membuka aplikasi Alasa
2. Klik sekali di folder **lib**, kemudian tekan tombol kanan mouse untuk membuat berkas baru: **New** > **Dart File**.
3. Beri nama berkas baru ini: **database_page.dart**
4. Impor kedua paket berikut dengan meletakkan kedua baris kode ini di baris pertama:

```
import 'dart:async';
import 'package:sqflite/sqflite.dart' as sql;
```

5. Buat kelas baru bernama DatabasePage untuk mulai menciptakan database

```
class DatabasePage {

}
```

6. Sekarang sisipkan baris kode berikut di dalam badan kelas tsb. Kode ini mendefinisikan tabel di dalam database:

```
  static Future<void> createTables(sql.Database database) async {
    await database.execute("""
    CREATE TABLE anggota(
    id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, 
    nama TEXT, 
    marga TEXT, 
    email TEXT, 
    telepon TEXT, 
    pendidikan TEXT, 
    tanggalLahir TEXT)
    """);
  }
```

7. Di bawahnya, sebelum tanda kurung kurawal penutup, sisipkan baris kode berikut. Kode ini mendefinisikan nama berkas database di harddisk dan versi database.

```
  static Future<sql.Database> db() async {
    return sql.openDatabase(
      'halasa.db',
      version: 1,
      onCreate: (sql.Database database, int version) async {
        await createTables(database);
      }
    );
  }
```

Sekarang menyusul berbagai blok kode yang mendefinisikan berbagai operasi database (menarik data, menyisipkan data baru, mengupdate dan menghapus)

8. Sisipkan kode berikut yang berfungsi untuk menyimpan data baru ke dalam database

```
  // Menyimpan data yang baru dimasukkan ke dalam tabel anggota di database
  static Future<int> simpanData(String nama, String marga, String email, String telepon, String pendidikan, String tanggalLahir) async {
    final db = await DBHelper.db();
    final data = {
      'nama': nama,
      'marga': marga,
      'email': email,
      'telepon': telepon,
      'pendidikan': pendidikan,
      'tanggalLahir': tanggalLahir
    };
    final id = await db.insert(
        'anggota', data, conflictAlgorithm: sql.ConflictAlgorithm.replace);
    return id;
  }
```

9. Lalu sisipkan kode berikut untuk mengambil data dari database:

```
  // Mengambil semua isi tabel anggota dari database
  static Future<List<Map<String, dynamic>>> ambilSemuaAnggota() async {
    final db = await DatabasePage.db();
    return db.query('anggota', orderBy: "nama");
  }

  // Mengambil satu item dari tabel anggota
  static Future<List<Map<String, dynamic>>> ambilSatuAnggota(int id) async {
    final db = await DatabasePage.db();
    return db.query('anggota', where: "id = ?", whereArgs: [id], limit: 1);
  }
```

9. Kemudian sisipkan kode berikut untuk mengupdate data yang telah ada:

```
  // Mengupdate satu item dalam tabel anggota
  static Future<int> updateAnggota(int id, String nama, String marga, String email, String telepon, String pendidikan, String tanggalLahir) async {
    final db = await DatabasePage.db();
    final data = {
      'nama': nama,
      'marga': marga,
      'email': email,
      'telepon': telepon,
      'pendidikan': pendidikan,
      'tanggalLahir': tanggalLahir
    };

    final hasil = await db.update('anggota', data, where: "id = ?", whereArgs: [id]);
    return hasil;
  }
```

10. Akhirnya sisipkan blok kode terakhir ini untuk menghapus item dalam database:

```
  // Menghapus satu item dalam tabel anggota
  static Future<void> hapusAnggota(int id) async {
    final db = await DatabasePage.db();
    try {
      await db.delete('anggota', where: "id = ?", whereArgs: [id]);
    } catch (err) {
      print("Ada masalah waktu mau menghapus: $err");
    }
  }
```

Keseluruhan kode di berkas database_page.dart adalah sbb.:

```
import 'dart:async';
import 'package:sqflite/sqflite.dart' as sql;

class DatabasePage {
  static Future<void> createTables(sql.Database database) async {
    await database.execute("""
    CREATE TABLE anggota(
    id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, 
    nama TEXT, 
    marga TEXT, 
    email TEXT, 
    telepon TEXT, 
    pendidikan TEXT, 
    tanggalLahir TEXT)
    """);
  }

  static Future<sql.Database> db() async {
    return sql.openDatabase(
        'halasa.db',
        version: 1,
        onCreate: (sql.Database database, int version) async {
          await createTables(database);
        }
    );
  }

  // Menyimpan data yang baru dimasukkan ke dalam tabel anggota di database
  static Future<int> simpanData(String nama, String marga, String email, String telepon, String pendidikan, String tanggalLahir) async {
    final db = await DatabasePage.db();
    final data = {
      'nama': nama,
      'marga': marga,
      'email': email,
      'telepon': telepon,
      'pendidikan': pendidikan,
      'tanggalLahir': tanggalLahir
    };
    final id = await db.insert(
        'anggota', data, conflictAlgorithm: sql.ConflictAlgorithm.replace);
    return id;
  }

  // Mengambil semua isi tabel anggota dari database
  static Future<List<Map<String, dynamic>>> ambilSemuaAnggota() async {
    final db = await DatabasePage.db();
    return db.query('anggota', orderBy: "nama");
  }

  // Mengambil satu item dari tabel anggota
  static Future<List<Map<String, dynamic>>> ambilSatuAnggota(int id) async {
    final db = await DatabasePage.db();
    return db.query('anggota', where: "id = ?", whereArgs: [id], limit: 1);
  }

  // Mengupdate satu item dalam tabel anggota
  static Future<int> updateAnggota(int id, String nama, String marga, String email, String telepon, String pendidikan, String tanggalLahir) async {
    final db = await DatabasePage.db();
    final data = {
      'nama': nama,
      'marga': marga,
      'email': email,
      'telepon': telepon,
      'pendidikan': pendidikan,
      'tanggalLahir': tanggalLahir
    };

    final hasil = await db.update('anggota', data, where: "id = ?", whereArgs: [id]);
    return hasil;
  }

  // Menghapus satu item dalam tabel anggota
  static Future<void> hapusAnggota(int id) async {
    final db = await DatabasePage.db();
    try {
      await db.delete('anggota', where: "id = ?", whereArgs: [id]);
    } catch (err) {
      print("Ada masalah waktu mau menghapus: $err");
    }
  }

}
```

Selesai!



**Navigasi**: [Menu Utama](./README.md) | [Anatomi aplikasi](./1_anatomi.md) | [Mendesain database](./2_mendesign_database.md) | [Merancang formulir](./3_membuat_formulir_1.md) | [Merancang formulir dengan validasi](./4_membuat_formulir_2.md) | [Membuat database dengan Moor] | [Mengatur Homepage](./6_mengatur_home_page.md) | [Membuat tampilan daftar Anggota](./8_membuat_daftar_anggota.md)
