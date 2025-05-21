<div align="center">
    <h1>MODULE 10 - TIMER</h1>
</div>

<div align="center">
    <img src="assets/images/burhancurse.png" alt="burhan" width="200"/>
</div>

<div align="center">
    <h2>Alwie Attar Elfandra</h2>
    <h2>2306241726</h2>
</div>

__1.2 Understanding how it works__

<div align="center">
    <img src="assets/images/foto1.jpg" alt="foto"/>
</div>

Berdasarkan hasil outputnya, dapat dipahami bahwa fungsi async yang dijalankan menggunakan executor akan dieksekusi **secara asinkron** dan **dijadwalkan terpisah dari alur utama program (`main`)**.

Pada program ini, perintah `println!("Attar's Computer: awo");` berada di luar future dan dieksekusi secara langsung di `main()`. Sementara itu, blok async yang berisi `"howdy!"` dan `"done!"` hanya akan dijalankan ketika future-nya dipoll oleh executor melalui `executor.run()`.

Akibatnya, urutan output menjadi:

1. `"awo"` dicetak dulu karena merupakan kode sinkron biasa.
2. Setelah executor mulai berjalan, task async dijalankan:

   * Mencetak `"howdy!"`
   * Menunggu `TimerFuture`, yang membuat task tertunda selama 2 detik.
3. Setelah timer selesai, task dibangunkan dan dilanjutkan, lalu mencetak `"done!"`.

Ini mencerminkan bagaimana mekanisme asynchronous Rust bekerja: future tidak langsung dieksekusi, melainkan dipoll oleh executor, dan executor akan mengatur lifecycle dari setiap future.