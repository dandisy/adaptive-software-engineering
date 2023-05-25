Pola Strategy adalah pola desain yang memungkinkan pemisahan algoritma dari kelas yang menggunakannya. Pola ini memungkinkan kita untuk mendefinisikan sejumlah algoritma yang berbeda dan memilih algoritma yang sesuai saat runtime.

Pola Strategy terdiri dari tiga komponen utama: Konteks (Context), Strategi (Strategy), dan Interface Strategi (Strategy Interface). Konteks adalah kelas yang berinteraksi dengan strategi dan memegang referensi ke objek strategi yang digunakan. Strategi adalah kelas-kelas konkret yang mengimplementasikan algoritma-algoritma yang berbeda. Interface Strategi adalah antarmuka yang diterapkan oleh kelas-kelas strategi untuk memastikan konsistensi dalam implementasi metode-metode strategi.

Dengan menggunakan pola Strategy, kita dapat memilih algoritma yang sesuai pada saat runtime tanpa perlu mengubah konteks atau melibatkan logika yang kompleks di dalamnya. Pola ini juga memungkinkan fleksibilitas dalam menambahkan atau mengubah algoritma tanpa mengganggu kode yang ada.

Berikut adalah contoh praktis implementasi pola Strategy dengan PHP:

```php
<?php

// Interface Strategi
interface PaymentStrategy {
    public function pay($amount);
}

// Strategi Konkret - Pembayaran dengan Kartu Kredit
class CreditCardPayment implements PaymentStrategy {
    private $creditCardNumber;
    private $expirationDate;
    private $cvv;

    public function __construct($creditCardNumber, $expirationDate, $cvv) {
        $this->creditCardNumber = $creditCardNumber;
        $this->expirationDate = $expirationDate;
        $this->cvv = $cvv;
    }

    public function pay($amount) {
        echo "Paying $" . $amount . " with Credit Card\n";
        // Logika pembayaran dengan kartu kredit
    }
}

// Strategi Konkret - Pembayaran dengan PayPal
class PayPalPayment implements PaymentStrategy {
    private $email;
    private $password;

    public function __construct($email, $password) {
        $this->email = $email;
        $this->password = $password;
    }

    public function pay($amount) {
        echo "Paying $" . $amount . " with PayPal\n";
        // Logika pembayaran dengan PayPal
    }
}

// Konteks
class ShoppingCart {
    private $paymentStrategy;

    public function setPaymentStrategy(PaymentStrategy $paymentStrategy) {
        $this->paymentStrategy = $paymentStrategy;
    }

    public function checkout($amount) {
        $this->paymentStrategy->pay($amount);
    }
}

// Penggunaan Strategy
$shoppingCart = new ShoppingCart();

$creditCardPayment = new CreditCardPayment("1234567890", "12/24", "123");
$shoppingCart->setPaymentStrategy($creditCardPayment);
$shoppingCart->checkout(100.50);

$payPalPayment = new PayPalPayment("email@example.com", "password123");
$shoppingCart->setPaymentStrategy($payPalPayment);
$shoppingCart->checkout(75.25);

?>
```

Dalam contoh di atas, kita memiliki interface `PaymentStrategy` yang diterapkan oleh kelas-kelas strategi konkret `CreditCardPayment` dan `PayPalPayment`. Setiap kelas strategi mengimplementasikan metode `pay()` yang merupakan algoritma pembayaran yang berbeda.

Kemudian, kita memiliki kelas `ShoppingCart` sebagai konteks yang menggunakan strategi pembayaran. Kelas ini memiliki metode `setPaymentStrategy()` untuk mengatur strategi pembayaran yang akan digunakan dan metode `checkout()` untuk melakukan proses pembayaran dengan menggunakan strategi yang telah ditentukan.

Dalam penggunaannya, kita membuat objek `ShoppingCart` dan mengatur strategi pembayaran menggunakan objek `CreditCardPayment` atau `PayPalPayment`. Setelah itu, kita memanggil metode `checkout()` pada objek `ShoppingCart` dengan nilai jumlah yang akan dibayarkan.

Hasil output dari contoh di atas akan mencetak:

```
Paying $100.5 with Credit Card
Paying $75.25 with PayPal
```

Output tersebut menunjukkan bahwa saat melakukan checkout, objek `ShoppingCart` menggunakan strategi pembayaran yang telah ditentukan. Terlepas dari jenis strategi yang digunakan, metode `pay()` pada strategi yang sesuai akan dipanggil untuk melakukan proses pembayaran.

Pola Strategy sangat berguna ketika kita memiliki beberapa algoritma yang berbeda dan ingin memilih algoritma yang sesuai pada saat runtime. Dengan memisahkan algoritma ke dalam kelas-kelas strategi, kita dapat dengan mudah menambahkan, mengubah, atau mengganti algoritma tanpa mengubah struktur atau logika pada konteks yang menggunakannya.