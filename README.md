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
    - **Description:** Endpoint ini menerima input teks dan mengembalikan skor sentimen dari teks tersebut.
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


