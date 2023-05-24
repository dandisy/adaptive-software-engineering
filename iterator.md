Iterator adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini digunakan untuk mengakses elemen-elemen dari suatu koleksi objek secara terurut tanpa mengungkapkan detail implementasi dari koleksi tersebut. Iterator memungkinkan kita untuk melintasi elemen-elemen koleksi dengan cara yang seragam tanpa harus bergantung pada struktur internal koleksi.

Pola Iterator terdiri dari dua komponen utama: Iterator dan Aggregate. Iterator adalah objek yang bertanggung jawab untuk melintasi dan mengakses elemen-elemen koleksi secara terurut. Aggregate adalah objek yang menyediakan metode untuk membuat Iterator.

Dengan menggunakan pola Iterator, kita dapat mengakses dan mengambil elemen-elemen koleksi dengan cara yang seragam, terlepas dari tipe dan struktur internal koleksi tersebut.

Berikut adalah contoh praktis implementasi Iterator dengan PHP:

```php
<?php

// Iterator
interface Iterator {
    public function hasNext();
    public function next();
}

// Aggregate
interface Aggregate {
    public function createIterator();
}

// Concrete Iterator
class ConcreteIterator implements Iterator {
    private $collection;
    private $position = 0;

    public function __construct($collection) {
        $this->collection = $collection;
    }

    public function hasNext() {
        return $this->position < count($this->collection);
    }

    public function next() {
        $item = $this->collection[$this->position];
        $this->position++;
        return $item;
    }
}

// Concrete Aggregate
class ConcreteAggregate implements Aggregate {
    private $collection;

    public function __construct() {
        $this->collection = [];
    }

    public function addItem($item) {
        $this->collection[] = $item;
    }

    public function createIterator() {
        return new ConcreteIterator($this->collection);
    }
}

// Penggunaan Iterator
$aggregate = new ConcreteAggregate();
$aggregate->addItem("Item 1");
$aggregate->addItem("Item 2");
$aggregate->addItem("Item 3");

$iterator = $aggregate->createIterator();

while ($iterator->hasNext()) {
    echo $iterator->next() . "\n";
}

?>
```

Dalam contoh di atas, terdapat antarmuka `Iterator` yang mendefinisikan metode `hasNext()` untuk memeriksa apakah masih ada elemen yang tersedia, dan metode `next()` untuk mendapatkan elemen selanjutnya dari koleksi.

Selanjutnya, terdapat antarmuka `Aggregate` yang mendefinisikan metode `createIterator()` untuk membuat objek Iterator.

Kemudian, terdapat kelas `ConcreteIterator` yang merupakan implementasi konkret dari `Iterator`. Kelas ini melintasi elemen-elemen koleksi dengan memanfaatkan array dan menggunakan variabel `$position` untuk melacak posisi saat ini dalam koleksi.

Selain itu, terdapat kelas `ConcreteAggregate` yang merupakan implementasi konkret dari `Aggregate`. Kelas ini menyimpan elemen-elemen koleksi dalam array dan memiliki metode `addItem()` untuk menambahkan item ke koleksi.

Pada saat penggunaannya, kita membuat objek `ConcreteAggregate` dan menambahkan beberapa item ke koleksinya. Kemudian, kita membuat objek Iterator dengan memanggil `createIterator()` pada objek `ConcreteAggregate`. Selanjutnya, kita menggunakan Iterator untuk melintasi dan mencetak elemen-elemen koleksi menggunakan perulangan `while`