Facade adalah pola desain yang termasuk dalam kategori pola Struktural. Pola ini digunakan untuk menyediakan antarmuka yang sederhana dan terpusat untuk mengakses atau berinteraksi dengan sistem yang kompleks. Facade menyediakan antarmuka yang lebih tinggi tingkat untuk menyembunyikan kompleksitas sistem yang ada di baliknya.

Facade memungkinkan klien untuk berinteraksi dengan sistem secara lebih mudah dengan menyediakan metode yang terkait dan relevan untuk tugas yang umum dilakukan oleh klien. Facade mengelola dan mengoordinasikan pemanggilan ke bagian-bagian sistem yang berbeda, sehingga klien tidak perlu mengetahui atau berinteraksi langsung dengan setiap komponen sistem secara terpisah.

Berikut adalah contoh praktis implementasi Facade dengan PHP:

```php
<?php

// Subsistem 1
class Subsystem1 {
    public function operation1() {
        echo "Subsystem 1: Operasi 1.\n";
    }

    public function operation2() {
        echo "Subsystem 1: Operasi 2.\n";
    }
}

// Subsistem 2
class Subsystem2 {
    public function operation1() {
        echo "Subsystem 2: Operasi 1.\n";
    }

    public function operation2() {
        echo "Subsystem 2: Operasi 2.\n";
    }
}

// Facade
class Facade {
    private $subsystem1;
    private $subsystem2;

    public function __construct() {
        $this->subsystem1 = new Subsystem1();
        $this->subsystem2 = new Subsystem2();
    }

    public function operation() {
        echo "Fasade memulai operasi:\n";
        $this->subsystem1->operation1();
        $this->subsystem1->operation2();
        $this->subsystem2->operation1();
        $this->subsystem2->operation2();
    }
}

// Penggunaan Facade
$facade = new Facade();
$facade->operation();

?>
```

Dalam contoh di atas, terdapat dua subsistem, yaitu `Subsystem1` dan `Subsystem2`, yang masing-masing memiliki beberapa operasi. Kemudian, terdapat `Facade` yang bertindak sebagai facade untuk mengelola dan menyembunyikan kompleksitas dari kedua subsistem tersebut.

Ketika klien memanggil metode `operation()` pada facade, facade akan mengoordinasikan pemanggilan ke operasi yang relevan pada kedua subsistem. Dalam contoh ini, facade memulai operasi dengan menampilkan pesan, kemudian memanggil operasi-operasi pada `Subsystem1` dan `Subsystem2`.

Dengan menggunakan facade, klien tidak perlu mengetahui atau berinteraksi langsung dengan setiap subsistem atau operasi di dalamnya. Facade menyediakan antarmuka yang sederhana dan terpusat untuk klien, yang mengelola kompleksitas sistem di belakang layar.