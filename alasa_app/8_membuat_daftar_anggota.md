# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Pengantar

Kita telah berhasil membuat database menggunakan paket sqflite, tetapi database itu sendiri masih kosong. Pada pertemuan ini kita mulai menggunakan database tsb. dengan memasukkan data dan menampilkan data tsb. ke layar.


## Langkah 1: Mengadakan pembersihan

Sebelum kita melangkah lebih jauh baiklah kita membersihkan proyek aplikasi Alasa dari berbagai berkas dan paket, yang tidak dibutuhkan lagi.

Membersihkan berkas **main.dart**

Kita tahu di berkas main.dart masih terdapat baris kode yang mubazir, yang tidak dibutuhkan lagi (baris 37 dan sesudahnya). Baiklah kita membuangnya, termasuk berbagai komentar, sehingga kode nampak lebih rapi dan gampang dipahami.

1. Buka berkas **main.dart**.
2. Hapus baris 37 sampai baris terakhir (baris 121)
3. Hapus komentar di baris 21 s/d 29.
4. Hapus impor yang tak diperlukan lagi yakni import `'package:alasa_app/alasa_database.dart';` dan `import 'package:provider/provider.dart';`
5. Klik di widget Provider di baris 14 (?), lalu melalui menu bola lampu, pilih `Remove this widget`

6. Buka berkas **pubspec.yaml**.
7. Hapus paket (atau pasang tanda komentar) `moor_flutter`, `moor`, `moor_generator` dan `build_runner`

8. Lihat isi folder **lib**.
9. Hapus berkas `alasa_database.dart` dan `alasa_database.dart`
10. Buka berkas **formulir_page.dart**
11. Hapus baris di mana terdapat `import 'package:moor/moor.dart' as moor;` dan `import 'package:alasa_app/alasa_database.dart';`
12. Hapus juga referensi ke database moor di baris 127 yang berbunyi `final dao = Provider.of<AnggotaDao>(context, listen: false);`
13. Demikian juga hapus baris 131-139, yakni:

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


## Langkah 2: Menambah paket sqflite dan paket lain

1. Buka kembali berkas pubspec.yaml
2. Sisipkan paket berikut di akhir blok dependencies:

```
  sqflite: ^2.0.0+4
  flutter_slidable: ^0.6.0
```

3. Tekan tombol **Pub get** di pinggir atas jendela pubspec.yaml

## Langkah 3: Membuat berkas daftar anggota

1. Klik sekali di folder **lib**, kemudian tekan tombol kanan mouse untuk membuat berkas baru: **New** > **Dart File**.
2. Beri nama berkas baru ini: **daftar_anggota.dart**
3. Impor ketiga paket berikut dengan meletakkan kedua baris kode ini di baris pertama:

```
import 'package:flutter/material.dart';
import 'package:flutter_slidable/flutter_slidable.dart';
import 'package:alasa_app/database_page.dart';
```

4. Buat widget stateful bernama DaftarAnggota:

```
class DaftarAnggota extends StatefulWidget {
  const DaftarAnggota({Key? key}) : super(key: key);

  @override
  _DaftarAnggotaState createState() => _DaftarAnggotaState();
}

class _DaftarAnggotaState extends State<DaftarAnggota> {

  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

5. Di baris 13 sisipkan baris kode berikut:

```
  // Semua anggota
  List<Map<String, dynamic>> _anggota = [];
  bool _sedangMengambil = true;

  // Mengambil data anggota dari database
  void _ambilDataAnggota() async {
    final data = await DatabasePage.ambilSemuaAnggota();
    setState(() {
      _anggota = data;
      _sedangMengambil = false;
    });
  }

  @override
  void initState() {
    _ambilDataAnggota();
    super.initState();
  }
```

6. Di baris 35 terdapat widget Container, yang otomatis diselipkan oleh AS. Di sini kita mulai menempatkan widget **Scaffold** dan widget-widget lainnya untuk membangun layar daftar aggota. Baris 35 dst akan nampak sbb.:

```
    return Scaffold(
      appBar: AppBar(
        title: const Text('Daftar anggota'),
      ),
      body: _sedangMengambil
          ? const Center(
        child: CircularProgressIndicator(),
      )
          : ListView.builder(
          itemCount: _anggota.length,
          itemBuilder: (context, index) => Card(
            color: Colors.orange[200],
            margin: const EdgeInsets.all(12.0),
            child: Slidable(
              actionPane: const SlidableDrawerActionPane(),
              secondaryActions: [
                IconSlideAction(
                  caption: 'Hapus',
                  color: Colors.red,
                  icon: Icons.delete,
                  // onTap: () => hapusData(_anggota[index]['id']),
                  onTap: () async {
                    await DatabasePage.hapusAnggota(_anggota[index]['id']);
                    _ambilDataAnggota();
                  },
                )
              ],
              child: ListTile(
                  title: Text(_anggota[index]['nama'] +
                      ' ' +
                      _anggota[index]['marga']),
                  subtitle: Text(_anggota[index]['email'] +
                      ',' +
                      _anggota[index]['telepon']),
                  onTap: () {
                    int id = _anggota[index]['id'];
                    String nama = _anggota[index]['nama'];
                    String marga = _anggota[index]['marga'];
                    String email = _anggota[index]['email'];
                    String telepon;
                    if (_anggota[index]['telepon'] != null) {
                      telepon = _anggota[index]['telepon'];
                    } else {
                      telepon = "kosong";
                    }
                    String pendidikan;
                    if (_anggota[index]['pendidikan'] != null) {
                      pendidikan = _anggota[index]['pendidikan'];
                    } else {
                      pendidikan = "kosong";
                    }
                    String tanggalLahir;
                    if (_anggota[index]['tanggalLahir'] != null) {
                      tanggalLahir = _anggota[index]['tanggalLahir'];
                    } else {
                      tanggalLahir = "kosong";
                    }

                    Navigator.push(
                      context,
                      MaterialPageRoute(
                        builder: (context) => DetilPage(
                            id: id,
                            nama: nama,
                            marga: marga,
                            email: email,
                            telepon: telepon,
                            pendidikan: pendidikan,
                            tanggalLahir: tanggalLahir),
                      ),
                    );
                  }),
            ),
          )),
    );
  }

  Future<void> hapusData(int id) async {
    await DatabasePage.hapusAnggota(id);
  }
}
```

## Langkah 4: Membuat layar detil dari anggota

1. Klik sekali di nama folder **lib**.
2. Tekan tombol kanan mouse dan **New** > **Dart File**
3. Beri nama berkas baru ini **detil_anggota.dart**
4. Kopi semu kode di bawah ini ke dalam berkas **detil_anggota.dart** ini:

```
import 'package:alasa_app/database_page.dart';
import 'package:flutter/material.dart';

class DetilAnggota extends StatefulWidget {
  final int id;
  final String nama;
  final String marga;
  final String email;
  final String telepon;
  final String pendidikan;
  final String tanggalLahir;

  const DetilAnggota(
      {Key? key,
      required this.id,
      required this.nama,
      required this.marga,
      required this.email,
      required this.telepon,
      required this.pendidikan,
      required this.tanggalLahir})
      : super(key: key);

  @override
  State<DetilAnggota> createState() => _DetilAnggotaState();
}

class _DetilAnggotaState extends State<DetilAnggota> {
  final _detilKey = GlobalKey<FormState>();
  final namaController = TextEditingController();
  final margaController = TextEditingController();
  final emailController = TextEditingController();
  final teleponController = TextEditingController();
  final pendidikanController = TextEditingController();
  final tanggalLahirController = TextEditingController();

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

  @override
  Widget build(BuildContext context) {
    namaController.text = widget.nama;
    margaController.text = widget.marga;
    emailController.text = widget.email;
    if (widget.telepon != "kosong") {
      teleponController.text = widget.telepon;
    } else {
      teleponController.text = "";
    }
    if (widget.pendidikan != "kosong") {
      pendidikanController.text = widget.pendidikan;
    } else {
      pendidikanController.text = "";
    }
    if (widget.tanggalLahir != "kosong") {
      tanggalLahirController.text = widget.tanggalLahir;
    } else {
      tanggalLahirController.text = "";
    }

    return Scaffold(
      appBar: AppBar(
        title: const Text('Detil data anggota'),
      ),
      body: Form(
        key: _detilKey,
        child: Padding(
          padding: const EdgeInsets.all(32.0),
          child: SingleChildScrollView(
            child: Column(
              children: [
                TextFormField(
                  controller: namaController,
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return 'Masukkan nama Anda!';
                    }
                    return null;
                  },
                  decoration: InputDecoration(
                      hintText: "Nama Anda",
                      labelText: "Nama depan",
                      hintStyle: const TextStyle(color: Colors.black26),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(8))),
                ),
                const SizedBox(height: 8.0),
                TextFormField(
                  controller: margaController,
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return 'Masukkan marga Anda!';
                    }
                    return null;
                  },
                  decoration: InputDecoration(
                      hintText: "Marga Anda",
                      labelText: "Nama belakang",
                      hintStyle: const TextStyle(color: Colors.black26),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(8))),
                ),
                const SizedBox(height: 8.0),
                TextFormField(
                  controller: emailController,
                  keyboardType: TextInputType.emailAddress,
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return 'Masukkan email Anda!';
                    }
                    return null;
                  },
                  decoration: InputDecoration(
                      hintText: "Email Anda",
                      labelText: "Alamat email (contoh: manu@hewan.com)",
                      hintStyle: const TextStyle(color: Colors.black26),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(8))),
                ),
                const SizedBox(height: 8.0),
                TextFormField(
                  controller: teleponController,
                  keyboardType: TextInputType.phone,
                  decoration: InputDecoration(
                      hintText: "Telepon Anda",
                      labelText: "Nomor telepon (08120897652)",
                      hintStyle: const TextStyle(color: Colors.black26),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(8))),
                ),
                const SizedBox(height: 8.0),
                TextFormField(
                  controller: pendidikanController,
                  decoration: InputDecoration(
                      hintText: "Pendidikan terakhir Anda",
                      labelText: "Pendidikan terakhir (SD/SMP/SMA/PT)",
                      hintStyle: const TextStyle(color: Colors.black26),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(8))),
                ),
                const SizedBox(height: 8.0),
                TextFormField(
                  controller: tanggalLahirController,
                  keyboardType: TextInputType.datetime,
                  decoration: InputDecoration(
                      hintText: "Tanggal lahir Anda",
                      labelText: "Tanggal lahir (contoh: 13/1/2001)",
                      hintStyle: const TextStyle(color: Colors.black26),
                      border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(8))),
                ),
                const SizedBox(height: 8.0),
                ElevatedButton(
                  onPressed: () {
                    // final dao = Provider.of<AnggotaDao>(context, listen: false);
                    // DateTime tanggal = DateTime.parse(tanggalLahirController.text);

                    final form = _detilKey.currentState;

                    if (_detilKey.currentState!.validate()) {
                      form?.save();
                      // mengupdate data yang telah ada ke dalm tabel anggota di database
                      updateData();

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
              ],
            ),
          ),
        ),
      ),
    );
  }

  Future<void> updateData() async {
    await DatabasePage.updateAnggota(widget.id, namaController.text, margaController.text, emailController.text, teleponController.text, pendidikanController.text, tanggalLahirController.text);
  }
}
```

5. Buka kembali berkas **daftar_anggota.dart**
6. Pergi ke baris 96 di mana ada tanda _error_ merah dan klik sekali di atas **DetilAnggota**.
7. Tekan secara bersamaan tombol **Alt+Enter**
8. Dari jendela kecil yang muncul, pilih `import 'package:alasa_app/detil_anggota.dart';`


## Langkah 5: Menyesuaikan menu di homepage

1. Buka berkas **home_page.dart**
2. Buat navigasi dari menu "Daftar anggota" ke halaman **DaftarAnggota**:

```
              Navigator.push(context, MaterialPageRoute(builder: (context) => const DaftarAnggota(),),);
```
3. Tekan secara bersamaan tombol **Alt+Enter**
4. Dari jendela kecil yang muncul, pilih `import 'package:alasa_app/daftar_anggota.dart';`


## Langkah 6: Menyesuaikan kode penyimpanan data di formulir

1. Buka **formulir_page.dart**
2. Pergi ke baris 130 dan hapus segala kode dari baris itu sampai sebelum baris di mana ada kode `kosongkanFormulir();`
3. Sisipkan kode berikut sebelum baris di mana `kosongkanFormulir()` tsb:

```
                      // menyimpan data yang telah ada ke dalm tabel anggota di database
                      simpanData();
```

4. Sebelum fungsi kosongkanFormulir() di baris 159, sisipkan baris kode fungsi menyimpan data berikut:

```
  Future<void> simpanData() async {
    await DatabasePage.simpanData(namaController.text, margaController.text, emailController.text, teleponController.text, pendidikanController.text, tanggalLahirController.text);
  }
```


Selesai! Kini Anda siap memasukkan data anggota baru, dan menayangkan anggota yang telah ada di dalam database. Bahkan Anda bisa mengubah entri yang telah ada atau menghapusnya!




**Navigasi**: [Menu Utama](./README.md) | [Anatomi aplikasi](./1_anatomi.md) | [Mendesain database](./2_mendesign_database.md) | [Merancang formulir](./3_membuat_formulir_1.md) | [Merancang formulir dengan validasi](./4_membuat_formulir_2.md) |  [Membuat database dengan Moor](./5_membuat_database1.md) | [Mengatur Homepage](./6_mengatur_home_page.md) | [Membuat database dengan Sqflite](./6_membuat_database2.md)
