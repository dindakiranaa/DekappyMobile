# dekappy

Nama   : Dinda Kirana Khairunnisa

Kelas  : PBP - C

NPM    : 2206082480

## Tugas 7
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
   
     
   
    

   



   
   
