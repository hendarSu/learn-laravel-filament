# Bagian 1: Dasar-Dasar Web Development

## Pengenalan Web Development

### Sejarah dan Evolusi Web
Web development telah berkembang pesat sejak awal kemunculannya. Dari era statis HTML hingga aplikasi web dinamis yang kompleks, teknologi web terus berevolusi. Pada awalnya, web hanya digunakan untuk berbagi dokumen teks sederhana. Namun, seiring waktu, web berkembang menjadi platform interaktif yang mendukung multimedia, aplikasi bisnis, dan jejaring sosial.

### Arsitektur Client-Server
Arsitektur client-server adalah dasar dari web development, di mana client (browser) mengirimkan permintaan ke server, dan server merespons dengan data yang diminta. Client bertanggung jawab untuk menampilkan antarmuka pengguna dan mengirimkan permintaan, sementara server menangani logika bisnis dan penyimpanan data.

### Frontend vs Backend Development
Frontend development berfokus pada tampilan dan interaksi pengguna, sedangkan backend development menangani logika bisnis dan pengelolaan data. Frontend developer bekerja dengan HTML, CSS, dan JavaScript untuk membuat antarmuka pengguna yang menarik dan responsif. Backend developer menggunakan bahasa pemrograman seperti PHP, Python, atau Node.js untuk mengelola data dan logika aplikasi.

## HTML: Struktur Halaman Web

### Sintaks HTML dan Elemen Dasar
HTML (HyperText Markup Language) adalah bahasa markup yang digunakan untuk membuat struktur halaman web. Elemen dasar HTML meliputi tag seperti `<div>`, `<p>`, `<a>`, dan lain-lain. Setiap elemen HTML memiliki tag pembuka dan penutup, serta atribut yang memberikan informasi tambahan.

### Semantic HTML
Semantic HTML menggunakan elemen yang memiliki makna khusus, seperti `<header>`, `<footer>`, `<article>`, dan `<section>`, untuk meningkatkan aksesibilitas dan SEO. Elemen-elemen ini membantu mesin pencari dan pembaca layar memahami struktur dan konten halaman web.

### Form dan Input
Form HTML memungkinkan pengguna untuk mengirimkan data ke server. Elemen input seperti `<input>`, `<textarea>`, dan `<select>` digunakan untuk menerima berbagai jenis data. Form juga dapat memiliki tombol submit untuk mengirimkan data ke server.

#### Studi Kasus: Membuat Form Kontak
Buat form kontak sederhana dengan HTML yang memungkinkan pengguna mengirimkan nama, email, dan pesan.

```html
<form action="/submit-contact" method="post">
  <label for="name">Nama:</label>
  <input type="text" id="name" name="name" required>
  
  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>
  
  <label for="message">Pesan:</label>
  <textarea id="message" name="message" required></textarea>
  
  <button type="submit">Kirim</button>
</form>
```

## CSS: Styling Halaman Web

### Selectors dan Properties
CSS (Cascading Style Sheets) digunakan untuk menambahkan gaya pada halaman web. Selectors digunakan untuk memilih elemen HTML, dan properties digunakan untuk menentukan gaya seperti warna, font, dan layout. Selectors dapat berupa tag, class, atau ID.

### Box Model dan Layout
Box model adalah konsep dasar dalam CSS yang menggambarkan bagaimana elemen HTML diatur dan diberi ruang. Box model terdiri dari margin, border, padding, dan content. Layout CSS mencakup teknik seperti flexbox dan grid untuk mengatur tata letak halaman.

### Responsive Web Design
Responsive web design memastikan bahwa halaman web terlihat dan berfungsi dengan baik di berbagai perangkat dan ukuran layar. Teknik seperti media queries digunakan untuk mencapai responsivitas.

#### Studi Kasus: Membuat Layout Responsif
Buat layout responsif sederhana menggunakan flexbox yang menampilkan dua kolom pada layar besar dan satu kolom pada layar kecil.

```css
.container {
  display: flex;
  flex-wrap: wrap;
}

.column {
  flex: 1;
  padding: 10px;
}

@media (max-width: 600px) {
  .column {
    flex: 100%;
  }
}
```

```html
<div class="container">
  <div class="column">Kolom 1</div>
  <div class="column">Kolom 2</div>
</div>
```

## JavaScript: Interaktivitas pada Web

### Sintaks Dasar JavaScript
JavaScript adalah bahasa pemrograman yang digunakan untuk menambahkan interaktivitas pada halaman web. Sintaks dasar JavaScript mencakup variabel, fungsi, dan kontrol alur. JavaScript dapat dijalankan di browser atau di server menggunakan Node.js.

### DOM Manipulation
DOM (Document Object Model) adalah representasi struktur halaman web. JavaScript dapat digunakan untuk memanipulasi DOM, seperti menambahkan, menghapus, atau mengubah elemen HTML. DOM manipulation memungkinkan pengembang untuk membuat halaman web yang dinamis dan interaktif.

### Event Handling
Event handling adalah proses menangani interaksi pengguna, seperti klik, input, dan hover. JavaScript menyediakan berbagai cara untuk menangani event, seperti menggunakan event listeners.

#### Studi Kasus: Menambahkan Interaktivitas pada Tombol
Buat tombol yang menampilkan pesan saat diklik menggunakan JavaScript.

```html
<button id="myButton">Klik Saya</button>
<p id="message"></p>

<script>
  document.getElementById('myButton').addEventListener('click', function() {
    document.getElementById('message').textContent = 'Tombol telah diklik!';
  });
</script>
