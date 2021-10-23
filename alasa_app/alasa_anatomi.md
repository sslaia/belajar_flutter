# alasa_app

Belajar membuat aplikasi berbasis database di Flutter melalui aplikasi Alasa


## Anatomi satu aplikasi

Silakan mengamati kode templat aplikasi yang otomatis dibuat waktu aplikasi baru Alasa diciptakan.

![Anatomi aplikasi Alasa](./alasa_app/anatomi1.png?raw=true)

1. Setiap aplikasi memiliki pintu gerbang (baris 3) di mana komputer mulai masuk ketika menjalankan aplikasi tsb. Namanya adalah **main()**. Dari sinilah diberi petunjuk di mana kode untuk menjalankan aplikasi, yakni di **MyApp()** dalam contoh ini (baris 4).
2. Kode dari **MyApp()** tsb. berada dalam kelas tersendiri yang mulai dari baris 7 dst.
3. Seperti bisa dilihat di baris 7 tsb. blok kode MyApp merupakan **StatelessWidget**. Widget ini seperti jelas dalam nama _stateless_, tidak memiliki status. Artinya apa pun yang dijalankan di dalam blok kode ini akan ditampilkan sekali di layar dan sesudah itu tak ada perubahan lagi. Nanti kita akan lihat bahwa ada juga widget lain bernama _stateful_, yang memungkinkan adanya perubahan status setelah berbagai elemen ditampilkan di layar. Namanya StatefulWidget.
4. Tugas dari blok kode baris 7 s/d 30 ini adalah mulai membangun aplikasi (lihat perintah _build(context)_) dengan menetapkan nama (baris 14), tema (baris 15) dan "home" (baris 27), yakni tempat di mana konstruksi aplikasi sendiri berada. Keseluruhannya nampak sbb. (saya telah menghapus baris-baris komentar yang dimulai dengan tanda //)

```
void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
```

Seperti bisa dilihat di baris 27, program mengindikasikan bahwa seterusnya konstruksi aplikasi berada di kelas tersendiri bernama **MyHomePage()**. Mari sekilas mengamati kelas kedua ini. Keseluruhan kode tsb. nampak sbb. setelah berbagai komentar dihapus:

```
class MyHomePage extends StatefulWidget {
  const MyHomePage({Key? key, required this.title}) : super(key: key);

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            const Text(
              'You have pushed the button this many times:',
            ),
            Text(
              '$_counter',
              style: Theme.of(context).textTheme.headline4,
            ),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: const Icon(Icons.add),
      ), // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}
```

5. Seperti bisa dilihat di baris 32, kelas ini merupakan **StatefulWidget**. Berarti dalam blok kode ini akan ada perubahan status elemen tertentu di layar.
6. Yang menarik blok kode berikut terdiri dari dua kelas. Yang pertama dari baris 32 s/d 48 dalam **AS** kita biarkan saja dulu. Kita tidak akan mengubah apa pun di sini. Bagian ini hanya mempersiapkan perubahan status widget.
7. Blok kode kelas yang kedua dari baris 50 s/d 115 mengandung berbagai kode yang akan kita tulis. Di sinilah aplikasi mulai dibangun dengan pertama meletakkan kerangka (_Scaffold_) (baris 72), lalu berbagai elemen lainnya di layar, seperti bar aplikasi di sudut atas layar (baris 73-77), lalu badan (_body_) dari aplikasi tsb. (baris 78-107) dan kemudian satu tombol yang melayang yang dinamakan FloatingActionButton (baris 108-112).
8. Kelas ini bisa diletakkan di sini atau lebih bagus lagi disimpan di berkas tersendiri, sehingga membuat kode dalam berkas ini tidak terlalu ramai.
9. Badan dari aplikasi ini terdiri dari **Center** (baris 78), yang bertugas membuat supaya elemen-elemen di bawahnya diletakkan di tengah layar
10. Kemudian **Column** untuk mengurutkan elemen-elemen di bawahnya (yakni dua buah widget **Text**) dari atas ke bawah.

Mungkin kini Anda sudah mulai merasakan betapa konstruksi dari aplikasi di dalam Flutter itu seperti hirarki yang semakin lama semakin turun ke bawah. Kita bisa mem-visualisasikannya sbb.:
```
- MyApp
  - MaterialApp
    - MyHomePage
      - Scaffold
        - AppBar
        - Center
          - Column
            - Text
            - Text
        - FloatingActionButton
```

Cara lain mem-visualisasikannya adalah dengan menggunakan gambar pohon. Dan memang sering orang menggunakan visualisasi terakhir ini. Para developer sering bicara tentang pohon widget (_widget tree_), tetapi dalam hal ini pohon terbalik.

![Pohon widget aplikasi](./alasa_app/pohon.jpg?raw=true)

Saya sendiri sering membayangkan gambar tsb. seperti rumah. Jadi mulai dari fondasi rumah (_Scaffold_), di atasnya dibangun lantai, dinding dan kolom. Di atas lantai ada meja, kursi, bangku dlsb. Kemudian di atas kolum dan dinding ada langit-langit dan loteng. Di dalam loteng ada mungkin banyak hal lain lagi. Kemudian paling atas ada atap.

Cara lain membayangkannya adalah bagaikan membangun sebuah bangunan dari potongan-potongan lego. Dengan memasang-masangkan potongan lego yang cocok, akhirnya kita bisa membangun sebuah gedung, sebuah kereta api, sebuah pesawat dlsb.

Entah apa pun gambar yang kita gunakan, semuanya untuk membantu kita memvisualisasikan relasi berbagai widget dalam membangun aplikasi. Keseluruhan proses membangun aplikasi mirip dengan membongkar pasang berbagai widget (Center, Column, Text, Button, Icon, Image, dst.). Berbagai widget tsb. mirip potongan-potongan lego.

![Tampilan pohon widget di layar](./alasa_app/pohon_screen.jpg?raw=true)


[Kembali ke Menu Utama](./alasa_app.md)
