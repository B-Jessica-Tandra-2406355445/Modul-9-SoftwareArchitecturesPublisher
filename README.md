> a. How much data your publisher program will send to the message broker in one run?  

Dalam satu kali eksekusi (run), program publisher akan mengirimkan lima buah data atau event ke message broker. Hal ini secara eksplisit terlihat pada kode di dalam fungsi utama program publisher, di mana terdapat lima pemanggilan fungsi untuk mempublikasikan pesan pembuatan pengguna baru (user created event) secara berturut-turut, yaitu memuat data untuk pengguna bernama Amir, Budi, Cica, Dira, dan Emir .

> b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean? 

Kesamaan URL koneksi antara program publisher dan subscriber mengindikasikan bahwa kedua program independen tersebut terhubung ke instansiasi message broker RabbitMQ yang persis sama. Dalam arsitektur event-driven, kesamaan jalur komunikasi ini sangat krusial karena program pengirim (publisher) harus meletakkan event pada sebuah queue yang sama dengan titik tempat program penerima (subscriber) mendengarkan atau mengonsumsi pesan tersebut. Jika URL berbeda, maka subscriber tidak akan pernah menerima event yang dipublikasikan oleh publisher.

## Screenshot of running RabbitMQ

![](image/RabbitMQ.png)

## Sending and processing event

![](image/Consoles.png)

Komunikasi antara publisher dan subscriber berhasil dilakukan melalui message broker RabbitMQ. Pada console publisher, aplikasi mengirim lima event “User Created” yang berisi data pengguna. Secara bersamaan, console subscriber yang berjalan di WSL berhasil menerima dan memproses pesan-pesan tersebut tanpa adanya error null pointer. Hal ini menunjukkan bahwa sistem event-driven telah berfungsi dengan baik, di mana publisher bertindak sebagai producer dan subscriber sebagai consumer. Dengan menggunakan WSL, subscriber dapat menangani proses eksekusi dengan baik sesuai kebutuhan.

## Monitoring chart based on publisher

![](image/RabbitMQ-spikes.png)

Grafik monitoring RabbitMQ tersebut dengan jelas memvisualisasikan interaksi event-driven selama eksekusi program berlangsung. Lonjakan pada grafik “Message rates” menunjukkan momen ketika publisher mengirim lima event pembuatan user, yang kemudian langsung ditangani oleh message broker. Terlihat bahwa tingkat “Publish” (garis oranye) dan “Consumer ack” (garis ungu) mencapai puncak secara bersamaan, menandakan bahwa pesan diproduksi dan dikonsumsi secara real-time. Hal ini mengonfirmasi bahwa koneksi antara aplikasi Rust dan instance RabbitMQ berjalan dengan stabil dan efisien. Aktivitas kemudian kembali ke angka nol setelah seluruh lima event yang telah ditentukan di dalam kode publisher selesai diproses sepenuhnya.