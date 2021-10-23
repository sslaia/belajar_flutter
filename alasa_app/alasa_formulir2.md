# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Membuat formulir dengan validasi data

Kita telah membuat formulir dalam berkas home_page.dart. Namun ada skenario di mana sekadar input data tidak cukup, yakni bila dalam satu formulir ada tempat isian wajib. Untuk mencek apakah tempat isian tsb telah diisi atau tidak kita perlu apa yang dinamakan validasi.

Untuk memungkinkan validasi data, Flutter menggunakan widget **TextFormField**. Dan itulah yang akan kita gunakan dalam aplikasi Alasa ini.

Widget TextFormField pada dasarnya hanyalah widget TextField, yang telah ditambahkan fungsi validasi. Karena itu pada prakteknya, kita hanya mengubah nama TextField menjadi TextFormField dan menambahkan parameter validator dengan argumennya.

## Langkah 1: Membuat kunci (GlobalKey)

Untuk memungkinkan validasi, Flutter membutuhkan satu kunci (**GlobalKey**), yang dalam hal ini adalah kunci untuk status dari formulir kita, dan keseluruhan formulir yang telah ada harus dimasukkan menjadi anak dari widget **Form**.

Karena itu kita menciptakan satu variable kunci yang diambil dari **GlobalKey<FormState>**, kemudian mengapit keseluruhan formulir ke widget **Form** dan memberinya kunci, yang telah kita buat.

1. Bukalah berkas **home_page.dart**, yang telah kita ciptakan pada pertemuan terakhir.
2. Pergi ke bagian di mana kita bisa menyisipkan kode, yakni setelah baris 10. Sisipkan baris baru setelah baris 10 ini.
3. Tuliskan baris kode berikut untuk membuat variable bernama _formKey, yang menyimpan kunci formulir kita:
```
  final _formKey = GlobalKey<FormState>();
```

## Langkah 2: Menggunakan kunci di dalam widget Form

1. Cari di mana formulir mulai, yakni di badan aplikasi (_body_) di mana ada widget **Padding** (di baris 35).
2. Letakkan cursor dan klik sekali di atas widget **Padding** tsb, kemudian klik di bola lampu yang muncul, lalu pilih `Wrap with Widget` dan tukar kata widget yang otomatis disisipkan menjadi **Form**.
3. Buat garis baru lalu sisipkan kunci yang telah dibuat di atas di dalam badan widget Form. Keseluruhan kode akan menjadi sbb.:
```
      body: Form(
        key: _formKey,
        child: Padding(
        ...
```


## Langkah 3: Mengubah TextField menjadi TextFormField

Cari semua widget bernama TextField dan ganti menjadi **TextFormField**


## Langkah 4: Menyisipkan validator untuk kolom isian

Kini tetapkan kolom isian mana yang wajib diisi dan yang mana tidak. Katakanlah misalnya bahwa kolom isian nama, marga dan email wajib, sedangkan yang lainnya tidak.

1. Pergi ke kolom isian pertama, yakni nama (baris 42).
2. Buat garis barus setelah controller (baris 43).
3. Tuliskan baris-baris kode validator berikut:
```
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return 'Masukkan nama Anda!';
                    }
                    return null;
                  },
```

4. Sisipkan baris-baris kode yang sama ke kolom isian marga dan email.
5. Sesuaikan pesan "Masukkan nama Anda" di validator tsb. menjadi "Masukkan marga Anda" di kolom isian marga dan "Masukkan email Anda" di kolom isian email.

Contoh keseluruhan kolom isian email misalnya akan menjadi sbb.:
```
                TextFormField(
                  controller: emailController,
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return 'Masukkan email Anda!';
                    }
                    return null;
                  },
                  decoration: InputDecoration(
                  ...
```


## langkah 5: Menentukan tipe keyboard waktu mengisi data

Untuk membantu penginput data, kadang bagus menyediakan tipe keyboard yang sesuai. Misalnya ketika saatnya mengetik angka tanggal lahir, maka bagus kalau tipe keyboard angka langsung muncul di layar. Untuk itu digunakan parameter keyboardType dengan berbagai argumen yang cocok: datetime (untuk tanggal), phone(untuk telepon), emailAddress(untuk email, sehingga tersedia tanda @ langsung di keyboard) dlsb.

1. Pergi ke kolom isian email (baris 72) dan buat baris baru setelah controller (baris 73).
2. Sisipkan baris kode berikut:
```
                  keyboardType: TextInputType.emailAddress,
```

3. Dengan modus yang sama sisipkan `keyboardType: TextInputType.phone` di kolom isian telepon dan `keyboardType: TextInputType.datetime` di kolom isian tanggal lahir.
4. Kolom isian tanggal lahir misalnya akan nampak sbb.:
```
                TextFormField(
                  controller: tanggalLahirController,
                  keyboardType: TextInputType.datetime,
                  decoration: InputDecoration(
                  ...
```


## Langkah 6: Menyisipkan validator untuk tombol Kirim

Formulir kita hampir rampung. Langkah terakhir adalah menyisipkan validator untuk tombol **Kirim**, artinya kita perintahkan komputer untuk memastikan bahwa kolom isian wajib telah diisi sebelum mengirim data ke database.

Untuk itu cari tombol kirim, yang ada di dalam widget **ElevatedButton** di baris 117.

Kita akan menyisipkan baris-baris kode berikut untuk validasi terakhir:
```
                    final form = _formKey.currentState;
                    if (_formKey.currentState!.validate()) {
                      form?.save();
                    }
```

Dan untuk menampilkan pesan kepada pengguna bahwa data telah disimpan, kita menggunakan satu widget bernama ScaffoldMessenger, yang akan menampilkan satu pesan:
```
                      ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(
                          content: Text('Data telah disimpan!'),
                          duration: Duration(seconds: 3),
                        ),
                      );
``` 

Keseluruhan kode **ElevatedButton** akan menjadi seperti ini setelah ditambah validasi dan pesan di atas:
```
                ElevatedButton(
                  onPressed: () {
                    final form = _formKey.currentState;
                    if (_formKey.currentState!.validate()) {
                      form?.save();
                      ScaffoldMessenger.of(context).showSnackBar(
                        const SnackBar(
                          content: Text('Data telah disimpan!'),
                          duration: Duration(seconds: 3),
                        ),
                      );
                    }
                    print('Data telah dikirim');
                  },
                  child: const Text('Kirim'),
                ),
```

Selesai!!!

Anda kini bisa melihat hasilnya di emulator.
1. Jalankan emulator. Setelah emulator tampil dan proses memuat layar selesai,
2. Jalankan aplikasi dengan menekan tombol panah hijau di baris icon menu. Setelah selesai kompilasi dan formulir tampil di layar emulator,
3. Klik tombol **Kirim**. Anda akan melihat beberapa _error_ muncul dengan pesan yang ditampilkan dalam warna merah, salah satu misalnya adalah "Masukan nama Anda!"

![Formulir Alasa](./formulir.jpg?raw=true)

4. Silakan juga mengklik dalam kolom isian telepon untuk melihat bahwa keyboard otomatis diubah ke dalam modus angka. Demikian juga bila Anda mengklik di kolom isian tanggal lahir.
5. Bila Anda mengklik dalam kolom isian email, tanda @ akan otomatis muncul di baris bawah keyboard, karena alamat email harus menggunakan tanda @!


Validator telah berfungsi dan kini formulir siap digunakan. Untuk itu kita siap membuat database.

Kode lengkap formulir, yang telah diperbaharui dengan fungsi validasi ini ada di [alasa_app](https://github.com/sslaia/alasa_app/blob/membuat_formulir_validasi/lib/home_page.dart)


**Navigasi**: [Menu Utama](./README.md) | [Anatomi aplikasi](./alasa_anatomi.md) | [Mendesain database](./alasa_design_database.md) | [Merancang formulir tanpa validasi](./alasa_formulir1.md) | [Membuat database](./alasa_database1.md)
