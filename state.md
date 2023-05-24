State adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini memungkinkan objek mengubah perilakunya ketika keadaannya berubah. State memodelkan berbagai keadaan sebagai objek-objek terpisah, dan objek tersebut dapat beralih dari satu keadaan ke keadaan lain secara dinamis.

Pola State membantu memisahkan logika keadaan dari objek utama. Setiap keadaan diimplementasikan sebagai kelas yang terpisah dengan metode-metode yang sesuai untuk menggambarkan perilaku keadaan tersebut. Objek utama memiliki referensi ke objek keadaan saat ini, dan ketika keadaan berubah, objek utama memperbarui referensinya ke objek keadaan baru.

Berikut adalah contoh praktis implementasi State dengan PHP:

```php
<?php

// State (Keadaan)
interface State {
    public function handle();
}

// Concrete State (Keadaan Konkret)
class StateA implements State {
    public function handle() {
        echo "Menghandle keadaan A.\n";
    }
}

// Concrete State (Keadaan Konkret)
class StateB implements State {
    public function handle() {
        echo "Menghandle keadaan B.\n";
    }
}

// Context (Konteks)
class Context {
    private $state;

    public function __construct() {
        // Menginisialisasi keadaan awal
        $this->state = new StateA();
    }

    public function setState(State $state) {
        $this->state = $state;
    }

    public function request() {
        $this->state->handle();
    }
}

// Penggunaan State
$context = new Context();

$context->request(); // Menghandle keadaan A
$context->setState(new StateB());
$context->request(); // Menghandle keadaan B

?>
```

Dalam contoh di atas, terdapat antarmuka `State` yang menggambarkan metode `handle()` yang akan diimplementasikan oleh keadaan konkret. Keadaan konkret, yaitu `StateA` dan `StateB`, masing-masing mengimplementasikan metode `handle()` sesuai dengan perilaku keadaannya.

Kemudian, terdapat kelas `Context` yang merupakan objek utama yang memiliki referensi ke objek keadaan saat ini. `Context` memiliki metode `setState()` untuk mengubah keadaan saat ini, dan metode `request()` yang memanggil metode `handle()` pada keadaan saat ini.

Pada saat penggunaannya, ketika `request()` dipanggil pada objek `Context`, metode `handle()` dari keadaan yang saat ini berlaku akan dipanggil dan perilaku sesuai dengan keadaan tersebut akan dieksekusi.