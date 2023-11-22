# dekappy

Nama   : Dinda Kirana Khairunnisa

Kelas  : PBP - C

NPM    : 2206082480

## TUGAS 7
1. **Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?**
   
   Stateless widget adalah jenis widget yang bersifat statis. Hal tersebut berarti stateless widget tidak dapat diubah atau bersifat immutable. Stateless widget tidak dapat mengubah keadaannya selama runtime aplikasi, yang berarti widget ini tidak dapat digambar ulang saat aplikasi berjalan. Contoh dari stateless widget adalah Icon, IconButton, dan Text.

   Stateful Widget adalah widget yang dapat mengubah properti-propertinya selama runtime. Mereka bersifat dinamis, dapat diubah (mutable), dan dapat digambar ulang beberapa kali selama masa hidupnya. Mereka dapat mengubah penampilannya sebagai respons terhadap peristiwa yang dipicu oleh interaksi pengguna atau ketika menerima data. Contoh stateful widget adalah Checkbox, Tombol Radio, Slider, InkWell, Form, dan TextField.

   Berdasarkan penjelasan tersebut, dapat disimpulkan bahwa perbedaan utama dari stateless widget dan stateful widget adalah stateless widget bersifat statis dan tidak bergantung pada perubahan data atau perubahan perilaku. Sedangkan, stateful widget adalah widget dinamis dan dapat diperbarui selama runtime berdasarkan tindakan pengguna atau perubahan data.

2. **Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.**
   MyHomePage (Stateless Widget):

      --> MyHomePage adalah widget utama yang merupakan stateless widget. Ini digunakan untuk mengatur tampilan halaman utama aplikasi, membuat daftar item dan menampilkannya dalam bentuk ItemCard.
   
      --> Scaffold (Stateless Widget) digunakan untuk membuat kerangka aplikasi. Ini menyediakan kerangka kerja umum untuk aplikasi Flutter, termasuk AppBar dan body.
   
      --> AppBar (Stateless Widget) adalah bagian atas aplikasi yang berisi judul aplikasi. Ini menampilkan teks "Dekappy" sebagai judul aplikasi.
   
      --> SingleChildScrollView (Stateless Widget) digunakan untuk membungkus kontennya agar dapat di-scroll jika kontennya lebih besar dari layar. Ini membantu menghindari overflow konten.
   
      --> Padding (Stateless Widget) digunakan untuk memberikan jarak atau padding pada elemen-elemen di dalamnya. Ini digunakan untuk memberikan jarak di sekitar elemen-elemen dalam kolom.
   
      --> Column (Stateless Widget) digunakan untuk menampilkan elemen-elemen secara vertikal. Ini digunakan untuk menampilkan judul dan daftar ItemCard secara vertikal.
   
      --> Text (Stateless Widget) digunakan untuk menampilkan teks. Ini menampilkan teks "Dekappy Shop" sebagai judul toko.
   
      --> GridView.count (Stateless Widget) digunakan untuk membuat tampilan grid dengan jumlah kolom yang telah ditentukan. Ini digunakan untuk menampilkan daftar ItemCard dalam grid.
   
      --> ItemCard (Stateless Widget) adalah custom widget yang dibuat untuk menampilkan setiap item dalam daftar. Ini menggunakan berbagai widget seperti Material, InkWell, Container, Icon, dan Text untuk menampilkan item dengan warna latar belakang yang berbeda berdasarkan nama item.
   
      --> Material (Stateless Widget) adalah kontainer yang mengatur tampilan kartu dengan latar belakang yang berbeda berdasarkan nama item.
   
      --> InkWell (Stateless Widget) digunakan untuk membuat area yang responsif terhadap sentuhan, sehingga ketika di-klik, itu memicu aksi tertentu.
   
      --> Container (Stateless Widget) digunakan untuk mengelola tata letak elemen-elemen di dalamnya. Ini digunakan untuk menyusun ikon dan teks.
   
      --> Icon (Stateless Widget) digunakan untuk menampilkan ikon. Ini menampilkan ikon yang sesuai dengan item.
      Text (Stateless Widget):
   

4. **Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step**
  
   **-> Membuat sebuah program Flutter baru dengan tema inventory seperti tugas-tugas sebelumnya.**

   Checklist ini diawali dengan menjalankan command berikut di dalam direktori dimana proyek disimpan.
  
    ```
    flutter create <dekappy>
    cd <dekappy>
    ```
  
    Command tersebut dilakukan untuk membuat sebuah proyek flutter bernama dekappy. Kemudian, proyek tersebut dijalankan dengan commaand ```flutter run```

   **-> Membuat tiga tombol sederhana dengan ikon dan teks untuk: Melihat daftar item (Lihat Item), Menambah item (Tambah Item), dan Logout (Logout).**

   Pada checklist ini, saya membuat tiga tombol tersebut dengan membuat class bernama Item terlebih dahulu

   ```
   class Item {
      final String name;
      final IconData icon;
    
      Item(this.name, this.icon);
    }
    ```
     Setelah itu, saya membuat list di dalam class MyHomePage dengan tipe Item yang berisi tombol melihat daftar item (Lihat Item), menambah item (Tambah Item), dan logout (Logout).

   ```
   final List<Item> items = [
    Item("Lihat Item", Icons.checklist),
    Item("Tambah Item", Icons.add_shopping_cart),
    Item("Logout", Icons.logout),
    ];
    ```

    **-> Memunculkan Snackbar dengan tulisan:**

      Untuk memunculkan snackbar yang berisi tulisan di setiap ketiga tombol yang sudah dibuat sebelumnya, saya membuat widget stateless baru seperti berikut.

   ```
   class ItemCard extends StatelessWidget {
      final Item item;
    
      const ItemCard(this.item, {super.key}); // Constructor
    
      @override
      Widget build(BuildContext context) {
        Color cardColor; // Warna latar belakang card
    
        // Tentukan warna berdasarkan nama item
        if (item.name == "Lihat Item") {
          cardColor = Colors.blue; // Warna biru untuk 'Lihat Item'
        } else if (item.name == "Tambah Item") {
          cardColor = Colors.green; // Warna hijau untuk 'Tambah Item'
        } else if (item.name == "Logout") {
          cardColor = Colors.red; // Warna merah untuk 'Logout'
        } else {
          cardColor = Colors.grey; // Warna default jika tidak ada yang cocok
        }
    
        return Material(
          color: cardColor, // Atur warna latar belakang card
          child: InkWell(
            // Area responsive terhadap sentuhan
            onTap: () {
              // Memunculkan SnackBar ketika diklik
              ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("Kamu telah menekan tombol ${item.name}!")));
            },
            child: Container(
              // Container untuk menyimpan Icon dan Text
              padding: const EdgeInsets.all(8),
              child: Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(
                      item.icon,
                      color: Colors.white,
                      size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                      item.name,
                      textAlign: TextAlign.center,
                      style: const TextStyle(color: Colors.white),
                    ),
                  ],
                ),
              ),
            ),
          ),
        );
      }
    }
    ```
   Pada kode tersebut, saya juga mengubah warna setiap tombol menjadi merah, hijau, dan biru.


## TUGAS 8
1. Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!

   
    Dalam Flutter, `Navigator.push()` dan `Navigator.pushReplacement()` adalah dua metode yang digunakan untuk navigasi antar halaman. `Navigator.push()` memungkinkan navigasi ke halaman baru dengan cara menambahkannya ke top of stack dari navigasi. Hal ini berarti halaman sebelumnya tetap ada dalam stack dan dapat kembali dilihat jika user menekan tombol kembali. Contoh dari penggunaan `Navigator.push()` adalah sebagai berikut.

      ```
      onTap: () {
       // Memunculkan SnackBar ketika diklik
       ScaffoldMessenger.of(context)
         ..hideCurrentSnackBar()
         ..showSnackBar(SnackBar(
             content: Text("Kamu telah menekan tombol ${item.name}!")));
             if (item.name == "Tambah Item") {
               Navigator.push(context,
               MaterialPageRoute(builder: (context) => const ShopFormPage()));
             }
      },
      ```
      
      Pada kode tersebut, saya menggunakan `Navigator.push()` untuk melakukan navigasi ke halaman ShopFormPage. Akan tetapi, halaman sebelumnya tidak akan terhapus karena hanya menambahkan halaman ke top of stack. Oleh karena itu, user masih bisa kembali ke halaman sebelumnya.

      Sebaliknya, `Navigator.pushReplacement()` melakukan navigasi ke halaman baru dengan menggantikan halaman saat ini dalam stack navigasi. Dengan demikian, halaman sebelumnya dihapus dari stack dan tidak dapat dilihat lagi jika user menekan tombol kembali. Contoh penggunaannya adalah sebagai berikut.

   ```
   // Bagian redirection ke MyHomePage
   onTap: () {
     Navigator.pushReplacement(
         context,
         MaterialPageRoute(
           builder: (context) => MyHomePage(),
         ));
   },
   ```
      Code tersebut melakukan redirection ke halaman utama. Ketika tombol diklik, maka halaman saat ini akan digantikan dengan halaman MyHomePage. Terdapat contoh lain sebagai berikut.

   ```
   // Bagian redirection ke ShopFormPage
   onTap: () {
     Navigator.pushReplacement(
     context,
     MaterialPageRoute(
         builder: (context) => const ShopFormPage(),
     ));
   
   },
   ```
      Code tersebut melakukan navigasi ke halaman ShopFormPage. Ketika tombol diklik, maka halaman saat ini akan digantikan dengan halaman ShopFormPage dan dihapus dari stack.

2. Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!

      - GridView : Menata elemen-elemennya dalam susunan grid dua dimensi. Aplikasi dari widget ini biasa terlihat dalam format grid seperti galeri foto atau keyboard virtual.
      - ListView : Membuat list scrollable dari widget anak-anaknya. Digunakan untuk membuat list yang panjang dan bisa discroll seperti daftar chat atau feed berita.
      - Column : Menempatkan elemen-elemennya secara berurutan dari atas ke bawah. Sangat berguna untuk desain yang memerlukan penyusunan vertikal, seperti form isian atau daftar tertata.
      - Row : Menempatkan elemen-elemennya dalam satu baris horizontal. Cocok untuk desain yang memerlukan elemen-elemen disusun secara horizontal, seperti bilah alat atau bilah status
      - Stack : Menumpuk elemen-elemennya satu atas yang lain. Ini sering digunakan untuk menciptakan tampilan bertingkat, seperti meletakkan lencana notifikasi di atas ikon aplikasi.
      - Container : Widget yang menggabungkan common painting, positioning, dan sizing widgets. Digunakan sebagai blok bangunan dasar untuk membuat bentuk, mengatur padding, margin, menambahkan background, dll.
      - Padding : Menambahkan ruang dalam di sekitar elemennya. Ini digunakan untuk memberikan ruang ekstra di sekitar elemen tertentu, memisahkannya dari elemen lain.
      - Align : Menempatkan elemennya berdasarkan parameter penjajaran yang ditetapkan. Digunakan untuk mengatur posisi elemen secara spesifik dalam wadah yang lebih besar.

3. Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!

      --> TextFormField untuk "Nama Produk": Ini digunakan untuk memungkinkan user memasukkan nama item. Validasi memastikan bahwa input tidak boleh kosong. Alasan menggunakan    elemen ini adalah karena nama produk adalah string teks, dan TextFormField adalah cara standar untuk mengumpulkan input teks dalam Flutter.
   
      --> TextFormField untuk "Amount" (Jumlah): Ini digunakan untuk memasukkan jumlah produk. Validasi pada input ini memastikan bahwa input tidak boleh kosong dan harus berupa angka. TextFormField digunakan disini karena dapat di-customize untuk menerima input numerik dan validasi untuk memastikan data yang dimasukkan sesuai dengan kebutuhan.

      --> TextFormField untuk "Harga": Mirip dengan field "Amount", field ini digunakan untuk memasukkan harga produk. Karena harga produk adalah nilai numerik, TextFormField diperlukan untuk menangkap input numerik dan memvalidasi bahwa input tidak kosong dan harus berupa angka.

      --> TextFormField untuk "Deskripsi": Elemen ini digunakan untuk memasukkan deskripsi produk. Menggunakan TextFormField untuk deskripsi memungkinkan user untuk memasukkan teks yang lebih panjang, dan validasi memastikan bahwa deskripsi tidak ditinggalkan kosong.


4. Bagaimana penerapan clean architecture pada aplikasi Flutter?

      Penerapan Clean Architecture pada aplikasi Flutter biasanya terdiri dari tiga lapisan utama:
   
      --> Presentasi (UI): Berisi komponen antarmuka pengguna, seperti widget, layar, dan tampilan. Ini menangani interaksi pengguna dan rendering UI.
   
      --> Lapisan Domain (Bisnis): Mewakili logika bisnis inti dari aplikasi.
   
      --> Lapisan Data & Platform: Lapisan data berada di lapisan terluar. Lapisan ini terdiri dari kode sumber data seperti konsumsi Rest API, akses ke database lokal, Firebase, atau sumber lain. Pada lapisan ini, biasanya ada kode platform yang membangun UI (widget).
      
      --> Lapisan Presentasi: Lapisan presentasi terdiri dari kode untuk mengakses data aplikasi dari repositori. Terdapat kode untuk manajemen status seperti penyedia, BLoC, dan sebagainya.
      
      Setiap lapisan bergantung pada lapisan lain. Lapisan terluar akan bergantung pada lapisan dalam dan seterusnya. Lapisan yang tidak bergantung pada lapisan lain di sini hanyalah lapisan domain (independen) yang merupakan kode untuk logika bisnis2.

5. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step!

      **-> Membuat minimal satu halaman baru pada aplikasi, yaitu halaman formulir tambah item baru dan memakai minimal tiga elemen input, yaitu name, amount, description. Tambahkan elemen input sesuai dengan model pada aplikasi tugas Django yang telah kamu buat..**

      Pada checklist ini, langkah pertama yang saya lakukan adalah membuat file baru dalam berkas lib dengan nama dekappy_form.dart. Kemudian saya menambahkan elemen input, yaitu name, amount, price, dan description seperti berikut ini.
      ```
      class ShopFormPage extends StatefulWidget {
        const ShopFormPage({super.key});
      
        @override
        State<ShopFormPage> createState() => _ShopFormPageState();
      }
      
      class _ShopFormPageState extends State<ShopFormPage> {
        final _formKey = GlobalKey<FormState>();
        String _name = "";
        int _price = 0;
        int _amount = 0;
        String _description = "";
      }
      ```

      **--> Memiliki sebuah tombol save***

      Pada checklist ini, saya membuat sebuah tombol save.
      ```
         Align(
           alignment: Alignment.bottomCenter,
           child: Padding(
             padding: const EdgeInsets.all(8.0),
             child: ElevatedButton(
               style: ButtonStyle(
                 backgroundColor:
                     MaterialStateProperty.all(Colors.indigo),
               ),
               onPressed: () {
                 if (_formKey.currentState!.validate()) {}
               },
               child: const Text(
                 "Save",
                 style: TextStyle(color: Colors.white),
               ),
             ),
           ),
         ),
      ```

   **--> Setiap elemen input di formulir juga harus divalidasi dengan ketentuan sebagai berikut: Setiap elemen input tidak boleh kosong dan Setiap elemen input harus berisi data dengan tipe data atribut modelnya.**

   Saya melakukan validasi untuk memastikan setiap elemen input tidak kosong dan sesuai dengan tipe data atribut modelnya.
   ```
   validator: (String? value) {
     if (value == null || value.isEmpty) {
       return "Amount tidak boleh kosong!";
     }
     if (int.tryParse(value) == null) {
       return "Amount harus berupa angka!";
     }
     return null;
   },
   ```


   **--> Mengarahkan pengguna ke halaman form tambah item baru ketika menekan tombol Tambah Item pada halaman utama.**

      Pada checklist ini, saya menggunakan navigator.push() untuk diarahkan ke halaman form ketika tambah item ditekan.
      ```
      if (item.name == "Tambah Item") {
         Navigator.push(context,
         MaterialPageRoute(builder: (context) => const ShopFormPage()));
      }
      ```

   **--> Memunculkan data sesuai isi dari formulir yang diisi dalam sebuah pop-up setelah menekan tombol Save pada halaman formulir tambah item baru.**

      Pada checklist ini, saya akan memunculkan data sesuai isi dari formulir yang diisi dalam sebuah pop-up setelah menekan tombol Save pada halaman formulir tambah item baru. Ketika pengguna menekan tombol Save, aplikasi akan melakukan validasi dan jika semua data benar, aplikasi akan menampilkan dialog pop-up dengan data yang sesuai dengan apa yang telah diisi pengguna dalam form tersebut. Tombol OK ketika ditekan, akan menutup dialog dengan memanggil Navigator.pop(context), yang menghapus AlertDialog dari tampilan. Setelah dialog ditampilkan, _formKey.currentState!.reset() membersihkan form, sehingga formulir bersih dari data sebelumnya.

   ```
      onPressed: () {
          if (_formKey.currentState!.validate()) {
            showDialog(
              context: context,
              builder: (context) {
                return AlertDialog(
                  title: const Text('Produk berhasil tersimpan'),
                  content: SingleChildScrollView(
                    child: Column(
                      crossAxisAlignment: CrossAxisAlignment.start,
                      children: [
                        Text('Nama: $_name'),
                        Text('Amount: $_amount'),
                        Text('Harga: $_price'),
                        Text('Deskripsi: $_description'),
                      ],
                    ),
                  ),
                  actions: [
                    TextButton(
                      child: const Text('OK'),
                      onPressed: () {
                        Navigator.pop(context);
                      },
                    ),
                  ],
                );
              },
   ```

   **--> Membuat sebuah drawer pada aplikasi sesuai dengan ketentuan.**

      Membuat sebuah drawer Saya membuat file left_drawer.dart pada lib/widgets. Lalu, saya membuat 2 opsi untuk ke halaman utama dan tambah item dalam ListTile anak dari ListView. Ketika salah satu opsi ditekan, Navigator.pushReplacement akan navigasi ke halaman yang sesuai.

      ```
   Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
         ...
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Halaman Utama'),
            // Bagian redirection ke MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                  context,
                  MaterialPageRoute(
                    builder: (context) => MyHomePage(),
                  ));
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Tambah Produk'),
            // Bagian redirection ke ShopFormPage
            onTap: () {
              Navigator.pushReplacement(
              context,
              MaterialPageRoute(
                  builder: (context) => const ShopFormPage(),
              ));

            },
          ),

        ],
      ),
    );
   ```


## Tugas 9
1. Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?

   Ya, bisa dilakukan dengan menggunakan ```Map<String, dynamic>``` untuk menangani data JSON secara langsung. Pengambilan data JSON tanpa model memberika fleksibilitas karena developer tidak perlu mendefinisikan struktur data terlebih dahulu. Hal ini berguna untuk prototyping cepat atau ketika berinteraksi dengan API yang sering berubah. Developer juga tidak perlu menulis kode tambahan untuk serialisasi dan deserialisasi data, yang bisa menghemat waktu pengembangan. Akan tetapi, jika dibandingkan dengan pembuatan model, membuat model kelas untuk JSON lebih membantu dalam menjaga kode menjadi lebih terorganisir dan mudah dibaca. Selain itu, pembuatan model membuat kode lebih mudah diperbarui. Oleh karena itu, penggunaan tanpa model lebih cocok untuk skenario ketika struktur data tidak tetap.

2. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.

   Fungsi dari CookieRequest adalah untuk menyimpan dan mengelola data sesi pengguna, seperti token autentikasi atau preferensi pengguna. Hal ini sangat penting dalam aplikasi yang membutuhkan pemeliharaan sesi pengguna, seperti penggunaan fitur login yang ada dalam aplikasi dekappy ini.

   Alasan mengapa sebuah instance CookieRequest perlu dibagikan ke semua komponen dalam aplikasi adalah untuk menjaga konsistensi sesi pengguna di seluruh aplikasi. Ini memastikan bahwa setiap komponen aplikasi dapat mengakses dan memanfaatkan data sesi yang sama. Misalnya, jika pengguna telah masuk (login), cookie yang memuat token autentikasi harus dapat diakses oleh semua komponen yang memerlukan verifikasi autentikasi, sehingga pengguna tidak perlu masuk berulang kali saat berpindah antar fitur aplikasi.

3. Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.

   Mekanisme pengambilan data dari JSON untuk ditampilkan pada aplikasi Flutter melibatkan beberapa langkah penting. Pertama, kita perlu mendefinisikan sebuah model dalam Flutter yang sesuai dengan struktur data JSON yang diharapkan. Model ini adalah kelas Dart dengan properti yang sesuai dengan kunci dalam data JSON. Di dalam kelas ini, kita juga mengimplementasikan metode fromJson dan toJson untuk mengonversi data antara format JSON dan objek Dart.

   Setelah model didefinisikan, langkah selanjutnya adalah mengambil data dari web service menggunakan paket http di Flutter. Kita mengirim permintaan HTTP ke endpoint web service dan menerima respons. Respons ini biasanya dalam format JSON, yang kemudian kita parse menggunakan metode jsonDecode dari Dart untuk mengubahnya menjadi objek Dart (Map atau List).

   Selanjutnya, kita menggunakan metode fromJson dari model yang telah kita buat untuk mengubah data JSON yang telah diparse menjadi objek model Dart. Jika data JSON adalah array, kita akan mengiterasi setiap item dan mengonversi setiap item menjadi instance model.

   Untuk menampilkan data di Flutter, kita menggunakan berbagai widget yang disediakan oleh Flutter. Dalam tugas ini, saya menggunakan ListView.builder untuk menampilkan daftar item

4. Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.

   Mekanisme autentikasi dari input data akun di Flutter ke proses autentikasi di Django dan kemudian menampilkan menu di Flutter berlangsung dalam beberapa tahap terintegrasi. Pertama, di sisi Flutter, pengguna memasukkan detail akun mereka, seperti username dan password, melalui antarmuka pengguna. Flutter kemudian mengirimkan data ini ke server Django menggunakan permintaan HTTP dengan metode POST dan data dikirim dalam format JSON. Setelah menerima data, Django memprosesnya untuk autentikasi. Proses ini melibatkan pengecekan ke database untuk memastikan bahwa detail akun yang diberikan valid dan sesuai dengan yang ada di database. Jika berhasil, Django akan menghasilkan token yang dikirim kembali ke Flutter sebagai bagian dari respons autentikasi.

   Di sisi Flutter, aplikasi menanggapi respons dari Django. Jika autentikasi berhasil, aplikasi menyimpan token untuk sesi pengguna dan mengarahkan mereka ke halaman utama atau dashboard aplikasi. Ini memungkinkan pengguna mengakses fitur-fitur yang tersedia sesuai dengan hak akses mereka. Sebaliknya, jika autentikasi gagal, Flutter akan menampilkan pesan kesalahan dan meminta pengguna untuk mencoba lagi. Setelah pengguna berhasil masuk, mereka dapat melihat dan berinteraksi dengan menu atau fitur aplikasi yang tersedia, yang sekarang diakses dengan keamanan dan verifikasi identitas yang telah dilakukan oleh Django. Proses ini menjamin keamanan dalam transaksi data dan memastikan bahwa hanya pengguna terotentikasi yang dapat mengakses fitur tertentu dalam aplikasi.

5. Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.

   ```Scaffold```: Widget ini digunakan sebagai kerangka dasar untuk layout halaman di Flutter. Ini menyediakan struktur dasar seperti appBar, body, dan lainnya.

```AppBar```: Widget ini digunakan untuk menampilkan app bar di bagian atas layar. Di dalamnya, Anda menampilkan judul halaman yang diambil dari data item.

```Form```: Widget ini digunakan untuk membuat formulir yang dapat diisi oleh pengguna. Ini membantu dalam validasi dan pengelolaan data formulir.

```IconButton```: Widget ini digunakan untuk menampilkan tombol ikon di app bar. Dalam kasus ini, Anda menggunakan ikon panah kembali (Icons.arrow_back) yang, ketika ditekan, akan memicu fungsi untuk kembali ke halaman sebelumnya (Navigator.pop(context)).

```Padding```: Widget ini digunakan untuk memberikan padding di sekitar konten lainnya, dalam hal ini di sekitar kolom yang menampilkan detail produk.

```Column```: Widget ini digunakan untuk menata beberapa widget lainnya secara vertikal. Ini digunakan untuk menampilkan informasi detail produk.

```Text```: Widget ini digunakan untuk menampilkan teks di layar. Dalam hal ini, digunakan untuk menampilkan berbagai atribut dari item, seperti nama, jumlah, harga, deskripsi, dan kategori

```TextFormField```: Widget ini digunakan untuk menerima input teks dari pengguna. Setiap TextFormField dikonfigurasi dengan dekorasi, validator, dan fungsi onChanged.

```ElevatedButton```: Widget ini digunakan untuk membuat tombol yang, ketika ditekan, akan menjalankan fungsi yang diberikan. Dalam kasus ini, tombol digunakan untuk mengirim data formulir ke server

```Align```: Widget ini digunakan untuk mengatur posisi widget anaknya, dalam hal ini digunakan untuk menempatkan tombol di bagian bawah

```SingleChildScrollView```: Widget ini memungkinkan pengguna untuk menggulir melalui konten yang mungkin tidak muat di layar

```FutureBuilder```: Widget ini digunakan untuk membangun UI berdasarkan hasil dari Future. Dalam kasus ini, digunakan untuk membangun UI setelah data dari fetchItem() diperoleh

```ListView.builder```: Widget ini digunakan untuk membuat daftar item yang dapat digulir. Ini membangun item daftar secara dinamis berdasarkan data yang diperoleh

```InkWell```: Widget ini digunakan untuk menangani ketukan pada item daftar. Ketika item ditekan, ia akan menavigasi ke DetailProductPage dengan data item yang relevan

```Container```: Widget ini digunakan untuk mengelompokkan dan memberikan margin, padding, dan tata letak lainnya pada item daftar

```SizedBox```: Widget ini digunakan untuk memberikan jarak antar widget dalam Column.

ShopCard: Widget ini adalah widget kustom, digunakan untuk menampilkan kartu untuk setiap item dalam grid. Setiap ShopCard mewakili sebuah item dalam aplikasi

```LeftDrawer```: Widget adalah widget kustom, digunakan untuk menampilkan menu drawer di sisi kiri layar.

```Drawer```: Widget ini digunakan untuk membuat menu drawer yang dapat ditarik dari sisi layar. Ini memberikan navigasi tambahan dalam aplikasi

```ListView```: Widget ini digunakan untuk membuat daftar item yang dapat discroll. Dalam konteks ini, digunakan untuk menampilkan item-item dalam drawer.

```ListTile```: Widget ini digunakan untuk membuat item yang dapat diklik di dalam ListView. Dalam hal ini, digunakan untuk membuat item navigasi di drawer

```Icon```: Widget ini digunakan untuk menampilkan ikon di samping teks dalam ListTile

```Material```: Widget ini digunakan sebagai dasar untuk menampilkan komponen UI yang mengikuti Material Design. Di sini, digunakan untuk memberikan warna latar belakang pada kartu

6. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step!

   **--> Membuat halaman login pada proyek tugas Flutter.**

   Pada checklist ini, langkah pertama yang saya lakukan adalah aplikasi baru bernama authentication di proyek Django saya. Kemudian, saya membuat fungsi login di views.py dan melakukan routing. Setelah itu, saya membuat file baru bernama login.dart di falam folder screens. File tersebut saya isi dengan kode berikut.
   ```
   import 'package:dekappy/screens/menu.dart';
   import 'package:flutter/material.dart';
   import 'package:pbp_django_auth/pbp_django_auth.dart';
   import 'package:provider/provider.dart';
   
   void main() {
       runApp(const LoginApp());
   }
   
   class LoginApp extends StatelessWidget {
   const LoginApp({super.key});
   
   @override
   Widget build(BuildContext context) {
       return MaterialApp(
           title: 'Login',
           theme: ThemeData(
               primarySwatch: Colors.blue,
       ),
       home: const LoginPage(),
       );
       }
   }
   
   class LoginPage extends StatefulWidget {
       const LoginPage({super.key});
   
       @override
       _LoginPageState createState() => _LoginPageState();
   }
   
   class _LoginPageState extends State<LoginPage> {
       final TextEditingController _usernameController = TextEditingController();
       final TextEditingController _passwordController = TextEditingController();
   
       @override
       Widget build(BuildContext context) {
           final request = context.watch<CookieRequest>();
           return Scaffold(
               appBar: AppBar(
                   title: const Text('Login'),
               ),
               body: Container(
                   padding: const EdgeInsets.all(16.0),
                   child: Column(
                       mainAxisAlignment: MainAxisAlignment.center,
                       children: [
                           TextField(
                               controller: _usernameController,
                               decoration: const InputDecoration(
                                   labelText: 'Username',
                               ),
                           ),
                           const SizedBox(height: 12.0),
                           TextField(
                               controller: _passwordController,
                               decoration: const InputDecoration(
                                   labelText: 'Password',
                               ),
                               obscureText: true,
                           ),
                           const SizedBox(height: 24.0),
                           ElevatedButton(
                               onPressed: () async {
                                   String username = _usernameController.text;
                                   String password = _passwordController.text;
   
                                   // Cek kredensial
                                   // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                                   // Untuk menyambungkan Android emulator dengan Django pada localhost,
                                   // gunakan URL http://10.0.2.2/
                                   final response = await request.login("http://127.0.0.1:8000/auth/login/", {
                                   'username': username,
                                   'password': password,
                                   });
                       
                                   if (request.loggedIn) {
                                       String message = response['message'];
                                       String uname = response['username'];
                                       Navigator.pushReplacement(
                                           context,
                                           MaterialPageRoute(builder: (context) => MyHomePage()),
                                       );
                                       ScaffoldMessenger.of(context)
                                           ..hideCurrentSnackBar()
                                           ..showSnackBar(
                                               SnackBar(content: Text("$message Selamat datang, $uname.")));
                                       } else {
                                       showDialog(
                                           context: context,
                                           builder: (context) => AlertDialog(
                                               title: const Text('Login Gagal'),
                                               content:
                                                   Text(response['message']),
                                               actions: [
                                                   TextButton(
                                                       child: const Text('OK'),
                                                       onPressed: () {
                                                           Navigator.pop(context);
                                                       },
                                                   ),
                                               ],
                                           ),
                                       );
                                   }
                               },
                               child: const Text('Login'),
                           ),
                       ],
                   ),
               ),
           );
       }
   }
   ```
   Kemudan, saya mengubah kode pada main.dart menjadi seperti berikut.
   ```
   child: MaterialApp(
    title: 'Flutter App',
    theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
        useMaterial3: true,
    ),
    home: LoginPage()),
   ```

   **--> Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.**

   Langkah pertama yang saya lakukan adala menginsta package berikut.
   ```
   flutter pub add provider
   flutter pub add pbp_django_auth
   ```

   Kemudian, saya mengubah kode pada main.dart untuk menyediakan cookierequest library.
   ```
   class MyApp extends StatelessWidget {
    const MyApp({Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        return Provider(
            create: (_) {
                CookieRequest request = CookieRequest();
                return request;
            },
            child: MaterialApp(
                title: 'Flutter App',
                theme: ThemeData(
                    colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
                    useMaterial3: true,
                ),
                home: LoginPage()),
               );
       }
   }
   ```

   **--> Membuat model kustom sesuai dengan proyek aplikasi Django.**

   Pada checklist ini, saya copy data JSON dan paste di Quicktype. Kemudian, saya membuat folder baru di dalam lib dengan nama models. Lalu, membuat file baru bernama ```product.dart``` dan paste kode yang sudah dicopy sebelumnya di file tersebut.

   **--> Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django yang telah kamu deploy.**

   Pada checklist ini, saya membuat file baru bernama ```list_product.dart``` di dalam folder screens. Kemudian, saya mengisi file tersebut dengan kode berikut.
   ```
   class _ProductPageState extends State<ProductPage> {
     Future<List<Product>> fetchProduct() async {
       var url = Uri.parse('http://127.0.0.1:8000/json/');
       var response = await http.get(
         url,
         headers: {"Content-Type": "application/json"},
       );
   
       // melakukan decode response menjadi bentuk json
       var data = jsonDecode(utf8.decode(response.bodyBytes));
   
       // melakukan konversi data json menjadi object Product
       List<Product> list_product = [];
       for (var d in data) {
         if (d != null) {
           list_product.add(Product.fromJson(d));
         }
       }
       return list_product;
     }
   ```
   Class tersebut berguna untuk memproses daftar produk dari JSON menjadi object Product.

   ```
     Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text('Product'),
        ),
        drawer: const LeftDrawer(),
        body: FutureBuilder(
            future: fetchProduct(),
            builder: (context, AsyncSnapshot snapshot) {
              if (snapshot.data == null) {
                return const Center(child: CircularProgressIndicator());
              } else {
                if (!snapshot.hasData) {
                  return const Column(
                    children: [
                      Text(
                        "Tidak ada data produk.",
                        style:
                            TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                      ),
                      SizedBox(height: 8),
                    ],
                  );
                } else {
                  return ListView.builder(
                    itemCount: snapshot.data!.length,
                    itemBuilder: (_, index) {
                      // Mengambil data produk saat ini
                      var product = snapshot.data![index];

                      return InkWell(
                        onTap: () {
                          // Navigasi ke halaman detail produk dengan data produk
                          Navigator.push(
                            context,
                            MaterialPageRoute(
                              builder: (context) =>
                                  ProductDetailPage(product: product),
                            ),
                          );
                        },
                        child: Container(
                          margin: const EdgeInsets.symmetric(
                              horizontal: 16, vertical: 12),
                          padding: const EdgeInsets.all(20.0),
                          child: Column(
                            mainAxisAlignment: MainAxisAlignment.start,
                            crossAxisAlignment: CrossAxisAlignment.start,
                            children: [
                              Text(
                                product.fields.name,
                                style: const TextStyle(
                                  fontSize: 18.0,
                                  fontWeight: FontWeight.bold,
                                ),
                              ),
                              const SizedBox(height: 10),
                              Text("${product.fields.price}"),
                              const SizedBox(height: 10),
                              Text("${product.fields.description}"),
                            ],
                          ),
                        ),
                      );
                    },
                  );
                }
              }
            }));
        }
      }
   ```
   Kode tersebut bertujuan untuk menampilkan name, amount, dan description dari masing-masing item yang ada dalam daftar item.

   **--> Membuat halaman detail untuk setiap item yang terdapat pada halaman daftar Item.**

   Pada checklist ini, saya membuat file baru bernama ```product_detail_page.dart``` di dalam folder screens. Kemudian, saya mengisi file tersebut dengan kode berikut

   ```
   
   import 'package:flutter/material.dart';
   import 'package:dekappy/models/product.dart';
   
   class ProductDetailPage extends StatelessWidget {
     final Product product;
   
     const ProductDetailPage({Key? key, required this.product}) : super(key: key);
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text(product.fields.name),
           actions: [
             IconButton(
               icon: Icon(Icons.arrow_back),
               onPressed: () => Navigator.pop(context),
             ),
           ],
         ),
         body: Padding(
           padding: EdgeInsets.all(16),
           child: Column(
             crossAxisAlignment: CrossAxisAlignment.start,
             children: <Widget>[
               Text("Name: ${product.fields.name}", style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold)),
               SizedBox(height: 10),
               Text("Price: ${product.fields.price}"),
               SizedBox(height: 10),
               Text("Items: ${product.fields.items}"),
               SizedBox(height: 10),
               Text("Description: ${product.fields.description}"),
             ],
           ),
         ),
       );
     }
   }
   ```
   

   

   

   
   

   

   
   
   
   

   
         
      
   



   
   
