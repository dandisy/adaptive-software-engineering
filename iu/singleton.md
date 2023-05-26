Singleton adalah pola desain yang digunakan untuk memastikan bahwa sebuah kelas memiliki hanya satu instansi tunggal (instance) yang dapat diakses secara global. Pola Singleton membatasi pembuatan objek dari kelas tersebut hanya menjadi satu, sehingga memastikan bahwa hanya ada satu instansi yang digunakan oleh seluruh aplikasi.

Pola Singleton biasanya digunakan ketika kita ingin membatasi akses ke objek tunggal yang bertanggung jawab atas sumber daya terpusat, seperti pengaturan aplikasi, koneksi database, atau log sistem. Dengan menggunakan Singleton, kita dapat memastikan bahwa hanya ada satu titik akses ke objek tersebut dan mencegah pembuatan lebih dari satu instansi yang tidak perlu.

Berikut adalah contoh praktis implementasi pola Singleton dengan PHP:

```php
<?php

class Singleton {
    private static $instance;
    private $data;

    private function __construct() {
        $this->data = "Hello, Singleton!";
    }

    public static function getInstance() {
        if (self::$instance === null) {
            self::$instance = new Singleton();
        }
        return self::$instance;
    }

    public function getData() {
        return $this->data;
    }
}

// Penggunaan Singleton
$singleton1 = Singleton::getInstance();
echo $singleton1->getData() . "\n";

$singleton2 = Singleton::getInstance();
echo $singleton2->getData() . "\n";

?>
```

Dalam contoh di atas, kita memiliki kelas `Singleton` yang mengimplementasikan pola Singleton. Kelas ini memiliki properti `$instance` yang menyimpan instansi Singleton dan properti `$data` yang berisi data yang akan diakses.

Konstruktor kelas `Singleton` dideklarasikan sebagai private, sehingga tidak dapat diakses dari luar kelas. Metode `getInstance()` adalah metode statis yang bertanggung jawab untuk memastikan bahwa hanya ada satu instansi Singleton yang dibuat. Jika belum ada instansi yang dibuat sebelumnya, metode ini akan membuat instansi baru menggunakan `new Singleton()` dan menyimpannya dalam properti `$instance`. Selanjutnya, metode ini akan mengembalikan instansi Singleton yang ada atau yang baru dibuat.

Dalam penggunaan pola Singleton, kita memanggil metode `getInstance()` untuk mendapatkan instansi Singleton. Setiap kali kita memanggil metode ini, kita akan mendapatkan instansi yang sama. Karena hanya ada satu instansi yang dibuat, maka pemanggilan metode `getInstance()` berulang kali akan menghasilkan objek yang sama.

Hasil output dari contoh di atas akan mencetak:

```
Hello, Singleton!
Hello, Singleton!
```

Output tersebut menunjukkan bahwa meskipun kita memanggil `getInstance()` dua kali, kita mendapatkan instansi Singleton yang sama, dan data yang diakses juga sama. Dengan demikian, pola Singleton memastikan bahwa hanya ada satu instansi yang ada dan dapat diakses oleh seluruh aplikasi.