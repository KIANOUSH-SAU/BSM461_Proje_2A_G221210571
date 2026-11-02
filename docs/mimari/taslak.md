# Z0 — Mimari taslak

*Taslak (Adım 5). "?" olan yerler ilgili katman kurulup ölçülünce doldurulur; Adım 15'te son hâli.*

```mermaid
flowchart LR
    A["Olay kaynağı<br/>uretici.py --sablon iot<br/>200 sensör"] -->|canlı| K["Kuyruk<br/>Kafka 4.0 KRaft<br/>konu: sensorler"]
    A -->|--toplu| H["Ham depolama<br/>SeaweedFS S3<br/>s3://ham/iot/tarih=…/"]
    K --> S["Akış işleme<br/>Spark 3.5 Structured Streaming<br/>pencere + watermark"]
    H --> B["Toplu işleme<br/>Spark 3.5 + Delta Lake<br/>temizle → join sensorler.csv → topla"]
    B --> T["Tablolar<br/>Delta @ s3://tablolar"]
    S --> M["Servis deposu<br/>MongoDB ?"]
    T --> M
    M --> P["Sunum<br/>pano ?"]
    S -.-> C["checkpoint"]
```

## Garanti tablosu

| Ok | Kaç kopya? | Sıra garantisi? | Ağ bölünürse? | Kit sadeleştirmesi → üretimde |
|---|---|---|---|---|
| Üretici → Kafka | ? | ? (anahtar başına bölüm içinde) | ? | tek düğüm, RF=1 → 3 düğüm, `min.insync.replicas=2` |
| Kafka → Spark Streaming | ? | ? | ? | ? |
| Üretici → S3 (toplu) | ? | — | ? | tek SeaweedFS düğümü → ? |
| S3 → Spark Batch → Delta | ? | — | ? | ? |
| Spark → MongoDB | ? | ? | ? | tek düğüm → replica set |
| MongoDB → Pano | ? | — | ? | ? |

Sürümler kitin `docker-compose.yml`'inden yazılacak (tahmin edilmeyecek).
