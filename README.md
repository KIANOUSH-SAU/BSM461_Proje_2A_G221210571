# BSM461_Proje_2A_G221210571 — IoT Sensör İzleme ve Anomali Tespit Sistemi

> ⚠️ **Taslak.** Bu README, kurulum adımları gerçekten denenip doğrulandıkça doldurulur. Aşağıdaki komutlar yönergeden alınmıştır; `kit/README.md` geldiğinde gerçek hâliyle güncellenecek.

BSM 461 Büyük Veriye Giriş (2026–2027 Güz) dönem projesi — **Şablon 3: IoT sensör telemetrisi ve anomali**.
200 sensörün sıcaklık / nem / titreşim olaylarını Kafka + Spark Structured Streaming ile canlı, S3 (SeaweedFS) + Spark + Delta Lake ile toplu işleyen; anomalileri ve susan sensörleri yakalayan bir hat.

| | |
|---|---|
| Grup kodu | `G221210571` |
| Şube | `2A` |
| Üyeler | `<ad soyad — no>` × 3 |
| Teslim commit'i | `git rev-parse teslim` → *(teslimde yazılacak)* |

## Sorular

| Tür | Soru |
|---|---|
| Akış 1 | Hangi sensör son *N* dakikada normalin dışına çıktı? |
| Akış 2 | Hangi sensör sustu (beklenen sürede olay göndermedi)? |
| Toplu 1 | Bölge bazında sıcaklık/nem/titreşim günlük desenleri nasıl? |
| Toplu 2 | Hangi sensör modellerinde anomali daha sık? (`sensorler.csv` join) |

*N*, anomali eşiği ve sessizlik süresi senaryo kartından (`kanit/senaryo.txt`) gerekçelendirilecek.

## Sıfırdan çalıştırma

Gereksinim: Docker Desktop, Docker'a ≥ 5 GB bellek.

```bash
git clone https://github.com/KIANOUSH-SAU/BSM461_Proje_2A_G221210571.git
cd BSM461_Proje_2A_G221210571/kit

docker compose up -d
./dogrula.sh --tam                       # Windows PowerShell: aşağıdaki iki komut
# docker compose exec araclar python araclar/dogrula.py
# docker compose exec spark spark-submit is/dogrula_spark.py

# Toplu veri (aynı grup kodu → aynı veri)
docker compose exec araclar python araclar/uretici.py --grup G221210571 --sablon iot --toplu
docker compose exec spark spark-submit is/toplu_is.py --sablon iot

# Akış
docker compose exec araclar python araclar/uretici.py --grup G221210571 --sablon iot --hiz 5
docker compose exec spark spark-submit is/akis_iskelet.py --sablon iot

# Servis deposu (MongoDB)
docker compose --profile servis up -d
```

## Depo düzeni

```
kit/        başlangıç kiti (docker-compose.yml, araclar/, is/) — kitten türetilir
analiz/     Python analiz ve grafik betikleri
kanit/      ortam.png, senaryo.txt, olcumler.csv, explain-*.txt, spark-ui-*.png, kirilma-deneyi.*
docs/       mimari, görev dağılımı, takvim, test/kırılma planı, YZ kullanım günlüğü
```

`docker-compose.yml`'de kite göre yapılan her değişiklik burada listelenecek.

## Yapay zekâ kullanımı

Bkz. `docs/yz-kullanim-gunlugu.md` (raporun Z12 bölümü buradan derlenir).
