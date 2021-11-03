# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Mengatur ulang HomePage

Dalam pertemuan kali lalu kita telah berhasil membuat database. Tentu saja kini kita ingin melihat isi database dan memanipulasinya. Namun sebelum sampai ke situ, kita perlu mereorganisasi HomePage kita. Mengapa?

Sampai sekarang kita telah memasukkan formulir isian database di dalam berkas home_page.dart. Itu berarti tak ada kemungkinan bagi kita memilih entah memasukkan data, memanipulasinya atau sekedar menampilkan isi database yang telah ada.

Karena itu kita perlu merancang ulang homepage tsb. Pertama kita mengganti nama berkas **home_page.dart** menjadi **formulir_page.dart**. Kedua kita mengubah nama klas di dalam berkas formulir_page.dart menjadi **FormulirPage**. Ketiga, ciptakan berkas baru dengan nama home_page.dart.

Di dalam berkas home_page.dart kita akan menempatkan halaman depan aplikasi, kemudian dari situ kita membuat navigasi ke berbagai operasi database di atas. Navigasi tsb. akan kita letakkan di tombol FloatingActionButton di sudut kanan bawah. Untuk itu kita menggunakan paket bernama `flutter_speed_dial`.

## Langkah 1: Persiapan

1. Buka aplikasi **alasa_app**
2. Buka berkas **puspec.yaml**
3. Sisipkan baris baru setelah baris 39, setelah paket provider, dan tulis baris kode berikut (pastikan awal huruf f sejajar dengan awal huruf berbagai paket di atasnya:
```
  flutter_speed_dial: ^4.6.6
```
4. Tekan tombol **Pub get** di pinggir atas jendela berkas pubspec.yaml.


## Langkah 2: Mengganti nama berkas

1. Di dalam folder **lib**, klik sekali di berkas home_page.dart
2. Tekan tombol kanan mouse, pilih **Refactor** lalu **Rename**
3. Ganti nama home_page.dart menjadi **formulir_page.dart**
4. Buka berkas formulir_page.dart
5. Sekarang kita perlu menjalankan Find and Replace. Untuk itu tekan tombol **Ctrl+R** lalu tulis **HomePage** di tempat isian pertama dan **FormulirPage** di tempat isian kedua.
6. Klik tombol **Replace All**
7. Simpan perubahan dengan menekan tombol **Ctrl+S**.


## Langkah 3: Menciptakan berkas home_page.dart

1. Klik sekali di nama folder **lib**, lalu tekan tombol kanan mouse.
2. Pilih **New** lalu **Dart File**, kemudian tulis nama berkas: **home_page.dart**
3. Sisipkan kode berikut:
```
import 'package:alasa_app/formulir_page.dart';
import 'package:flutter/material.dart';
import 'package:flutter_speed_dial/flutter_speed_dial.dart';

class HomePage extends StatefulWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
          title: const Text("Alasa")
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: const [
            Spacer(),
            Text("Ya'ahowu", style: TextStyle(fontSize: 24)),
            SizedBox(height: 50),
            Text("ALASA", style: TextStyle(fontSize: 48)),
            SizedBox(height: 50),
            Text("Aplikasi database anggota", style: TextStyle(fontSize: 24)),
            Spacer(),
          ],
        ),
      ),
      floatingActionButton: SpeedDial(
        icon: Icons.menu,
        activeIcon: Icons.close,
        spacing: 3,
        childPadding: const EdgeInsets.all(5),
        spaceBetweenChildren: 4,
        elevation: 8.0,
        isOpenOnStart: false,
        animationSpeed: 200,
        children: [
          SpeedDialChild(
            child: const Icon(Icons.margin),
            backgroundColor: Colors.indigo,
            foregroundColor: Colors.white,
            label: 'Daftar anggota',
            visible: true,
            onTap: () {
              // TODO: Daftar anggota
            },
          ),
          SpeedDialChild(
            child: const Icon(Icons.accessibility),
            backgroundColor: Colors.deepOrange,
            foregroundColor: Colors.white,
            label: 'Manipulasi data',
            onTap: () {
              //TODO: Operasi database (update, delete)
            },
          ),
          SpeedDialChild(
            child: const Icon(Icons.edit),
            backgroundColor: Colors.green,
            foregroundColor: Colors.white,
            label: 'Memasukkan data',
            onTap: () {
              Navigator.push(context, MaterialPageRoute(builder: (context) => FormulirPage(),),);
              //TODO: Memasukkan data
            },
          ),
        ],
      ),
    );
  }
}

```
4. Buka berkas **main.dart**.
5. Di baris 32 klik sekali di atas nama klas **HomePage()**.
6. Tekan tombol **Alt+Enter** dan pilih `import 'package:alasa_app/home_page.dart'`
7. Hapus baris `import 'package:alasa_app/formulir_page.dart';` di baris 2.

Kini jalankan aplikasi dengan menekan tombol tanda panah berwarna hijau. Coba bereksperimen dengan tombol FloatingActionButton. Pastikan melihat satu item menu "Memasukkan data". Klik item tsb. dan formulir memasukkan data akan dibuka.



**Navigasi**: [Menu Utama](./README.md) | [Anatomi aplikasi](./1_anatomi.md) | [Mendesain database](./2_mendesign_database.md) | [Merancang formulir](./3_membuat_formulir_1.md) | [Merancang formulir dengan validasi](./4_membuat_formulir_2.md) | [Membuat database](./5_membuat_database.md) | [Mengatur ulang HomePage](./7_manipulasi_database.md)
