Proxy adalah pola desain yang termasuk dalam kategori pola Struktural. Pola ini digunakan untuk menyediakan objek pengganti atau placeholder untuk objek asli. Proxy bertindak sebagai perantara antara klien dan objek asli, sehingga klien tidak perlu berinteraksi langsung dengan objek asli.

Pola Proxy berguna dalam situasi di mana objek asli memiliki biaya komputasi atau sumber daya yang tinggi untuk dibuat, atau ketika objek asli harus dilindungi dari akses langsung oleh klien. Proxy memungkinkan klien untuk melakukan operasi tertentu pada objek asli melalui objek proxy, yang dapat melakukan tugas tambahan seperti caching, validasi, kontrol akses, atau logging.

Berikut adalah contoh praktis implementasi Proxy dengan PHP:

```php
<?php

// Abstraksi antarmuka yang diperlukan oleh klien dan proxy
interface Subject {
    public function request();
}

// Implementasi konkret dari subjek asli
class RealSubject implements Subject {
    public function request() {
        echo "RealSubject: Menjalankan permintaan.\n";
    }
}

// Implementasi konkret dari proxy
class Proxy implements Subject {
    private $realSubject;

    public function request() {
        if ($this->realSubject === null) {
            $this->realSubject = new RealSubject();
        }
        $this->preRequest();
        $this->realSubject->request();
        $this->postRequest();
    }

    private function preRequest() {
        echo "Proxy: Persiapan permintaan.\n";
    }

    private function postRequest() {
        echo "Proxy: Penanganan permintaan setelahnya.\n";
    }
}

// Penggunaan Proxy
$proxy = new Proxy();
$proxy->request();

?>
```

Dalam contoh di atas, terdapat abstraksi antarmuka `Subject` yang diperlukan oleh klien dan proxy. Implementasi konkret `RealSubject` adalah subjek asli yang akan diakses oleh klien melalui proxy. Implementasi konkret `Proxy` bertindak sebagai proxy yang menyediakan pengganti untuk `RealSubject`.

Ketika klien melakukan permintaan (`$proxy->request()`), proxy melakukan persiapan permintaan (`preRequest()`), kemudian membuat instance `RealSubject` jika belum ada. Setelah itu, proxy memanggil metode `request()` pada `RealSubject`. Setelah penanganan permintaan selesai, proxy juga dapat melakukan tugas tambahan setelahnya (`postRequest()`).

Dengan menggunakan proxy, klien tidak perlu berinteraksi langsung dengan `RealSubject`. Proxy bertanggung jawab untuk mengelola objek asli dan dapat melakukan tugas tambahan sebelum dan setelah pemanggilan metode pada objek asli.