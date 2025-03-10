# Bagian 2: Pengenalan PHP

## Sejarah dan Pentingnya PHP

### Evolusi PHP
PHP (Hypertext Preprocessor) adalah bahasa pemrograman yang dirancang khusus untuk pengembangan web. PHP pertama kali dikembangkan oleh Rasmus Lerdorf pada tahun 1994 dan telah berkembang menjadi salah satu bahasa pemrograman paling populer untuk web development.

### Peran PHP dalam Pengembangan Web
PHP digunakan untuk membuat halaman web dinamis dan interaktif. PHP dapat diintegrasikan dengan berbagai database dan mendukung berbagai framework, seperti Laravel, untuk mempercepat pengembangan aplikasi web.

## Sintaks Dasar PHP

### Struktur Program PHP
Program PHP dimulai dengan tag `<?php` dan diakhiri dengan `?>`. Kode PHP dapat disisipkan ke dalam HTML untuk membuat halaman web dinamis.

```php
<?php
echo "Hello, World!";
?>
```

### Output dan Komentar
PHP menggunakan `echo` atau `print` untuk menghasilkan output. Komentar dapat ditulis menggunakan `//` untuk satu baris atau `/* */` untuk beberapa baris.

```php
<?php
// Ini adalah komentar satu baris
/* Ini adalah komentar
   beberapa baris */
echo "Hello, World!";
?>
```

## Variabel dan Tipe Data

### Jenis Tipe Data
PHP mendukung berbagai tipe data, termasuk integer, float, string, boolean, array, dan object. Variabel dalam PHP diawali dengan tanda `$`.

```php
<?php
$integer = 10;
$float = 10.5;
$string = "Hello, World!";
$boolean = true;
$array = array(1, 2, 3);
?>
```

### Type Casting dan Konversi
PHP secara otomatis mengonversi tipe data sesuai kebutuhan, tetapi Anda juga dapat melakukan type casting secara eksplisit.

```php
<?php
$number = "10";
$integer = (int)$number;
?>
```

## Array dan Fungsi

### Array Numerik dan Asosiatif
Array numerik menggunakan indeks angka, sedangkan array asosiatif menggunakan kunci string.

```php
<?php
$numerik = array(1, 2, 3);
$asosiatif = array("satu" => 1, "dua" => 2, "tiga" => 3);
?>
```

### Built-in Functions
PHP memiliki banyak fungsi bawaan untuk berbagai keperluan, seperti manipulasi string, operasi matematika, dan pengelolaan array.

```php
<?php
echo strlen("Hello, World!"); // Output: 13
?>
```

### User-defined Functions
Anda dapat mendefinisikan fungsi sendiri untuk mengorganisir kode dan menghindari pengulangan.

```php
<?php
function greet($name) {
    return "Hello, " . $name;
}
echo greet("World"); // Output: Hello, World
?>
```

## Object-Oriented Programming (OOP) dalam PHP

### Class dan Objek
OOP memungkinkan Anda untuk membuat class dan objek untuk mengorganisir kode dengan lebih baik.

```php
<?php
class Person {
    public $name;
    public function __construct($name) {
        $this->name = $name;
    }
    public function greet() {
        return "Hello, " . $this->name;
    }
}
$person = new Person("World");
echo $person->greet(); // Output: Hello, World
?>
```

### Properties dan Methods
Class dapat memiliki properties (variabel) dan methods (fungsi) yang mendefinisikan perilaku dan data dari objek.

### Inheritance dan Polymorphism
Inheritance memungkinkan class untuk mewarisi properties dan methods dari class lain. Polymorphism memungkinkan objek untuk mengambil banyak bentuk.

```php
<?php
class Animal {
    public function makeSound() {
        return "Some sound";
    }
}
class Dog extends Animal {
    public function makeSound() {
        return "Bark";
    }
}
$dog = new Dog();
echo $dog->makeSound(); // Output: Bark
?>
```

## Database dan PHP

### Koneksi ke Database
PHP dapat terhubung ke berbagai jenis database, seperti MySQL, menggunakan ekstensi seperti PDO atau MySQLi.

```php
<?php
$dsn = 'mysql:host=localhost;dbname=testdb';
$username = 'root';
$password = '';
$options = array(
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
);
$pdo = new PDO($dsn, $username, $password, $options);
?>
```

### CRUD Operations
CRUD (Create, Read, Update, Delete) adalah operasi dasar untuk mengelola data dalam database.

```php
<?php
// Create
$sql = "INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com')";
$pdo->exec($sql);

// Read
$sql = "SELECT * FROM users";
$stmt = $pdo->query($sql);
$users = $stmt->fetchAll(PDO::FETCH_ASSOC);

// Update
$sql = "UPDATE users SET email = 'john.doe@example.com' WHERE name = 'John Doe'";
$pdo->exec($sql);

// Delete
$sql = "DELETE FROM users WHERE name = 'John Doe'";
$pdo->exec($sql);
?>
```

### Prepared Statements
Prepared statements digunakan untuk mencegah SQL injection dan meningkatkan keamanan aplikasi.

```php
<?php
$sql = "SELECT * FROM users WHERE email = :email";
$stmt = $pdo->prepare($sql);
$stmt->execute(['email' => 'john@example.com']);
$user = $stmt->fetch(PDO::FETCH_ASSOC);
?>
```
