# Belajar Bersama Flutter

Pertemuan 10, 30 September 2021


## Merangkum kembali apa yang telah dipelajari kali lalu

Dalam pertemuan minggu lalu kita telah belajar menciptakan layar kedua dengan memanfaatkan yang dinamakan navigator, yang bertugas mengkoordinasikan berbagai rute dalam aplikasi. Hal itu kita mulai dengan aplikasi sederhana, kemudian kita menerapkannya di aplikasi Gogowaya.

Hari ini kita akan mempelajari bagaimana memasang apa yang dinamakan icon launcher, yakni icon yang mewakili penampakkan aplikasi kita dalam daftar aplikasi di smartphone. Biasanya hal ini merupakan logo.

Kemudian kita akan berkenalan dengan topik baru, yakni membuat blok menu di dalam aplikasi atau istilah teknisnya menu drawer.

Lalu kalau ada kesempatan kita akan belajar menandatangani dan membuat paket aplikasi kita sehingga siap untuk diinstalasi di smartphone lain atau di-upload ke Google Play Store.


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


## Menciptakan menu drawer

Jauh lebih sederhana daripada yang kita bayangkan. Tambahkan parameter drawer di **Scaffold** lalu isi dengan berbagai item menu yang masing-masing ditampilkan dengan widget Text. Namun untuk memungkinkan menggeser ke bawah dan ke atas kalau daftar menu tsb panjang melebihi tinggi layar, gunakanlah widget ListView + ListTile.


## Menyiapkan aplikasi untuk siap diinstalasi/diupload ke Play Store

Persiapan:

Anda perlu menetapkan
1. Satu folder di mana Anda menyimpan kunci, yang akan digunakan menandatangani aplikasi
2. Satu password yang dinamakan key store password. Password ini akan digunakan waktu meng-upload aplikasi ke Google Play Store. Anda harus membuatnya walaupun tidak meng-upload ke sana!
3. Satu password yang dinamakan key password, yang merupakan kunci untuk mengunci aplikasi yang sedang dibuat.
4. Nama alias yang akan digunakan untuk mengakses password tsb. seandainya karena satu alasan kita lupa passwordnya.

Saran:

Simpanlah versi produksi (aplikasi siap rilis) bersama kuncinya di satu folder tertentu, mis.
```
kunci\                      <-- folder kunci, yang berisi kunci berbagai aplikasi yang telah dibuat
kunci\gogowaya\             <-- folder gogowaya
kunci\gogowaya\info.txt     <-- satu berkas berisi info aplikasi dan kuncinya
kunci\gogowaya\gogowaya.jks <-- kunci aplikasi gogowaya
kunci\gogowaya\gogowaya.apk <-- aplikasi gogowaya, yang bisa diinstalasi (telah ditandatangani)
```

### Langkah menciptakan paket aplikasi untuk rilis

![Contoh jendela menandatangani aplikasi](./gogowaya/kunci.png?raw=true)

1. Buka aplikasi Kartu Nama di dalam **Android Studio**
2. Dari menu **Tools > Flutter > Open for editing in Android Studio**. Tunggu sampai Gradle selesai mensinkronisasi berbagai komponen yang diperlukan untuk mengkompilasi aplikasi ke dalam bahasa mesin.
3. Di barisan menu, klik **Build** lalu **Generate signed Bundle/APK**
4. Klik **APK**, lalu **Next**
5. Di **Key store path**, klik **Create new** (atau Choose existing kalau kuncinya telah dibuat sebelumnya.) Di sini kita andaikan belum ada kunci, jadi harus buat baru (lihat no. 5). Alternatif, langsung masukkan nama path di mana Anda akan menyimpan kunci, mis. saya menyimpannya di /home/username/keys/gogowaya/gogowaya.jks jadi saya masukkan langsung di situ (lihat gambar di atas).
6. Di jendela yang terbuka, masukkan nama _path_ dari folder yang telah ditetapkan di atas di **Key store path**. Mis. di tempat saya /home/username/keys/gogowaya/gogowaya.jks.
7. Masukkan key store password yang telah dipersiapkan tadi dan ulangi di tempat **Confirm**.
8. Di bawah, setelah baris **Alias**, masukkan key password yang telah dipersiapkan tadi. Demikian juga di sini harus diulangi, untuk memastikan kita tidak salah ketik.
9. Masukkan nama (seandainya ini aplikasi komersial, berarti nama di sini adalah nama lengkap seperti tertera dalam dokumen resmi)
10. Silakan mengisi detil lainnya yang sesuai (Country code Indonesia adalah ID)
11. Tekan tombol **OK**.
12. Tekan tombol **Next**.
13. Di jendela baru pilih **release** untuk **Build Variants**.
14. Tekan tombol **Finish**. Perhatikan di situ ditunjukkan juga di mana aplikasi siap jadi itu nanti disimpan.
15. Setelah selesai akan muncul notifikasi Generate signed APK **di sebelah kanan bawah**. Buka jendela tsb. dengan mengklik tanda panah bawah di sebelah kanan jendela notifikasi, lalu pilih **locate**.
16. Anda akan menemukan aplikasi yang telah dikompilasi tsb. dengan nama **app-release.apk** di folder android/app/release/
17. Tinggal ubah namanya menjadi nama yang sesuai mis. gogowaya.apk dan siap untuk diinstalasi di smartphone lain.


# Kalau ada waktu: Mengorganisir kode, sehingga gampang dibaca.

Sampai sekarang kita menulis semua kode kita di dalam berkas main.dart. Coba perhatikan berkas tsb. Lama-lama berkas tsb. menjadi sesak oleh kode dan kita sulit bernavigasi dari satu bagian ke bagian lainnya.

Di sinilah perlunya memecah-mecahkan kode ke blok-blok yang lebih kecil. Misalnya dalam aplikasi **Gogowaya** yang kita kembangkan minggu lalu ada satu blok kode untuk layar baru (dari baris 131). Daripada menambahkannya di dalam berkas main.dart, lebih baik memindahkannya ke berkas baru misalnya dengan nama halaman_detil.dart.

Silakan memecah-mecahkan berbagai kelas dalam aplikasi Gogowaya menjadi berkas-berkas tersendiri.


## Refleksi

Bagaimana selanjutnya? Apakah kita teruskan dengan mengenal berbagai peralatan (_tools_) yang ada untuk membangun aplikasi, seperti selama ini? Saya lihat telah ada banyak tutorial dalam bahasa Indonesia, jadi mungkin kurang efisien menduplikasi yang telah ada. 

Ataukah kita konsentrasi saja membuat satu aplikasi yang diusulkan oleh peserta lalu kita mencari segala peralatan yang kita butuhkan untuk itu? 


## Referensi

- [Publish your app](https://developer.android.com/studio/publish) 
- Flutter packages ada di [pub.dev/flutter/packages](https://pub.dev/flutter/packages)
- Berbagai dokumentasi, contoh, tutorial dlsb. ada di [https://flutter.dev/docs](https://flutter.dev/docs)

Bantuan selalu dapat di [stockoverflow.com](https://www.stockoverflow.com) dan di berbagai situs di Internet (perhatikan yang ada medium dalam alamatnya).

Di YouTube juga ada banyak berbagai tutorial di antaranya:
- [Flutter](https://www.youtube.com/c/flutterdev)
- [Learn App Code](https://www.youtube.com/c/LearnFlutterCode)
- [Reso Coder](https://www.youtube.com/ResoCoder)
- [Johannes Milke](https://www.youtube.com/JohannesMilke)

