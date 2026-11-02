# Çalışma takvimi (2 Kasım – 11 Aralık 2026)

Resmî ara teslim yoktur; bu bizim iç planımızdır. İç hedef: **6 Aralık'ta hat entegre ve test edilmiş**, 7–11 Aralık rapor + sıfırdan kurulum + teslim.

| Hafta | Rol 1 (toplu) | Rol 2 (akış) | Rol 3 (kalite) | Hafta sonu çıktısı |
|---|---|---|---|---|
| 2–8 Kas | Kit kurulumu, S3 inceleme | Kafka, olay inceleme | Depo, senaryo kartı, veri sözlüğü, Z1, Z0 taslak | `ortam.png`, `senaryo.txt`, 4 soru |
| 9–15 Kas | Toplu üretim, JSON→Parquet, kodekler, dosya düzeni | Bölüm anahtarı / sıcak nokta | Kirli veri sayımı, KVKK | Depolama ölçümleri |
| 16–22 Kas | `toplu_is.py`, join, explain, Spark UI, Delta | Akış tasarımı, ilk deneme | İki grafik, Z11 aday listesi | Toplu hat + grafikler |
| 23–29 Kas | Performans kararı (3×önce/sonra), Delta kesme deneyi | Watermark, sessiz sensör, MongoDB, pano | Entegrasyon, README | Çalışan canlı hat |
| 30 Kas–6 Ara | Depolama kırılma deneyleri | Watermark + restart deneyleri | Uçtan uca kanıt kontrolü | Z11 deneyleri |
| 7–11 Ara | Kendi rapor bölümleri | Kendi rapor bölümleri | Birleştirme, sunum, `teslim` etiketi, SABIS | **Teslim 11 Ara 23.59** |

Her hafta kısa durum toplantısı: ne çalışıyor, hangi ölçüm alındı, ne engelliyor.
