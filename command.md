Command adalah pola desain yang termasuk dalam kategori pola Behavioral. Pola ini memungkinkan pemisahan antara permintaan atau aksi yang dilakukan oleh klien dan objek yang melaksanakan aksi tersebut. Command mengemas permintaan sebagai objek yang dapat diproses secara terpisah, sehingga memungkinkan fleksibilitas, penjadwalan, atau penundaan eksekusi permintaan.

Pola Command terdiri dari empat komponen utama: Receiver (penerima), Command (perintah), Invoker (pengundang), dan Client (klien).

- **Receiver**: Merupakan objek yang berisi logika bisnis atau implementasi nyata dari aksi yang akan dilakukan.
- **Command**: Merupakan antarmuka atau kelas abstrak yang menyediakan metode yang direpresentasikan sebagai permintaan. Biasanya memiliki metode `execute()` untuk menjalankan aksi.
- **Invoker**: Bertanggung jawab untuk memanggil atau mengeksekusi perintah yang diberikan. Invoker tidak perlu mengetahui detail implementasi dari perintah yang diberikan.
- **Client**: Menciptakan objek Command dan menentukan Receiver yang sesuai untuk setiap perintah.

Berikut adalah contoh praktis implementasi Command dengan PHP:

```php
<?php

// Receiver
class Light {
    public function turnOn() {
        echo "Lampu dinyalakan.\n";
    }

    public function turnOff() {
        echo "Lampu dimatikan.\n";
    }
}

// Command
interface Command {
    public function execute();
}

// Concrete Command
class TurnOnCommand implements Command {
    private $light;

    public function __construct(Light $light) {
        $this->light = $light;
    }

    public function execute() {
        $this->light->turnOn();
    }
}

// Concrete Command
class TurnOffCommand implements Command {
    private $light;

    public function __construct(Light $light) {
        $this->light = $light;
    }

    public function execute() {
        $this->light->turnOff();
    }
}

// Invoker
class RemoteControl {
    private $command;

    public function setCommand(Command $command) {
        $this->command = $command;
    }

    public function pressButton() {
        $this->command->execute();
    }
}

// Client
$light = new Light();
$turnOnCommand = new TurnOnCommand($light);
$turnOffCommand = new TurnOffCommand($light);

$remoteControl = new RemoteControl();

$remoteControl->setCommand($turnOnCommand);
$remoteControl->pressButton();

$remoteControl->setCommand($turnOffCommand);
$remoteControl->pressButton();

?>
```

Dalam contoh di atas, terdapat `Light` yang berperan sebagai Receiver, yaitu objek yang menerima dan melaksanakan aksi. Terdapat juga `Command` sebagai antarmuka yang menyediakan metode `execute()` yang akan diimplementasikan oleh Concrete Command, yaitu `TurnOnCommand` dan `TurnOffCommand`. 

Selanjutnya, terdapat `RemoteControl` sebagai Invoker, yang memiliki metode `setCommand()` untuk mengatur perintah yang akan dieksekusi, dan metode `pressButton()` untuk memanggil dan menjalankan perintah tersebut.

Pada saat penggunaannya, Client menciptakan objek Command ses