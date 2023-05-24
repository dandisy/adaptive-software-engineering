Observer adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini memungkinkan objek-objek yang tergantung pada suatu subjek untuk secara otomatis mendapatkan pembaruan ketika subjek tersebut mengalami perubahan. Observer membangun hubungan one-to-many antara subjek (subject) dan objek-objek yang mengamatinya (observers).

Pola Observer terdiri dari dua komponen utama: Subject dan Observer. Subject adalah objek yang diamati dan dapat memiliki banyak objek Observer yang tergantung padanya. Observer adalah objek yang mengamati subjek dan akan menerima pembaruan ketika subjek mengalami perubahan.

Ketika subjek mengalami perubahan, subjek akan memberi tahu semua observer yang terdaftar dan observer tersebut dapat mengambil tindakan yang sesuai berdasarkan pembaruan yang diterima.

Berikut adalah contoh praktis implementasi Observer dengan PHP:

```php
<?php

// Subject (Subjek)
interface Subject {
    public function registerObserver(Observer $observer);
    public function removeObserver(Observer $observer);
    public function notifyObservers();
}

// Concrete Subject (Subjek Konkret)
class WeatherStation implements Subject {
    private $temperature;
    private $observers;

    public function __construct() {
        $this->observers = [];
    }

    public function registerObserver(Observer $observer) {
        $this->observers[] = $observer;
    }

    public function removeObserver(Observer $observer) {
        $index = array_search($observer, $this->observers);
        if ($index !== false) {
            unset($this->observers[$index]);
        }
    }

    public function notifyObservers() {
        foreach ($this->observers as $observer) {
            $observer->update($this->temperature);
        }
    }

    public function setTemperature($temperature) {
        $this->temperature = $temperature;
        $this->notifyObservers();
    }
}

// Observer
interface Observer {
    public function update($temperature);
}

// Concrete Observer
class User implements Observer {
    public function update($temperature) {
        echo "Notifikasi: Temperatur saat ini adalah $temperature derajat Celsius.\n";
    }
}

// Concrete Observer
class Logger implements Observer {
    public function update($temperature) {
        echo "Log: Temperatur saat ini di-log: $temperature derajat Celsius.\n";
    }
}

// Penggunaan Observer
$weatherStation = new WeatherStation();

$userObserver = new User();
$loggerObserver = new Logger();

$weatherStation->registerObserver($userObserver);
$weatherStation->registerObserver($loggerObserver);

$weatherStation->setTemperature(25); // Notifikasi dan log akan diterima oleh observer

$weatherStation->removeObserver($loggerObserver);

$weatherStation->setTemperature(30); // Hanya notifikasi yang akan diterima oleh observer

?>
```

Dalam contoh di atas, terdapat antarmuka `Subject` yang mendefinisikan metode-metode untuk mendaftar observer, menghapus observer, dan memberi tahu observer-observer. `WeatherStation` adalah implementasi konkret dari `Subject`, yang menyimpan temperatur saat ini dan mampu memberitahu semua observer ketika terjadi perubahan temperatur.

Selanjutnya, terdapat antarmuka `Observer` yang mendefinisikan metode `update()` yang akan diimplementasikan oleh observer konkret. `User` dan `Logger` adalah