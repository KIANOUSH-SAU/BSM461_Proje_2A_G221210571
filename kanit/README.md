# kanit/

| Dosya | Ne | Adım |
|---|---|---|
| `ortam.png` | `dogrula.sh --tam` çıktısının ekran görüntüsü | 2 |
| `senaryo.txt` | `senaryo.py --grup <kod> --sablon iot` çıktısı | 3 |
| `olcumler.csv` | Bütün ölçümler — ne, kaç kez, sonuç, birim | 4–14 |
| `explain-*.txt` | `explain(mode="formatted")` çıktıları | 8 |
| `spark-ui-*.png` | Spark UI: aşamalar, görev süresi dağılımı | 8 |
| `kirilma-deneyi.*` | Z11 deney günlükleri / ekran görüntüleri | 14 |

**Kural:** Raporda geçen her sayı `olcumler.csv`'de olmalı. Ölçülmemiş sayı yazılmaz.

`olcumler.csv` sütunları: `tarih, uye, bilesen (Z2…), olcum, deger, birim, tekrar, veri_boyutu, makine, komut_veya_not, kanit_dosyasi`
