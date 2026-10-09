# tugas-n8n-image-generator-telegram
# Image Generator Telegram (n8n)

**Nama:** Fachri Fadilah
**NIM:** 0110224146

Workflow n8n yang menerima prompt teks lewat n8n Form, membuat gambar
dengan API image generator (Kie AI), menunggu hasilnya dengan polling loop,
lalu mengirim gambar yang sudah diunduh ke pengguna lewat Telegram.

## Alur Workflow

```
Input Prompt -> Buat Task -> Tunggu 10 detik -> Cek Status -> Status Success?
                                  ^                              |-- true  -> Ambil URL Gambar -> Unduh Gambar -> Kirim ke Telegram
                                  |------------- false ----------|
```

## Node yang Digunakan

| Node | Fungsi |
|---|---|
| Input Prompt (n8n Form Trigger) | Menangkap prompt teks dari pengguna |
| Buat Task (HTTP Request, POST) | Mengirim prompt ke API dan mendapatkan `taskId` |
| Tunggu 10 detik (Wait) | Jeda 10 detik sebelum mengecek status |
| Cek Status (HTTP Request, GET) | Mengecek status task berdasarkan `taskId` |
| Status Success?
