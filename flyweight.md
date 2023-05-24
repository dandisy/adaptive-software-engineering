Flyweight adalah pola desain yang termasuk dalam kategori pola Struktural. Pola ini digunakan untuk mengurangi penggunaan memori dengan berbagi sebanyak mungkin data yang sama di antara objek-objek yang berbeda.

Pola Flyweight berfokus pada efisiensi penyimpanan data dengan memisahkan data intrinsik (bersifat umum dan dapat dibagikan) dan ekstrinsik (bersifat spesifik untuk setiap objek). Data intrinsik disimpan secara terpusat dan dibagikan di antara objek-objek yang membutuhkannya, sedangkan data ekstrinsik disimpan secara terpisah untuk setiap objek.

Berikut adalah contoh praktis implementasi Flyweight dengan PHP:

```php
<?php

// Abstraksi kelas Flyweight
abstract class Flyweight {
    abstract public function render($extrinsicState);
}

// Implementasi konkret Flyweight
class ConcreteFlyweight extends Flyweight {
    private $intrinsicState;

    public function __construct($intrinsicState) {
        $this->intrinsicState = $intrinsicState;
    }

    public function render($extrinsicState) {
        echo "Intrinsic State: " . $this->intrinsicState . ", Extrinsic State: " . $extrinsicState . "\n";
    }
}

// Flyweight Factory
class FlyweightFactory {
    private $flyweights = [];

    public function getFlyweight($key) {
        if (!isset($this->flyweights[$key])) {
            $this->flyweights[$key] = new ConcreteFlyweight($key);
        }
        return $this->flyweights[$key];
    }
}

// Penggunaan Flyweight
$factory = new FlyweightFactory();

// Objek pertama dengan flyweight A
$flyweightA = $factory->getFlyweight('A');
$flyweightA->render('State 1');

// Objek kedua dengan flyweight A
$flyweightA = $factory->getFlyweight('A');
$flyweightA->render('State 2');

// Objek ketiga dengan flyweight B
$flyweightB = $factory->getFlyweight('B');
$flyweightB->render('State 3');

?>
```

Dalam contoh di atas, terdapat abstraksi kelas `Flyweight` yang merupakan kerangka dasar untuk flyweight. Kemudian, terdapat implementasi konkret `ConcreteFlyweight` yang menyimpan data intrinsik (intrinsic state) dan mengimplementasikan metode `render()` untuk menampilkan data ekstrinsik (extrinsic state) bersamaan dengan data intrinsik.

Flyweight Factory (`FlyweightFactory`) bertindak sebagai pabrik untuk menciptakan dan mengelola objek flyweight. Jika flyweight dengan kunci (key) tertentu belum ada, factory akan membuatnya dan menyimpannya dalam koleksi flyweights yang sudah ada. Jika flyweight dengan kunci yang sama sudah ada, factory akan mengembalikan flyweight yang sudah ada tersebut.

Dalam contoh tersebut, kita menggunakan flyweight untuk membuat beberapa objek dengan menggunakan flyweight yang sama. Objek-objek ini menggunakan flyweight untuk menyimpan data intrinsik (dalam hal ini, kunci flyweight), sedangkan data ekstrinsik (state) disediakan saat rendering.

Pola Flyweight membantu mengurangi penggunaan memori dengan membagikan data yang sama di antara objek-objek yang membutuh