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

    | Nama | Spesifikasi | Harga |
    |-----------------------|--------------| --------- |
    | Client - 10.184.0.5 | 2 vCPU + 4 GB memory + 25 GB disk | $36.14 |
    | Database - 10.184.0.4 | 2 vCPU + 4 GB memory + 25 GB disk | $36.14 |
    | Load Balancer - 10.184.0.3| 2 vCPU + 4 GB memory + 25 GB disk |  $36.14 |
    | Worker 1 - 10.184.0.2 | 2 vCPU + 4 GB memory + 25 GB disk | $36.14 |
    | Worker 2 - 10.184.0.6 | 2 vCPU + 4 GB memory + 25 GB disk | $36.14 |
    |Total | | $180.7 |

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

   ### Uji Coba Di Locust

   ![WhatsApp Image 2024-06-21 at 11 48 30_2487ecde](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/85f45716-1197-4764-83b5-24ac303c0a1c)

   ![WhatsApp Image 2024-06-21 at 13 57 13_9fa09c1c](https://github.com/NaufanZaki/FP-TKA-A04/assets/128389289/a9febdd8-244d-4fe7-9a16-daec6a5eca3d)


   ## Kesimpulan


    


    





    
