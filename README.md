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
         
      
   



   
   
