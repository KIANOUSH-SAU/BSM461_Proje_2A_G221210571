# Proje durumu

*Son güncelleme: 2 Kasım 2026*

## Yapıldı
- [x] Şablon seçimi: **Şablon 3 — IoT** (kesin)
- [x] Yönerge (27 s.) incelendi; gereksinimler `CLAUDE.md` ve bu klasöre aktarıldı
- [x] Yerel depo iskeleti: README taslağı, `.gitignore`, `kanit/olcumler.csv` başlığı, planlama belgeleri

## Bekleyen — engelleyici
- [ ] **Şube** ve **grup kodu** (üç üyenin öğrenci numarasından en küçüğü) → depo adı `BSM461_Proje_<şube>_<grupkodu>`
- [ ] Diğer iki üyenin **GitHub kullanıcı adları** (collaborator eklemek için)
- [ ] Hocanın **`kit/` başlangıç arşivi** (SABIS / ders sayfası) → `kit/` içine
- [ ] **Docker Desktop** kurulumu (bu makinede yok); Docker'a ≥ 5 GB bellek

## Sırada (engeller kalkınca)
1. GitHub'da public depoyu aç, üyeleri ekle, bu iskeleti gönder
2. `kit/`'i depoya koy, `docker compose up -d`, `dogrula.sh --tam` → `kanit/ortam.png`
3. `senaryo.py --grup <kod> --sablon iot` → `kanit/senaryo.txt`
4. Üreticiyi kısa çalıştır → veri sözlüğü, dört kusurdan birer örnek, olay kimliği / tekrar ayıklama stratejisi
5. Z1 hesabı, Z0 ilk taslak (bkz. `docs/mimari/taslak.md`)

## Açık tasarım soruları (senaryo kartı + veriyle cevaplanacak)
- Olaylarda benzersiz kimlik var mı? Yoksa tekrar ayıklama hangi alanlarla? (`sensor_id` + `olay_zamani`?)
- `sensorler.csv`'nin gerçek sütunları (model, kurulum yılı — doğrulanacak)
- Kafka bölüm sayısı ve anahtarı; watermark süresi; pencere türü/boyutu
- Anomali eşiği (statik mi, sensör/model/bölge bazlı mı?); sessizlik zaman aşımı
- Servis sorgusu p99 → MongoDB veri modeli
- MongoDB'ye yazım: `foreachBatch` + idempotent upsert mi, Delta'dan ara aşama mı?
