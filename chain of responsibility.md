Chain of Responsibility adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini memungkinkan serangkaian objek yang berpotensi menghandle suatu permintaan untuk berkolaborasi secara berurutan. Permintaan akan dikirim melalui serangkaian objek hingga satu objek yang sesuai dengan kriteria tertentu menanganinya.

Pola Chain of Responsibility menghindari ketergantungan yang kuat antara pengirim permintaan (client) dan penerima permintaan (handler). Setiap handler dalam rantai memiliki kemampuan untuk menangani permintaan atau meneruskannya ke handler berikutnya dalam rantai. Dengan cara ini, handler dalam rantai dapat bergantian menangani permintaan dan menghindari ketergantungan langsung antara pengirim dan penerima.

Berikut adalah contoh praktis implementasi Chain of Responsibility dengan PHP:

```php
<?php

// Handler abstrak
abstract class Handler {
    protected $nextHandler;

    public function setNext(Handler $handler) {
        $this->nextHandler = $handler;
    }

    public function handleRequest($request) {
        if ($this->canHandle($request)) {
            $this->processRequest($request);
        } elseif ($this->nextHandler != null) {
            $this->nextHandler->handleRequest($request);
        } else {
            echo "Tidak ada handler yang cocok untuk permintaan ini.\n";
        }
    }

    abstract protected function canHandle($request);
    abstract protected function processRequest($request);
}

// Handler konkret
class ConcreteHandlerA extends Handler {
    protected function canHandle($request) {
        return $request >= 0 && $request < 10;
    }

    protected function processRequest($request) {
        echo "ConcreteHandlerA menangani permintaan dengan nilai: " . $request . "\n";
    }
}

// Handler konkret
class ConcreteHandlerB extends Handler {
    protected function canHandle($request) {
        return $request >= 10 && $request < 20;
    }

    protected function processRequest($request) {
        echo "ConcreteHandlerB menangani permintaan dengan nilai: " . $request . "\n";
    }
}

// Handler konkret
class ConcreteHandlerC extends Handler {
    protected function canHandle($request) {
        return $request >= 20 && $request < 30;
    }

    protected function processRequest($request) {
        echo "ConcreteHandlerC menangani permintaan dengan nilai: " . $request . "\n";
    }
}

// Penggunaan Chain of Responsibility
$handlerA = new ConcreteHandlerA();
$handlerB = new ConcreteHandlerB();
$handlerC = new ConcreteHandlerC();

$handlerA->setNext($handlerB);
$handlerB->setNext($handlerC);

$requests = [5, 15, 25, 35];

foreach ($requests as $request) {
    $handlerA->handleRequest($request);
}

?>
```

Dalam contoh di atas, terdapat hierarki handler yang terdiri dari `ConcreteHandlerA`, `ConcreteHandlerB`, dan `ConcreteHandlerC`. Setiap handler memiliki metode `canHandle()` untuk menentukan apakah dia dapat menangani permintaan atau harus meneruskannya ke handler berikutnya. Metode `processRequest()` digunakan untuk menangani permintaan yang sesuai.

Pada saat penggunaannya, pengirim permintaan (client) memulai permintaan dengan