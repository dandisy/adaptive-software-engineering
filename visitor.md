Visitor adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini memungkinkan penambahan operasi baru pada objek-objek yang ada tanpa mengubah struktur atau kelas objek tersebut. Visitor memisahkan algoritma operasi dari objek-objek yang diterapkannya, sehingga memudahkan penambahan operasi baru tanpa mengganggu kelas-kelas yang ada.

Pola Visitor melibatkan dua komponen utama: Visitor dan Element. Visitor mendefinisikan metode-metode yang sesuai dengan setiap kelas Element yang ingin dikunjungi. Element merupakan objek-objek yang akan dikunjungi dan memiliki metode untuk menerima Visitor.

Berikut adalah contoh praktis implementasi Visitor dengan PHP:

```php
<?php

// Visitor
interface Visitor {
    public function visitElementA(ElementA $elementA);
    public function visitElementB(ElementB $elementB);
}

// Element
interface Element {
    public function accept(Visitor $visitor);
}

// Concrete Element
class ElementA implements Element {
    public function accept(Visitor $visitor) {
        $visitor->visitElementA($this);
    }

    public function operationA() {
        echo "Operasi A dilakukan pada ElementA.\n";
    }
}

// Concrete Element
class ElementB implements Element {
    public function accept(Visitor $visitor) {
        $visitor->visitElementB($this);
    }

    public function operationB() {
        echo "Operasi B dilakukan pada ElementB.\n";
    }
}

// Concrete Visitor
class ConcreteVisitor implements Visitor {
    public function visitElementA(ElementA $elementA) {
        echo "ConcreteVisitor mengunjungi ElementA.\n";
        $elementA->operationA();
    }

    public function visitElementB(ElementB $elementB) {
        echo "ConcreteVisitor mengunjungi ElementB.\n";
        $elementB->operationB();
    }
}

// Penggunaan Visitor
$visitor = new ConcreteVisitor();

$elementA = new ElementA();
$elementA->accept($visitor);

$elementB = new ElementB();
$elementB->accept($visitor);

?>
```

Dalam contoh di atas, terdapat antarmuka `Visitor` yang mendefinisikan metode-metode `visitElementA()` dan `visitElementB()` yang sesuai dengan kelas-kelas `Element` yang ingin dikunjungi. Antarmuka `Element` memiliki metode `accept()` yang menerima objek `Visitor`.

Kemudian, terdapat kelas `ElementA` dan `ElementB` yang merupakan implementasi konkret dari `Element` dan memiliki metode `operationA()` dan `operationB()` yang dapat dieksekusi oleh Visitor.

Selanjutnya, terdapat kelas `ConcreteVisitor` yang merupakan implementasi konkret dari `Visitor`. Dalam kelas ini, metode-metode `visitElementA()` dan `visitElementB()` didefinisikan untuk mengunjungi dan melakukan operasi pada objek `ElementA` dan `ElementB` secara berturut-turut.

Pada saat penggunaannya, Visitor (`ConcreteVisitor`) dapat mengunjungi objek `ElementA` dan `ElementB` dengan memanggil metode `accept()` pada objek tersebut dan memberikan dirinya sendiri sebagai parameter. Saat objek `Element` menerima Visitor, metode `visitElementA()` atau `visitElementB()` yang sesuai akan dipanggil, dan operasi yang sesuai dengan setiap objek akan