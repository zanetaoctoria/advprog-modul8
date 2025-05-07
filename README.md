# Reflection : 8th Module

Name    : Rebecca Zaneta Octoria Hutajulu

NPM     : 2306275065

Class   : B

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
> - Unary: Client mengirim satu request, server mengirim satu response. Cocok untuk operasi sederhana seperti login atau validasi data. 
> - Server Streaming: Client mengirim satu request, server mengirim multiple responses. Ideal untuk pengambilan data berjumlah besar seperti hasil pencarian. 
> - Bi-directional Streaming: Client dan server dapat mengirim pesan secara independen dan simultan. Optimal untuk aplikasi interaktif seperti chat atau game online.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
> - Authentication: Implementasikan TLS/mTLS untuk verifikasi identitas client dan server. \
> - Authorization: Terapkan mekanisme kontrol akses berbasis peran untuk membatasi akses pengguna. \
> - Data Encryption: Gunakan protokol TLS untuk mengenkripsi data selama transmisi dan lindungi informasi sensitif.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
> 1. Kompleksitas Sinkronisasi: Mengelola aliran data dua arah secara bersamaan memerlukan mekanisme sinkronisasi yang tepat.
> 2. Penanganan Koneksi Terputus: Perlu strategi untuk mendeteksi dan mengatasi putusnya koneksi atau kegagalan jaringan.
> 3. Manajemen Memori: Aliran data yang terus-menerus dapat menyebabkan kebocoran memori jika tidak dikelola dengan baik.
> 4. Scaling dan Throughput: Menjaga performa sistem saat jumlah koneksi meningkat memerlukan desain yang efisien.
> 5. Penanganan Kesalahan: Sistem harus robust dalam menangani kesalahan dari client maupun server.

4. What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?
> Keunggulan:
> 1. Integrasi sempurna dengan ekosistem async Tokio.
> 2. Menyediakan abstraksi yang mudah digunakan untuk streaming data.
> 3. Mendukung backpressure secara otomatis melalui channel Tokio.

> Kelemahan:
> 1. Pemahaman mendalam tentang lifetime dan ownership Rust diperlukan untuk penggunaan yang tepat.
> 2. Potensi overhead karena lapisan abstraksi tambahan.
> 3. Keterbatasan dalam penanganan error yang kompleks.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
> Struktur kode gRPC di Rust sebaiknya menerapkan prinsip pemisahan tanggung jawab dengan membagi komponen menjadi modul-modul terpisah. Gunakan trait untuk mendefinisikan antarmuka yang jelas, implementasikan dependency injection untuk memudahkan testing, dan pisahkan logika bisnis dari implementasi gRPC. Organisasi kode yang baik juga mencakup penanganan error yang konsisten dan dokumentasi yang komprehensif.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
> - Implementasi Transaksi: Pastikan atomisitas operasi dengan pendekatan transaksional.
> - Integrasi dengan Gateway Pembayaran: Hubungkan dengan penyedia layanan pembayaran eksternal.
> - Mekanisme Retry: Rancang strategi untuk menangani kegagalan sementara.
> - Validasi Mendalam: Verifikasi semua data pembayaran dengan teliti.
> - Notifikasi Asinkron: Implementasikan sistem notifikasi untuk status pembayaran.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
> Adopsi gRPC menawarkan efisiensi komunikasi dengan serialisasi Protocol Buffers yang cepat dan efektif. Ini memungkinkan layanan dengan bahasa pemrograman berbeda untuk berkomunikasi secara lancar dan memungkinkan pembuatan kontrak API yang jelas. Namun, ini juga memerlukan pertimbangan tentang kompatibilitas dengan sistem yang menggunakan REST atau protokol lain, dan mungkin memerlukan gateway atau adapter untuk integrasi dengan teknologi yang ada.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
> Keunggulan: \
> HTTP/2 mendukung multiplexing, memungkinkan multiple request dan response dalam satu koneksi TCP, serta kompresi header yang mengurangi overhead jaringan dan meningkatkan throughput. \
> Kelemahan: \
> Implementasi HTTP/2 lebih kompleks dan mungkin kurang didukung di lingkungan legacy. Debugging juga bisa lebih sulit karena multiplexing dan encoding biner yang digunakan.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
> Model REST API tradisional mengharuskan client untuk melakukan polling atau inisiasi koneksi baru untuk setiap interaksi, menciptakan overhead dan latency yang dapat menghambat aplikasi real-time. Sebaliknya, kemampuan streaming dua arah gRPC memungkinkan komunikasi berkelanjutan, dimana server dapat mengirim data ke client kapan saja tanpa menunggu request baru, secara signifikan meningkatkan responsivitas dan mengurangi overhead jaringan untuk aplikasi yang membutuhkan update cepat dan konstan.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
> Protocol Buffers dalam gRPC memberikan keunggulan validasi tipe data yang ketat, serialisasi yang efisien, dan menghasilkan kode client/server otomatis yang menjamin konsistensi API. Namun, pendekatan berbasis skema ini kurang fleksibel dibandingkan JSON yang dapat berevolusi tanpa perubahan skema formal. Perubahan pada API gRPC memerlukan pembaruan .proto dan regenerasi kode, sementara REST dengan JSON dapat beradaptasi lebih mudah meskipun dengan risiko inkonsistensi data.
