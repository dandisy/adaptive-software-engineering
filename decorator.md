Decorator adalah pola desain yang termasuk dalam kategori pola Struktural. Pola ini memungkinkan penambahan fungsi atau perilaku tambahan pada objek tanpa mengubah struktur atau antarmuka objek tersebut. Decorator mengikuti prinsip Open-Closed yang menyatakan bahwa sebuah kelas harus terbuka untuk ekstensi (penambahan perilaku baru) tetapi tertutup untuk modifikasi (tidak mengubah kode yang ada).

Pola Decorator menggunakan komposisi untuk membungkus objek asli dengan decorator tambahan. Setiap decorator memiliki hubungan has-a dengan objek asli dan menerapkan fungsi tambahan sebelum atau setelah memanggil metode objek asli. Decorator dapat bertumpuk dan saling berantur dengan cara yang fleksibel, sehingga memungkinkan penambahan fungsi tambahan secara dinamis.

Berikut adalah contoh praktis implementasi Decorator dengan PHP:

```php
<?php

// Komponen dasar (interface atau kelas abstrak)
interface Coffee {
    public function getCost();
    public function getDescription();
}

// Implementasi konkret dari komponen dasar
class SimpleCoffee implements Coffee {
    public function getCost() {
        return 1.0;
    }

    public function getDescription() {
        return "Kopi sederhana";
    }
}

// Decorator abstrak
abstract class CoffeeDecorator implements Coffee {
    protected $decoratedCoffee;

    public function __construct(Coffee $coffee) {
        $this->decoratedCoffee = $coffee;
    }

    public function getCost() {
        return $this->decoratedCoffee->getCost();
    }

    public function getDescription() {
        return $this->decoratedCoffee->getDescription();
    }
}

// Decorator konkret
class Milk extends CoffeeDecorator {
    public function getCost() {
        return $this->decoratedCoffee->getCost() + 0.5;
    }

    public function getDescription() {
        return $this->decoratedCoffee->getDescription() . ", Susu";
    }
}

// Decorator konkret
class Vanilla extends CoffeeDecorator {
    public function getCost() {
        return $this->decoratedCoffee->getCost() + 0.7;
    }

    public function getDescription() {
        return $this->decoratedCoffee->getDescription() . ", Vanilla";
    }
}

// Penggunaan Decorator
$coffee = new SimpleCoffee();
$coffee = new Milk($coffee);
$coffee = new Vanilla($coffee);

echo "Harga: $" . $coffee->getCost() . "\n";
echo "Deskripsi: " . $coffee->getDescription() . "\n";

?>
```

Dalam contoh di atas, terdapat komponen dasar `Coffee` yang didefinisikan melalui antarmuka. Implementasi konkret `SimpleCoffee` adalah objek dasar yang akan didekorasi. Kemudian, terdapat decorator abstrak `CoffeeDecorator` yang melaksanakan antarmuka `Coffee` dan memiliki referensi ke objek yang didekorasi.

Kelas decorator konkret, seperti `Milk` dan `Vanilla`, mewarisi dari `CoffeeDecorator` dan menambahkan perilaku tambahan sebelum atau setelah memanggil metode pada objek yang didekorasi. Dalam contoh ini, `Milk` menambahkan biaya dan deskripsi susu, sedangkan `Vanilla` menambahkan biaya dan deskripsi vanilla.

Pada saat pengguna