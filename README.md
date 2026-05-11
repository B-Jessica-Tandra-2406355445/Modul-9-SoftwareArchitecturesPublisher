> a. How much data your publisher program will send to the message broker in one run?  

Dalam satu kali eksekusi (run), program publisher akan mengirimkan lima buah data atau event ke message broker. Hal ini secara eksplisit terlihat pada kode di dalam fungsi utama program publisher, di mana terdapat lima pemanggilan fungsi untuk mempublikasikan pesan pembuatan pengguna baru (user created event) secara berturut-turut, yaitu memuat data untuk pengguna bernama Amir, Budi, Cica, Dira, dan Emir .

> b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean? 

Kesamaan URL koneksi antara program publisher dan subscriber mengindikasikan bahwa kedua program independen tersebut terhubung ke instansiasi message broker RabbitMQ yang persis sama. Dalam arsitektur event-driven, kesamaan jalur komunikasi ini sangat krusial karena program pengirim (publisher) harus meletakkan event pada sebuah queue yang sama dengan titik tempat program penerima (subscriber) mendengarkan atau mengonsumsi pesan tersebut. Jika URL berbeda, maka subscriber tidak akan pernah menerima event yang dipublikasikan oleh publisher.