# Final Project Komputasi Awan

## Kelompok A4

| Nama | NRP |
|-----------------------|--------------|
| Muhammad Arsy Athallah | 5027221048 |
| Irfan Qobus Salim| 5027221058 |
| Hafiz Akmaldi Santosa| 5027221061 |
| Naufan Zaki Luqmanulhakim| 5027221065 |

## Permasalahan

Anda adalah seorang lulusan Teknologi Informasi, sebagai ahli IT, salah satu kemampuan yang harus dimiliki adalah Keampuan merancang, membangun, mengelola aplikasi berbasis komputer menggunakan layanan awan untuk memenuhi kebutuhan organisasi.

Pada suatu saat anda mendapatkan project untuk mendeploy sebuah aplikasi Sentiment Analysis dengan komponen Backend menggunakan python: sentiment-analysis.py dengan spesifikasi sebagai berikut

## Endpoints

1. Analyze Text
    - **Endpoints:** `POST /analyze`
    - **Description:**  This endpoint accepts a text input and returns the sentiment score of the text.

    - **Requests:**
    ~~~
    {
    "text": "Your text here"
    }
    ~~~

    - **Response:**
    ~~~
    {
    "sentiment": <sentiment_score>
    }
    ~~~

2. Retrieve History
    - **Endpoint:** `GET /history`
    - **Description:** This endpoint retrieves the history of previously analyzed texts along with their sentiment scores.
    - **Response:**
    ~~~
    {
        {
   "text": "Your previous text here",
   "sentiment": <sentiment_score>
    }, 
    ...
    }
    ~~~

    Kemudian juga disediakan sebuah Frontend sederhana menggunakan index.html dan styles.css dengan tampilan antarmuka sebagai berikut
    ![alt text](image.png)
    Kemudian anda diminta untuk mendesain arsitektur cloud yang sesuai dengan kebutuhan aplikasi tersebut. Apabila dana maksimal yang diberikan adalah 1 juta rupiah per bulan (65 US$) konfigurasi cloud terbaik seperti apa yang bisa dibuat?

    ## Rancangan Arsitektur Cloud

    Pada rancangan ini kami menggunakan model yaitu 1 web service, 1 load balancer, 2 worker, dan 1 database seperti gambar berikut:
   
    ![alt text](image-1.png)

    pada rancangan tersebut kami menggunakan Google Cloud Platform dengan spesifikasi seperti berikut:

   ![WhatsApp Image 2024-06-21 at 15 20 47_e84389c0](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/c1de1180-f676-416c-8d4a-00ba117ac7ba)


    | Nama | Spesifikasi | Harga |
    |-----------------------|--------------| --------- |
    | Client - 10.184.0.5 | 2 vCPU + 4 GB memory + 25 GB disk | $9.52 |
    | Database - 10.184.0.4 | 2 vCPU + 4 GB memory + 25 GB disk | $9.52 |
    | Load Balancer - 10.184.0.3| 2 vCPU + 4 GB memory + 25 GB disk |  $9.52 |
    | Worker 1 - 10.184.0.2 | 2 vCPU + 4 GB memory + 25 GB disk | $9.52 |
    | Worker 2 - 10.184.0.6 | 2 vCPU + 4 GB memory + 25 GB disk | $9.52 |
    |Total | | $47.6 |

    ## Implementasi

    ### Set Up dan Konfigurasi Database
    
    ![alt text](<WhatsApp Image 2024-06-20 at 23.16.36_199de0f0.jpg>)
    lakukan config awal untuk meng set up database dengan menggunakan command seperti ini:
    ~~~
    sudo apt update
    sudo apt upgrade

    # Install dependency
    sudo apt install gnupg wget apt-transport-https ca-certificates software-properties-common
    echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.list.d/focal-security.list
    sudo apt-get update
    sudo apt-get install libssl1.1

    # Install mongodb
    wget -qO- https://pgp.mongodb.com/server-7.0.asc | gpg --dearmor | sudo tee /usr/share/keyrings/mongodb-server-7.0.gpg >/dev/null
    echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu $(lsb_release -cs)/mongodb-org/7.0 multiverse" | sudo tee -a         /etc/apt/sources.list.d/mongodb-org-7.0.list
    sudo apt update
    sudo apt install mongodb-org -y
    ~~~

    Lanjutkan untuk Enable MongoDb dengan commmand seperti berikut:
    ~~~
    sudo systemctl start mongod
    sudo systemctl enable mongod
    ~~~

    Masuk ke Konfigurasi MongoDB dengan `sudo nano /etc/mongod.conf`

    ![alt text](<WhatsApp Image 2024-06-20 at 23.17.34_dcb5e892.jpg>)

    ![alt text](<WhatsApp Image 2024-06-20 at 23.30.53_7d6e15c2.jpg>)

    Membuat User dan Pass

    ![alt text](<WhatsApp Image 2024-06-20 at 23.41.06_20ae04c5.jpg>)

    ![alt text](<WhatsApp Image 2024-06-20 at 23.42.42_5ab5e758.jpg>)

    ### Set Up Client

    ![alt text](<WhatsApp Image 2024-06-21 at 00.03.20_42fecd6e.jpg>)

    ### Set Up Worker - 1

    ![alt text](<WhatsApp Image 2024-06-21 at 00.28.33_19c8f695.jpg>)

    ### Set Up Worker - 2

    ![alt text](<WhatsApp Image 2024-06-21 at 01.14.04_f590653b.jpg>)

    ### Uji Coba Get /history
    ![alt text](<WhatsApp Image 2024-06-21 at 10.58.56_29ab6bbc.jpg>)

    ### Uji Coba Post /analyze
    ![alt text](<WhatsApp Image 2024-06-21 at 10.59.29_127df4ec.jpg>)

   ### Uji Coba Di Locust

   **Berikut merupakan IP yang digunakan: 34.101.54.162 dan 34.101.181.48**
    
    ### 1. Berapakah jumlah Request per seconds (RPS) maksimum yang dapat ditangani oleh server dengan durasi waktu load testing 60 detik? (tingkat failure harus 0%)
   ![WhatsApp Image 2024-06-21 at 16 05 47_186fdda1](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/7ea449d2-072d-4263-902c-af02281e7952)

    RPS yang didapatkan berjumlah 130 Request
    ***
    ### 2. Berapa jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 50 dan durasi waktu load testing 60 detik? (tingkat failure harus 0%)
   ![WhatsApp Image 2024-06-21 at 16 05 47_186fdda1](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/7ea449d2-072d-4263-902c-af02281e7952)
   RPS yang didapatkan berjumlah 131.4 (19.71 poin)
   ***
    ### 3. Berapa jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 100 dan durasi waktu load testing 60 detik? (tingkat failure harus %)
    ![WhatsApp Image 2024-06-21 at 16 09 49_a6614a03](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/e0283b42-1672-4c67-bd65-2a00215ae0c4)
    RPS yang didapatkan berjumlah 130.8 (19.62 poin)
   ***
    ### 4. Berapa jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 200 dan durasi waktu load testing 60 detik? (tingkat failure harus 0%)

    ![WhatsApp Image 2024-06-21 at 16 12 38_0ff690fb](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/d64a3ff4-5332-4365-8cd2-c57fc2ffd8dd)
    RPS yang didapatkan berjumlah 133.2 (19.98 poin)
   ***
    ### 5. Berapa jumlah peak concurrency maksimum yang dapat ditangani oleh server dengan spawn rate 500 dan durasi waktu load testing 60 detik? (tingkat failure harus 0%)
   ![WhatsApp Image 2024-06-21 at 16 14 46_2d8b1859](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/34a16dd7-75df-4351-aee2-5f8308cbdb5e)
    RPS yang didapatkan berjumlah 133.7 (20.055 poin)
    ***
    ## Dashboard Project GCP
   ![WhatsApp Image 2024-06-21 at 16 16 44_5a94c39d](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/406a125d-1923-4e49-8675-ff37d1684862)


   ## Kesimpulan

   Bisa disimpulkan bahwa semakin besar spesifikasi yang digunakan pada suatu environment cloud, maka angka request per second yang dapat di-handle akan semakin besar.

## Video Demo Revisi

https://youtu.be/KNxJaqDo8-A

    


    





    
