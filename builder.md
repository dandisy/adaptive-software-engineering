Builder adalah pola desain yang termasuk dalam kategori pola Creational. Pola ini digunakan untuk memisahkan proses pembuatan objek kompleks dari representasi objeknya, sehingga objek-objek yang sama dapat dibangun dengan cara yang berbeda. Builder memungkinkan kita untuk mengkonstruksi objek kompleks langkah demi langkah tanpa harus mengekspos semua detail implementasinya kepada klien.

Pola Builder terdiri dari beberapa komponen utama: Director, Builder, dan Product. Director bertanggung jawab untuk mengatur proses pembangunan objek kompleks dengan menggunakan Builder. Builder adalah antarmuka yang didefinisikan untuk membuat langkah-langkah konstruksi objek. Product adalah objek yang kompleks yang akan dibangun oleh Builder.

Dengan menggunakan pola Builder, kita dapat memisahkan logika konstruksi objek kompleks dari klien yang menggunakan objek tersebut. Hal ini memungkinkan fleksibilitas dalam konstruksi objek dan menghasilkan objek yang berbeda tanpa perlu mengubah kode klien.

Berikut adalah contoh praktis implementasi Builder dengan PHP:

```php
<?php

// Product
class House {
    private $foundation;
    private $structure;
    private $roof;

    public function setFoundation($foundation) {
        $this->foundation = $foundation;
    }

    public function setStructure($structure) {
        $this->structure = $structure;
    }

    public function setRoof($roof) {
        $this->roof = $roof;
    }

    public function showDetails() {
        echo "House Details:\n";
        echo "Foundation: " . $this->foundation . "\n";
        echo "Structure: " . $this->structure . "\n";
        echo "Roof: " . $this->roof . "\n";
    }
}

// Builder
interface HouseBuilder {
    public function buildFoundation();
    public function buildStructure();
    public function buildRoof();
    public function getHouse();
}

// Concrete Builder
class SimpleHouseBuilder implements HouseBuilder {
    private $house;

    public function __construct() {
        $this->house = new House();
    }

    public function buildFoundation() {
        $this->house->setFoundation("Simple Foundation");
    }

    public function buildStructure() {
        $this->house->setStructure("Simple Structure");
    }

    public function buildRoof() {
        $this->house->setRoof("Simple Roof");
    }

    public function getHouse() {
        return $this->house;
    }
}

// Director
class HouseDirector {
    private $builder;

    public function setBuilder(HouseBuilder $builder) {
        $this->builder = $builder;
    }

    public function buildHouse() {
        $this->builder->buildFoundation();
        $this->builder->buildStructure();
        $this->builder->buildRoof();
    }

    public function getHouse() {
        return $this->builder->getHouse();
    }
}

// Penggunaan Builder
$builder = new SimpleHouseBuilder();
$director = new HouseDirector();

$director->setBuilder($builder);
$director->buildHouse();

$house = $director->getHouse();
$house->showDetails();

?>
```

Dalam contoh di atas, terdapat kelas `House` yang merupakan objek kompleks yang akan dibangun menggunakan Builder. Kelas ini memiliki beberapa atribut seperti foundation, structure, dan roof, serta metode-metode untuk mengatur dan