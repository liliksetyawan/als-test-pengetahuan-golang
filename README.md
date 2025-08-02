# als-test-pengetahuan-golang
1. Framework golang apa saja yang pernah anda pakai? Dan jelaskan secara singkat dengan framework tersebut project apa yang anda kerjakan dan mengapa menggunakan framework tersebut. 

Jawab: 
- Saya menggunakan framework gormmigarte untuk running sql migration. Saya menggunakan gormmigrate karena lebih mudah untuk manajemen perubahan table maupun data dan setiap perubahan dapat terrecord dengan baik pada table gorm_migration. Saya menggunakan framework tersebut pada project Nexchief2 dan Grochat.
- Framework gorilla/mux untuk handle routing. Saya menggunakan gorilla/mux karena framework tersebut salah satu framework yang banyak digunakan untuk hanle routing dan penggunaanya juga cukup mudah. Saya menggunakan framework tersebut di project Nexchief2 dan Grochat.
- Framework dgrr/fastws untuk handle websocket. Framework tersebut cukup lightweight untuk digunakan. Saya menggunakan framework tersebut pada project Grochat.


2. Jelaskan apa yang anda ketahui mengenai concurrency pada golang?

Jawab:
Concurrency pada golang adalah cara untuk menangani beberapa task atau job yang berjalan secara bersamaan (parallel). Concurrency di golang menggunakan goroutine atau dengan bantuan channle agar setiap goroutine dapat saling terhubung.


3. Buatlah contoh kode/function golang yang memanfaatkan antara WaitGroup dan Channel, dan jelaskan kapan bisa menggunakan waitgroup atau channel atau keduanya secara bersamaan.
4. Apa yang anda ketahui dengan goroutine? Pernahkah memakainya? Ceritakan jika pernah, jelaskan kegunaan dan tujuan nya dalam project yang pernah anda kerjakan.
5. Jelaskan apa yang anda ketahui mengenai queueing pada golang, dan buat contoh kode sederhana.
6. Dalam microservices yang semuanya menggunakan Go, bagaimana cara/metode terbaik masing2 service berkomunikasi satu sama lain?
7. Buatlah contoh kode dalam Go, yang menggambarkan komunikasi antar service yang telah anda jelaskan diatas.
8. Bagaimana anda mengatasi error dalam Go? Ceritakan pengalaman anda.
9. Apakah anda memiliki pengalaman dalam error logging dalam Go? Jika ya, jelaskan bagaimana anda menyimpan atau menampilkan setiap log agar mudah dikelola, terutama dalam microservices.
