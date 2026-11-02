# Z11 — "Bu sistem nerede kırılır?" planı (notun %20'si)

Adaylar ilk günden toplanır; deneyler süreç boyunca yapılır. Raporda en az 3 nokta, en az 1 gerçek deney (`kanit/kirilma-deneyi.*`), en az 2 sayfa.

| # | Kırılma noktası | Tetikleyen | Belirti — neye bakınca görürüz | Ne yaparız | Deney | Sorumlu |
|---|---|---|---|---|---|---|
| 1 | Tek Kafka düğümü | `docker compose stop kafka` | üretici zaman aşımı, tüketici gecikmesi | 3 düğüm, RF=3, `min.insync.replicas=2` | planlandı | Rol 2 |
| 2 | Geç veri watermark'ı aşar | `--gec-orani 0.3` | sayıma girmeyen olay sayısı artar | watermark süresi ↔ uyarı gecikmesi ödünleşimi | planlandı (Z8 ile ortak) | Rol 2 |
| 3 | Akış işi yeniden başlar | işi durdur/başlat, `--cikti s3` | kayıp ya da çift sayım | checkpoint + idempotent/atomik yazma | planlandı (Z8 ile ortak) | Rol 2 |
| 4 | S3 yazma sırasında gider | `docker compose stop s3` (toplu iş çalışırken) | iş hatası, yarım dosyalar | Delta atomik commit; çıplak Parquet ile karşılaştır | planlandı (Z7 ile ortak) | Rol 1 |
| 5 | Sıcak bölüm / çarpık anahtar | üreticinin çarpık sensörleri | en dolu bölüm ÷ ortalama yüksek, görev süresi dağılımı kuyruklu | anahtar değişikliği / tuzlama | planlandı (Z3, Z5) | Rol 1–2 |
| 6 | Tepe yük | `--hiz` = karttaki tepe | tüketici gecikmesi büyür, mikro-yığın süresi > tetik aralığı | bölüm/çekirdek ölçekleme | aday | Rol 2 |
| 7 | Sessiz sensör yanlış alarmı | ağ kesintisi sonrası toplu geç veri | sustu → geri geldi dalgalanması | zaman aşımını kart + geç veri dağılımından seç | aday | Rol 2–3 |
| 8 | Küçük dosya patlaması | çok sık akış yazımı | S3 listeleme süresi, dosya sayısı | birleştirme / `OPTIMIZE` | aday | Rol 1 |

Her deney için yaz: **ne gördük** (hata iletisi, gecikme, eksik sonuç) · **neye bakınca** · **gerçek sistemde ne yapardık**. "Hiçbir yerde kırılmaz" = 0 puan.
