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

    Jawab:
    
    
    Waitgroup tanpa channel digunakan untuk menjalankan task atau job tanpa perlu mengirim data antar goroutine dan hanya perlu menunggu setiap groroutine selesai.
    
    waitgroup.go
    ```go
    
    func main() {
        var wg sync.WaitGroup
        totalWorker := 5
    
        for i := 1; i <= totalWorker; i++ {
            wg.Add(1)
            go worker(i, &wg, ch)
        }
    
       
        wg.Wait()
    
    }
    
    func worker(id int, wg *sync.WaitGroup) {
        defer wg.Done()
    
        // do task here
    }
       
    ```
    
    Channel digunakan untuk menerima/mengirim data antar goroutine.
    
    channel.go
    ```go
    
    func worker(id int, ch chan<- string) {
        ch <- fmt.Sprintf("Worker %d selesai", id)
    }
    
    func main() {
        ch := make(chan string, 3) // buffered channel dengan kapasitas 3
    
        // Jalankan 3 goroutine
        go worker(1, ch)
        go worker(2, ch)
        go worker(3, ch)
    
        // Terima hasil dari 3 goroutine
        for i := 0; i < 3; i++ {
            msg := <-ch
            fmt.Println(msg)
        }
    
        fmt.Println("Semua worker selesai.")
    }
       
    ```
    
    
    Channel dan Waitgroup digunakan bersamaan saat menjalankan beberapa goroutine, mengirim datanya ke channel dan perlu tahu kapan semua task atau job selesai sehingga dapat close channel dengan aman.
    
    channel_waitgroup.go
    ```go
    
    func worker(id int, wg *sync.WaitGroup, resultChan chan<- string) {
        defer wg.Done()
    
        result := fmt.Sprintf("Worker %d selesai", id)
    
        // Kirim hasil ke channel
        resultChan <- result
    }
    
    func main() {
        var wg sync.WaitGroup
        resultChan := make(chan string, 5) // buffered channel
    
        totalWorker := 5
    
        // Jalankan semua worker
        for i := 1; i <= totalWorker; i++ {
            wg.Add(1)
            go worker(i, &wg, resultChan)
        }
    
        // Goroutine khusus untuk menutup channel saat semua worker selesai
        go func() {
            wg.Wait()
            close(resultChan)
        }()
    
        // Terima semua hasil dari channel
        for msg := range resultChan {
            fmt.Println(msg)
        }
    
        fmt.Println("Semua pekerjaan selesai.")
    }
    
    ```


4. Apa yang anda ketahui dengan goroutine? Pernahkah memakainya? Ceritakan jika pernah, jelaskan kegunaan dan tujuan nya dalam project yang pernah anda kerjakan.

    Jawab:

    Goroutine adalah fitur di golang untuk menjalankan banyak task dalam waktu yang bersamaan. Goroutine di golang running in background proccess. Saya pernah menggunakan goroutine beberapa kali. Salah satunya adalah ketika saya membuat scheduler untuk generate tiga data report dalam format .csv kemudian upload file tersebut ke FTP dan mengirim message email jika proses berhasil maupun ada error. Saya menggunakan tiga goroutine untuk menjalankan tiga job tersebut.

5. Jelaskan apa yang anda ketahui mengenai queueing pada golang, dan buat contoh kode sederhana.

    Jawab:

    Queue adalah struktur antrian data yang menggunakan pola first in first out ( FIFO ) dimana data yang masuk terlebih dahulu akan kelaur lebih dahulu juga. Berikut contoh konsep queue sedehana.

    queue.go
    ```go
    
    type Queue []string

    // Tambah data ke belakang (enqueue)
    func (q *Queue) Enqueue(item string) {
        *q = append(*q, item)
    }
    
    // Ambil data dari depan (dequeue)
    func (q *Queue) Dequeue() (string, bool) {
        if len(*q) == 0 {
            return "", false // queue kosong
        }
        item := (*q)[0]
        *q = (*q)[1:] // hapus elemen pertama
        return item, true
    }
    
    func main() {
        var q Queue

        // Tambah data ke queue
        q.Enqueue("Job A")
        q.Enqueue("Job B")
        q.Enqueue("Job C")

        // Ambil data dari queue
        for {
            item, ok := q.Dequeue()
            if !ok {
                break
            }
            fmt.Println("Proses:", item)
        }
    }
    
    ```
 
6. Dalam microservices yang semuanya menggunakan Go, bagaimana cara/metode terbaik masing2 service berkomunikasi satu sama lain?
7. Buatlah contoh kode dalam Go, yang menggambarkan komunikasi antar service yang telah anda jelaskan diatas.
8. Bagaimana anda mengatasi error dalam Go? Ceritakan pengalaman anda.
9. Apakah anda memiliki pengalaman dalam error logging dalam Go? Jika ya, jelaskan bagaimana anda menyimpan atau menampilkan setiap log agar mudah dikelola, terutama dalam microservices.
