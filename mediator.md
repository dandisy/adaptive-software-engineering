Mediator adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini memungkinkan komunikasi terstruktur antara objek-objek yang berinteraksi, tanpa harus terjadi ketergantungan langsung antara objek-objek tersebut. Mediator memisahkan logika komunikasi menjadi komponen terpisah yang dikenal sebagai mediator, sehingga memudahkan komunikasi dan koordinasi antara objek-objek yang terlibat.

Pola Mediator berfungsi sebagai perantara antara objek-objek yang berinteraksi. Semua komunikasi antara objek-objek dilakukan melalui mediator, yang mengendalikan aliran informasi dan tindakan di antara objek-objek tersebut. Mediator memungkinkan objek-objek tersebut bekerja sama tanpa perlu mengetahui secara langsung tentang keberadaan dan detail implementasi satu sama lain.

Berikut adalah contoh praktis implementasi Mediator dengan PHP:

```php
<?php

// Mediator
interface Mediator {
    public function sendMessage($message, Colleague $colleague);
}

// Colleague
abstract class Colleague {
    protected $mediator;

    public function setMediator(Mediator $mediator) {
        $this->mediator = $mediator;
    }

    public function send($message) {
        $this->mediator->sendMessage($message, $this);
    }

    abstract public function receive($message);
}

// Concrete Colleague
class ConcreteColleagueA extends Colleague {
    public function receive($message) {
        echo "ConcreteColleagueA menerima pesan: " . $message . "\n";
    }
}

// Concrete Colleague
class ConcreteColleagueB extends Colleague {
    public function receive($message) {
        echo "ConcreteColleagueB menerima pesan: " . $message . "\n";
    }
}

// Concrete Mediator
class ConcreteMediator implements Mediator {
    private $colleagueA;
    private $colleagueB;

    public function setColleagueA(ConcreteColleagueA $colleague) {
        $this->colleagueA = $colleague;
    }

    public function setColleagueB(ConcreteColleagueB $colleague) {
        $this->colleagueB = $colleague;
    }

    public function sendMessage($message, Colleague $colleague) {
        if ($colleague === $this->colleagueA) {
            $this->colleagueB->receive($message);
        } elseif ($colleague === $this->colleagueB) {
            $this->colleagueA->receive($message);
        }
    }
}

// Penggunaan Mediator
$mediator = new ConcreteMediator();

$colleagueA = new ConcreteColleagueA();
$colleagueB = new ConcreteColleagueB();

$mediator->setColleagueA($colleagueA);
$mediator->setColleagueB($colleagueB);

$colleagueA->send("Halo dari ConcreteColleagueA"); // ConcreteColleagueB menerima pesan
$colleagueB->send("Halo juga dari ConcreteColleagueB"); // ConcreteColleagueA menerima pesan

?>
```

Dalam contoh di atas, terdapat antarmuka `Mediator` yang mendefinisikan metode `sendMessage()` yang akan diimplementasikan oleh mediator konkret. `Mediator` bertanggung jawab untuk mengatur komunikasi antara objek-objek yang berpart