# myportofolio_mobile

## Tugas 7
AI Disclosure: This Individual Assignment 7 is purely made by myself without copy-paste from AI. But, I still use AI for new knowledge/information.

Link : https://claude.ai/share/05885cf4-4e12-4d7c-9cd5-f797cf4cbb0e (Claude AI Sonnet 5.5 Medium)

1. Di Flutter, hampir semuanya adalah widget: teks, tombol, padding, bahkan layar. Widget-widget itu disusun bertingkat seperti pohon, dan itulah yang disebut widget tree.
Widget paling atas jadi akar (root), lalu di dalamnya ada widget lain yang jadi anaknya. Widget yang membungkus disebut parent, yang dibungkus disebut child.
Hubungan ini penting karena parent menentukan batas ukuran dan posisi child, sedangkan data dan tema diturunkan dari parent ke child. Kalau parent berubah dan dibangun ulang, child-nya ikut diproses ulang.

2. Widget yang saya gunakan dalam mobile app porto ini,
- MaterialApp: pembungkus utama aplikasi, mengatur tema, judul, dan halaman awal.
- Scaffold: kerangka halaman (app bar, body, bottom navigation, dll).
- AppBar: bar di bagian atas halaman, biasanya berisi judul.
- Text: menampilkan tulisan.
- Image / CircleAvatar: menampilkan gambar atau foto profil.
- Container: kotak serbaguna untuk atur warna, ukuran, margin, dan dekorasi.
- Column: menyusun widget ke bawah (vertikal).
- Row: menyusun widget ke samping (horizontal).
- Padding: memberi jarak di sekeliling widget.
- SizedBox: memberi jarak kosong atau mengatur ukuran tetap.
- Center: menaruh child di tengah.
- ListView: daftar yang bisa di-scroll (misalnya daftar project atau skill).
- Card: kotak dengan bayangan, cocok untuk menampilkan item project.
- Icon: menampilkan ikon.
- ElevatedButton / TextButton / IconButton: tombol yang bisa ditekan.
- Expanded / Flexible: membagi sisa ruang di dalam Row atau Column.
- SingleChildScrollView: membuat halaman bisa di-scroll.

3. MaterialApp adalah widget yang menyiapkan hal-hal dasar aplikasi bergaya material design.
Alasan dipakai sebagai root: widget seperti Scaffold, AppBar, Navigator, dan Theme butuh “lingkungan” yang disediakan MaterialApp supaya bisa jalan. Karena itu dia ditaruh paling atas, supaya semua widget di bawahnya otomatis dapat tema dan navigasi yang sama.

4. 
- StatelessWidget: tampilannya tetap, tidak punya data yang berubah selama aplikasi jalan. Sekali dibangun, isinya sama terus.
- StatefulWidget: punya state (data yang bisa berubah). Kalau datanya berubah dan kita panggil setState(), tampilannya ikut diperbarui.

Pilih Stateless kalau tampilannya statis, misalnya halaman profil yang isinya teks dan gambar saja. Pilih Stateful kalau ada yang berubah karena interaksi atau waktu, misalnya tombol ganti tema gelap/terang, counter, isi form, checkbox, atau data yang dimuat dari internet.

5. BuildContext adalah penanda posisi sebuah widget di dalam widget tree. Lewat context ini, widget tahu di mana keberadaannya dan bisa mengambil informasi dari widget di atasnya (parent).

Penggunaannya di dalam build(BuildContext context) untuk mengambil tema, ukuran layar, memindahkan page, dan menampilkan snackbar atau dialog.
Tanpa context, widget tidak bisa “melihat” ke atas pohonnya untuk mengambil tema, ukuran layar, atau navigasi.

6. 
- Hot reload: kode yang baru diubah langsung dimasukkan ke aplikasi yang sedang jalan, dalam hitungan detik. State tetap tersimpan, jadi kamu tidak kembali ke awal. Cocok untuk ngubah tampilan, warna, atau teks.
- Hot restart: aplikasi dijalankan ulang dari awal, jadi state hilang dan semua kembali ke kondisi awal. Tetap lebih cepat daripada build ulang total.

Hot reload saja tidak akan cukup ketika:
- Mengubah nilai variabel global atau static yang sudah terlanjur diinisialisasi
- Mengubah isi main() atau initState() (karena hanya jalan sekali di awal)
- Mengubah StatelessWidget jadi StatefulWidget (atau sebaliknya)
- Mengubah enum atau tipe data tertentu

Kita harus hot restar atau full restart ketika:
- Menambah atau mengubah dependency di pubspec.yaml
- Menambah aset baru seperti gambar atau font
- Mengubah kode native (Android/iOS), izin di AndroidManifest.xml, atau konfigurasi Gradle
- Menambah plugin yang punya kode native


## Tugas 8

1.
- Navigator.push() berfungsi menumpuk halaman baru di atas halaman aktif sehingga pengguna masih bisa kembali ke halaman sebelumnya. 
- Navigator.pushReplacement() mengganti halaman aktif sekaligus menghapusnya dari tumpukan navigasi agar pengguna tidak bisa kembali ke halaman lama. 
- Navigator.pop() bertugas menutup halaman paling atas untuk kembali ke halaman persis di bawahnya. 

Untuk membuka formulir dari kartu aksi, metode yang digunakan adalah Navigator.push() agar pengguna tetap memiliki opsi untuk batal dan kembali ke halaman utama. Pada opsi Home di dalam drawer, Navigator.pushReplacement() digunakan untuk mengganti layar aktif dengan halaman utama sehingga tumpukan navigasi tetap bersih dan tidak menumpuk halaman yang sama berulang kali.

2. 
Scaffold bertindak sebagai kerangka dasar tata letak material pada setiap layar, sementara AppBar menjaga konsistensi bagian kepala halaman (judul dan tombol menu) dan Drawer menyatukan akses navigasi samping yang seragam di seluruh aplikasi. Untuk menjaga keseragaman warna tema di lebih dari satu halaman, tema warna didefinisikan secara terpusat pada ThemeData di level MaterialApp, lalu dipanggil menggunakan Theme.of(context).colorScheme.primary—misalnya untuk menyamakan warna latar AppBar di halaman utama dengan warna tombol simpan pada halaman formulir.

3.
Tata letak vertikal seperti Column dipilih untuk formulir karena menciptakan alur pengisian data yang alami dan mudah dibaca dari atas ke bawah. Ketika ruang layar terbatas—seperti pada layar kecil atau saat papan ketik muncul—widget penggulir seperti SingleChildScrollView mencegah terjadinya bottom overflow dengan memungkinkan seluruh konten formulir digulir. Di sisi lain, widget pengatur jarak seperti SizedBox atau Padding menjaga agar antar-kolom input tetap memiliki batas visual yang rapi dan tidak saling berhimpitan.

4.
Saat tombol Simpan ditekan, GlobalKey<FormState> berperan sebagai pengenal unik untuk mengakses dan mengontrol status seluruh Form dari luar, sedangkan pemanggilan method validate() memicu eksekusi fungsi validator pada setiap kolom input secara serentak guna memeriksa kelayakan data. Sebagai contoh, pada input jumlah atau harga, nilai negatif seperti "-10" atau string kosong "" akan ditolak oleh validasi. Mengatur jenis input atau papan ketik (TextInputType.number) saja belum cukup karena tidak mencegah pengguna mengosongkan kolom, memasukkan simbol minus secara tidak valid, maupun menempelkan (paste) teks huruf dari clipboard.