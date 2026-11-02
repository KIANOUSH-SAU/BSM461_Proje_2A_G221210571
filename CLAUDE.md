# BSM461 Büyük Veri Dönem Projesi — IoT Sensör İzleme ve Anomali Tespit Sistemi

Sakarya Üniversitesi, BSM 461 Büyük Veriye Giriş, 2026–2027 Güz, Dr. Öğr. Üyesi Sümeyye Kaynak.
Şablon 3 (IoT) **kesin seçildi** — başka şablona yönlendirme.

## Resmî kaynak
- Yönerge: `~/Downloads/Proje-Odevi (1).pdf` (27 sayfa). Çelişkide yönerge ve gerçek `kit/` önceliklidir.
- Teslim: **11 Aralık 2026 Cuma 23.59**, tek teslim. Public repo `BSM461_Proje_<şube>_<grupkodu>`, `teslim` git etiketi teslimden önce.
- Notun en büyük kalemi Z11 (kırılma) = 20/100; Z5 ve Z8 = 10'ar.

## Kesin kurallar
- **Ölçülmemiş hiçbir sayı yazma.** Ölçülmeyen sayı → o bileşen sıfır. Her ölçüm `kanit/olcumler.csv`'ye (birim, tekrar, veri boyutu, makine).
- Uydurma kaynak/alıntı yok (−10).
- Kit dosyalarını (`uretici.py`, `toplu_is.py`, `akis_iskelet.py`…) elle yeniden yazma; kitten başla.
- Ham veri depoya girmez; `--grup <kod>` ile yeniden üretilebilir.
- Her yapay zekâ kullanımını `docs/yz-kullanim-gunlugu.md`'ye ekle (Z12 beyanı buradan çıkar).
- Komutlar `kit/` dizininde çalışır: `docker compose exec araclar …`, `docker compose exec spark spark-submit …`.

## Ortam
- Bu makine: macOS, Apple M4, 16 GB RAM. Docker Desktop'a ≥5 GB (ES+Kibana ile 7 GB).
- Kafka konusu `sensorler`; S3 = SeaweedFS `localhost:8333`, kovalar `ham`, `islenmis`, `tablolar`; Spark UI `localhost:4040`.

## Durum ve açık bilgiler
Bkz. `docs/durum.md` (neyin yapıldığı, neyin beklediği). Plan: `docs/`.
