Bridge adalah pola desain yang termasuk dalam kategori pola Struktural. Pola ini digunakan untuk memisahkan antara abstraksi (interface) dan implementasi dari suatu komponen, sehingga keduanya dapat berubah secara independen tanpa harus mempengaruhi satu sama lain.

Pola Bridge menggunakan konsep "penghubung" (bridge) yang berfungsi sebagai jembatan antara abstraksi dan implementasi. Dengan menggunakan bridge, abstraksi dan implementasi dapat berevolusi secara terpisah tanpa mempengaruhi kode yang terkait.

Berikut adalah contoh praktis implementasi Bridge dengan PHP:

```php
<?php

// Abstraksi (interface) yang terpisah dari implementasi
interface Renderer {
    public function renderShape($shape);
}

// Implementasi konkret untuk menggambar bentuk sebagai vektor
class VectorRenderer implements Renderer {
    public function renderShape($shape) {
        echo "Menggambar bentuk " . $shape . " sebagai vektor.\n";
    }
}

// Implementasi konkret untuk menggambar bentuk sebagai raster
class RasterRenderer implements Renderer {
    public function renderShape($shape) {
        echo "Menggambar bentuk " . $shape . " sebagai raster.\n";
    }
}

// Abstraksi yang terpisah dari implementasi
abstract class Shape {
    protected $renderer;

    public function __construct(Renderer $renderer) {
        $this->renderer = $renderer;
    }

    abstract public function draw();
}

// Implementasi konkret dari bentuk lingkaran
class Circle extends Shape {
    private $x, $y, $radius;

    public function __construct($x, $y, $radius, Renderer $renderer) {
        parent::__construct($renderer);
        $this->x = $x;
        $this->y = $y;
        $this->radius = $radius;
    }

    public function draw() {
        $this->renderer->renderShape("lingkaran");
    }
}

// Implementasi konkret dari bentuk persegi
class Square extends Shape {
    private $x, $y, $side;

    public function __construct($x, $y, $side, Renderer $renderer) {
        parent::__construct($renderer);
        $this->x = $x;
        $this->y = $y;
        $this->side = $side;
    }

    public function draw() {
        $this->renderer->renderShape("persegi");
    }
}

// Penggunaan Bridge
$vectorRenderer = new VectorRenderer();
$rasterRenderer = new RasterRenderer();

$circle = new Circle(5, 10, 8, $vectorRenderer);
$circle->draw(); // Output: Menggambar bentuk lingkaran sebagai vektor.

$square = new Square(3, 6, 12, $rasterRenderer);
$square->draw(); // Output: Menggambar bentuk persegi sebagai raster.

?>
```

Dalam contoh di atas, terdapat abstraksi yang terpisah dari implementasi. Interface `Renderer` mendefinisikan metode `renderShape()` yang akan digunakan oleh implementasi konkret. Implementasi konkret `VectorRenderer` dan `RasterRenderer` menerapkan metode tersebut sesuai dengan kebutuhan masing-masing.

Selanjutnya, terdapat abstraksi `Shape` yang memiliki referensi ke objek `Renderer`. Kelas `Circle` dan `Square` adalah implementasi konkret dari `Shape` yang menerima objek `Renderer` melal