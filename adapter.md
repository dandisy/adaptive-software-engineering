Adapter adalah pola desain yang termasuk dalam kategori pola Struktural. Pola ini digunakan untuk menyatukan dua antarmuka yang tidak kompatibel dan memungkinkan mereka untuk bekerja bersama. Adapter bertindak sebagai perantara antara dua kelas atau komponen yang berbeda sehingga mereka dapat berkomunikasi dan berinteraksi secara harmonis.

Adapter digunakan ketika ada kelas atau komponen yang memiliki antarmuka yang tidak sesuai dengan antarmuka yang diharapkan oleh klien. Dengan menggunakan adapter, klien dapat menggunakan antarmuka yang diharapkan tanpa perlu memodifikasi kode klien atau komponen yang ada.

Ada dua jenis adapter yang umum digunakan:

1. **Adapter Objek**: Adapter objek menggunakan komposisi untuk menghubungkan dua antarmuka yang tidak kompatibel. Adapter ini memiliki referensi ke objek yang tidak sesuai dan menerapkan antarmuka yang diharapkan oleh klien.

2. **Adapter Kelas**: Adapter kelas menggunakan warisan (inheritance) untuk menghubungkan dua antarmuka yang tidak kompatibel. Adapter ini mewarisi kelas yang tidak sesuai dan mengimplementasikan antarmuka yang diharapkan oleh klien.

Berikut adalah contoh praktis implementasi Adapter dengan PHP menggunakan adapter objek:

```php
<?php

// Target
interface MediaPlayer {
    public function play($filename);
}

// Adaptee
class AdvancedMediaPlayer {
    public function playVlc($filename) {
        echo "Memutar file VLC: " . $filename . "\n";
    }

    public function playMp4($filename) {
        echo "Memutar file MP4: " . $filename . "\n";
    }
}

// Adapter
class MediaAdapter implements MediaPlayer {
    private $advancedMediaPlayer;

    public function __construct(AdvancedMediaPlayer $advancedMediaPlayer) {
        $this->advancedMediaPlayer = $advancedMediaPlayer;
    }

    public function play($filename) {
        $fileExtension = pathinfo($filename, PATHINFO_EXTENSION);
        if ($fileExtension === 'vlc') {
            $this->advancedMediaPlayer->playVlc($filename);
        } elseif ($fileExtension === 'mp4') {
            $this->advancedMediaPlayer->playMp4($filename);
        }
    }
}

// Client
class AudioPlayer implements MediaPlayer {
    private $mediaAdapter;

    public function play($filename) {
        $fileExtension = pathinfo($filename, PATHINFO_EXTENSION);
        if ($fileExtension === 'mp3') {
            echo "Memutar file MP3: " . $filename . "\n";
        } elseif ($fileExtension === 'vlc' || $fileExtension === 'mp4') {
            $this->mediaAdapter = new MediaAdapter(new AdvancedMediaPlayer());
            $this->mediaAdapter->play($filename);
        } else {
            echo "Format file tidak didukung.\n";
        }
    }
}

// Penggunaan Adapter
$audioPlayer = new AudioPlayer();
$audioPlayer->play("file.mp3");
$audioPlayer->play("file.vlc");
$audioPlayer->play("file.mp4");
$audioPlayer->play("file.avi");

?>
```

Dalam contoh di atas, terdapat `MediaPlayer` yang merupakan target yang diharapkan oleh klien. `AdvancedMediaPlayer` adalah adaptee yang memiliki antarmuka yang tidak sesuai dengan `MediaPlayer`. Kemudian, terdapat `MediaAdapter` yang bertindak sebagai adapter objek dengan menggunakan komposisi untuk menghubungkan antarm