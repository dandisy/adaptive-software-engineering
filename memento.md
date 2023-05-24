Memento adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini digunakan untuk menyimpan dan mengembalikan status internal suatu objek tanpa mengungkapkan rincian implementasinya kepada objek lain. Memento memungkinkan objek untuk mengambil "snapshot" dari keadaannya pada suatu titik waktu tertentu dan kemudian mengembalikan objek ke keadaan tersebut jika diperlukan.

Pola Memento melibatkan tiga komponen utama: Originator, Memento, dan Caretaker. Originator adalah objek yang memiliki status internal yang ingin disimpan dan dikembalikan. Memento adalah objek yang berfungsi sebagai wadah untuk menyimpan status internal Originator. Caretaker adalah objek yang bertanggung jawab untuk mengelola Memento dan berinteraksi dengan Originator.

Dengan menggunakan pola Memento, kita dapat menyimpan keadaan objek pada suatu titik waktu, sehingga objek tersebut dapat dikembalikan ke keadaan tersebut jika diperlukan. Hal ini berguna dalam situasi seperti pembatalan operasi atau pemulihan status objek setelah kegagalan.

Berikut adalah contoh praktis implementasi Memento dengan PHP:

```php
<?php

// Memento
class Memento {
    private $state;

    public function __construct($state) {
        $this->state = $state;
    }

    public function getState() {
        return $this->state;
    }
}

// Originator
class Originator {
    private $state;

    public function setState($state) {
        $this->state = $state;
    }

    public function getState() {
        return $this->state;
    }

    public function saveStateToMemento() {
        return new Memento($this->state);
    }

    public function restoreStateFromMemento(Memento $memento) {
        $this->state = $memento->getState();
    }
}

// Caretaker
class Caretaker {
    private $mementos = [];

    public function addMemento(Memento $memento) {
        $this->mementos[] = $memento;
    }

    public function getMemento($index) {
        return $this->mementos[$index];
    }
}

// Penggunaan Memento
$originator = new Originator();
$caretaker = new Caretaker();

$originator->setState("State 1");
$originator->setState("State 2");

$caretaker->addMemento($originator->saveStateToMemento()); // Simpan snapshot saat ini

$originator->setState("State 3");

$caretaker->addMemento($originator->saveStateToMemento()); // Simpan snapshot saat ini

$originator->setState("State 4");

$memento1 = $caretaker->getMemento(0); // Mendapatkan snapshot pertama
$originator->restoreStateFromMemento($memento1); // Mengembalikan objek ke keadaan snapshot pertama
echo $originator->getState() . "\n"; // Output: State 2

$memento2 = $caretaker->getMemento(1); // Mendapatkan snapshot kedua
$originator->restoreStateFromMemento($memento2); // Mengembalikan objek ke keadaan snapshot kedua
echo $originator->getState() . "\n"; // Output: State 3

?>
```

Dalam contoh sebelumnya, terdapat kelas `Memento` yang berfungsi sebagai wadah untuk menyimpan status internal `Originator`. `Memento` memiliki metode `getState()` untuk mengembalikan status yang disimpan.

Kemudian, terdapat kelas `Originator` yang merupakan objek yang memiliki status internal yang ingin disimpan dan dikembalikan. `Originator` memiliki metode `setState()` dan `getState()` untuk mengatur dan mengakses statusnya. Metode `saveStateToMemento()` digunakan untuk membuat `Memento` yang berisi snapshot dari status saat ini, sedangkan `restoreStateFromMemento()` digunakan untuk mengembalikan objek ke keadaan yang disimpan dalam `Memento`.

Selanjutnya, terdapat kelas `Caretaker` yang bertanggung jawab untuk mengelola `Memento` dan berinteraksi dengan `Originator`. `Caretaker` memiliki array `$mementos` untuk menyimpan `Memento`. Metode `addMemento()` digunakan untuk menambahkan `Memento` ke dalam array, sedangkan `getMemento()` digunakan untuk mendapatkan `Memento` berdasarkan indeksnya.

Dalam penggunaannya, `Originator` mengubah statusnya dengan menggunakan metode `setState()`. Ketika ingin menyimpan snapshot status saat ini, `Originator` menggunakan metode `saveStateToMemento()` untuk membuat `Memento`, yang kemudian ditambahkan ke `Caretaker` dengan metode `addMemento()`.

Jika ingin mengembalikan `Originator` ke keadaan yang disimpan dalam `Memento`, `Caretaker` menggunakan metode `getMemento()` untuk mendapatkan `Memento` berdasarkan indeksnya. Kemudian, `Originator` menggunakan metode `restoreStateFromMemento()` untuk mengembalikan objek ke keadaan yang disimpan dalam `Memento`. Setelah itu, `getState()` digunakan untuk mendapatkan status yang telah dikembalikan.

Dengan menggunakan pola Memento, kita dapat menyimpan status internal objek dan mengembalikannya jika diperlukan, tanpa mengungkapkan rincian implementasi kepada objek lain. Hal ini memungkinkan pemulihan keadaan objek setelah kegagalan atau pembatalan operasi.