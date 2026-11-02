# Görev dağılımı

Yönerge Bölüm 11'deki öneriye dayanır. İsimler henüz atanmadı.

| Rol | Üye | Birincil bileşenler | Dal |
|---|---|---|---|
| 1 — Depolama ve toplu hat | *?* | Z2, Z4, Z5, Z7 | `feature/batch` |
| 2 — Akış hattı ve servis | *?* | Z3, Z6, Z8, Z9 | `feature/stream` |
| 3 — Ölçek, veri kalitesi, entegrasyon | *?* | Z1, Z10, Z11 derlemesi | `feature/kalite` |
| Ortak | herkes | Z0, Z11 | — |

## Rol 1 — Depolama ve toplu hat
- S3 dizin düzeni (`s3://ham/iot/tarih=…/`), dosya sayısı/boyutu, küçük dosya birleştirme (Z4)
- JSON ↔ Parquet boyut ve sorgu süresi; snappy / zstd / gzip (Z2)
- `is/toplu_is.py`: temizleme → `sensorler.csv` join → toplulaştırma → yazma; `explain(mode="formatted")` → `kanit/explain-1.txt`, her Exchange'in açıklaması; Spark UI görüntüsü; ≥3 tekrarlı önce/sonra performans kararı (Z5)
- Delta: ikinci yazma, `DESCRIBE HISTORY`, `versionAsOf`, milyonlarca satırla yarıda kesme deneyi + çıplak Parquet karşılaştırması (Z7)

## Rol 2 — Akış hattı ve servis
- Aday bölüm anahtarları; 8 bölümde en dolu ÷ ortalama; sıcak nokta çözümü önce/sonra; tekrar sayımı; CAP/PACELC (Z3)
- `sensorler` konusu: bölüm sayısı (karttaki hıza göre), anahtar, sıra garantisi; `acks=all` + idempotent üretici (Z8)
- `is/akis_iskelet.py` TODO'ları: pencere, watermark, çıktı; iki akış sorusu
- Watermark deneyi: karttaki oran vs `--gec-orani 0.3`; yeniden başlatma deneyi (`--cikti s3`); teslim garantisi (Z8)
- MongoDB erişim deseni tablosu, veri modeli, shard anahtarı riski (Z6); pano (Z9)

## Rol 3 — Ölçek, veri kalitesi, entegrasyon
- Senaryo kartı → Z1: olay/s × bayt × 86 400 × saklama günü; tepe yük; ×10 / ×100
- Veri sözlüğü, dört kusurdan örnek, kirli veri tablosu, KVKK notu, iki grafik + bulgu cümlesi (Z10)
- Z11 tablosunun derlenmesi, `kanit/` bütünlüğü, README'nin sıfırdan çalıştırılması, rapor birleştirme, teslim kontrol listesi

## Ortak kurallar
- `main`'e doğrudan push yok: dal → PR → başka bir üye inceler → birleştir.
- Her üye kendi bölümünün rapor metnini ve ölçümlerini kendisi yazar.
- Her üye sunumda en az bir bölüm anlatır ve diğer bölümlerin kararlarını da savunabilir.
- Her ölçüm aynı gün `kanit/olcumler.csv`'ye; her YZ kullanımı `docs/yz-kullanim-gunlugu.md`'ye.
