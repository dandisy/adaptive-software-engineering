Pola Interpreter adalah pola desain yang digunakan untuk menginterpretasikan atau mengevaluasi ekspresi atau pernyataan yang ditulis dalam bahasa yang lebih tinggi atau kompleks. Pola ini menguraikan ekspresi ke dalam representasi yang lebih sederhana, memungkinkan eksekusi langkah-demi-langkah berdasarkan struktur ekspresi tersebut.

Pola Interpreter terdiri dari beberapa komponen utama: Ekspresi (Expression), Konteks (Context), dan Interpreter. Ekspresi adalah representasi dari ekspresi yang akan diinterpretasikan. Konteks menyimpan informasi yang diperlukan selama proses interpretasi. Interpreter menginterpretasikan ekspresi dan menghasilkan hasil yang sesuai berdasarkan konteks.

Dalam implementasi pola Interpreter, ekspresi kompleks biasanya diurai menjadi pohon ekspresi yang terdiri dari simpul-simpul yang mewakili operasi, operan, atau ekspresi lainnya. Setiap simpul dalam pohon ekspresi dapat menjadi objek kelas yang berbeda yang mengimplementasikan metode interpretasi sesuai dengan peran mereka dalam ekspresi.

Berikut adalah contoh praktis implementasi pola Interpreter dengan PHP:

```php
<?php

// Konteks
class Context {
    private $input;
    private $output;

    public function setInput($input) {
        $this->input = $input;
    }

    public function getInput() {
        return $this->input;
    }

    public function setOutput($output) {
        $this->output = $output;
    }

    public function getOutput() {
        return $this->output;
    }
}

// Ekspresi - Abstrak
interface Expression {
    public function interpret(Context $context);
}

// Ekspresi - Terminal
class NumberExpression implements Expression {
    private $number;

    public function __construct($number) {
        $this->number = $number;
    }

    public function interpret(Context $context) {
        return $this->number;
    }
}

// Ekspresi - Non-Terminal
class AddExpression implements Expression {
    private $leftExpression;
    private $rightExpression;

    public function __construct(Expression $leftExpression, Expression $rightExpression) {
        $this->leftExpression = $leftExpression;
        $this->rightExpression = $rightExpression;
    }

    public function interpret(Context $context) {
        $result = $this->leftExpression->interpret($context) + $this->rightExpression->interpret($context);
        return $result;
    }
}

// Penggunaan Interpreter
$context = new Context();

$number1 = new NumberExpression(5);
$number2 = new NumberExpression(3);

$addExpression = new AddExpression($number1, $number2);

$context->setInput("5 + 3");
$context->setOutput($addExpression->interpret($context));

echo $context->getInput() . " = " . $context->getOutput();

?>
```

Dalam contoh di atas, kita memiliki kelas `Context` yang menyimpan informasi konteks yang diperlukan selama proses interpretasi. Kemudian, kita memiliki antarmuka `Expression` yang diterapkan oleh kelas-kelas ekspresi konkret, yaitu `NumberExpression` dan `AddExpression`.

Kelas `NumberExpression` mewakili ekspresi angka tunggal, sedangkan `AddExpression` mewakili ekspresi penjumlahan antara dua ekspresi lainnya. Setiap kelas ekspresi mengimplementasikan metode `interpret()` yang menginterpretasikan ekspresi sesuai dengan peran mereka.

Selanjutnya, kita membuat objek `Context` yang akan digunakan untuk menyimpan konteks dan hasil interpretasi. Kemudian, kita membuat objek-objek ekspresi yang sesuai, yaitu `NumberExpression` dengan angka 5 dan 3, serta `AddExpression` yang menerima dua ekspresi sebagai argumen.

Kemudian, kita mengatur input konteks dengan ekspresi yang akan diinterpretasikan, dalam contoh ini adalah "5 + 3". Selanjutnya, kita memanggil metode `interpret()` pada ekspresi penjumlahan (`AddExpression`) dengan menggunakan objek konteks sebagai argumen. Hasil interpretasi akan disimpan dalam output konteks.

Hasil output dari contoh di atas akan mencetak:

```
5 + 3 = 8
```

Output tersebut menunjukkan bahwa ekspresi "5 + 3" diinterpretasikan dengan benar menggunakan pola Interpreter. Hasil interpretasi, yaitu 8, disimpan dalam output konteks dan ditampilkan sebagai hasil akhir.

Pola Interpreter sangat berguna dalam kasus-kasus di mana kita perlu menginterpretasikan atau mengevaluasi ekspresi yang ditulis dalam bahasa yang lebih tinggi atau kompleks. Dengan memisahkan interpretasi ke dalam hierarki ekspresi yang terstruktur, kita dapat dengan mudah menambahkan atau mengubah perilaku interpretasi tanpa mengubah struktur ekspresi atau logika di luar interpretasi.