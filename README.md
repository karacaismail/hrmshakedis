# hrmshakedis — Asgari İşçilik & Hakediş Uyum Platformu (Yazılım Geliştirme Projesi)

İnşaat firması için özel geliştirilen headless SGK uyum ürününün **codebase'i**: yazılım geliştirme teklifi, waterfall proje planı, modül kapsam sözleşmeleri ve canlı C-level raporu.

**Canlı rapor:** https://karacaismail.github.io/hrmshakedis/ · **Teklif formu (A4):** https://karacaismail.github.io/hrmshakedis/teklif.html
**Veri kaynağı (tek):** Google Sheets çalışma kitabı — https://docs.google.com/spreadsheets/d/1VXwPEh-eEIYXqRpxRO3MoN3cib-R5jBjkNRU-GPJIYw/edit

## Depo yapısı

```
hrmshakedis/
├── index.html                  # C-level canlı rapor (Tailwind + ECharts + Phosphor, min 1rem, Roboto)
├── teklif.html                 # Yazılım Geliştirme Teklif Formu — canlı, A4 yazdırılabilir
├── docs/
│   ├── data-map.md             # SÖZLEŞME: Sheets hücresi → WEB_PARAM → web bileşeni haritası + bakım kuralları
│   ├── gap-analizi.md          # Kapsam üç katman: MVP (Excel+Genelge) · Faz 2 Gap · Enterprise
│   ├── guides/
│   │   ├── yonetici-kilavuzu.md   # Yazılım tarafını işleten kişi için
│   │   └── musteri-kilavuzu.md    # İnşaat firması temsilcileri için (teknik bilgi gerektirmez)
│   ├── modules/                # Modül kapsam sözleşmeleri (rapor kartlarındaki modallar buradan beslenir)
│   │   ├── M0-cekirdek-altyapi.md
│   │   ├── M1-ruhsat-hesap-motoru.md
│   │   ├── M2-ihale-hesabi.md
│   │   ├── M3-hakedis-izleme-kota.md
│   │   ├── M4-mevzuat-parametre.md
│   │   ├── M5-google-sheets-koprusu.md
│   │   └── M6-denetim-raporlari-kvkk.md
│   └── setup/
│       └── google-sheets-mcp.md  # Sheets'i Claude'dan canlı düzenleme (Zapier kurulu; alternatif yollar)
└── tools/
    └── build_xlsx.py           # Çalışma kitabı üretici (v5): teklif + waterfall + parametreler + WEB_PARAM + katman
```

## Mimari akış

Google Sheets = tek doğruluk kaynağı (kapsam seçimi, hız modeli, fiyat, mevzuat parametreleri) → `WEB_PARAM` sayfası tüm değerleri **metin protokolüyle** dışa verir (gviz tip karışması önlemi) → `index.html` ve `teklif.html` her açılışta + 60 sn'de bir okur → grafikler, waterfall zaman çizelgesi ve teklif kendini günceller. Modül kartına tıklanınca ilgili `docs/modules/*.md` dosyası modal içinde açılır (alt bileşenler + efor kırılımı + kabul kriterleri).

## Kapsam katmanı (MVP · Faz 2 Gap · Enterprise)

Kapsam üç katmandır; katman ataması Google Sheets `TEKLİF GİRDİ` F sütununda (MVP/GAP/ENT) canlıdır, `WEB_PARAM` bunu web raporuna taşır ve rapor üç grubu ayrı gösterir. **MVP (Faz 1)** = müşterinin Excel'i + SGK Genelge 2026/16 çekirdek hesabı (M1–M4, 90 adam-gün). **Faz 2 · Gap** = Excel'de/Genelge'de olmayan iyileştirmeler; ayrı modül M5 (18 a-g) + M1–M4'e gömülü kesişen kalemler (giriş denetimi, düzeltme kalemleme, iş akışı durumları, dönem kilidi). **Enterprise** = M0 çekirdek altyapı & CI + M6 KVKK/denetim raporları (45 a-g). Ayrıntı: `docs/gap-analizi.md`.

## Hız (velocity) modeli

Tamamen vibecoding: AI kodu ultra hızlı yazar, insan doğrular. Takvim çarpanı = Amdahl oranı × ECA kuralları ÷ geliştirici sayısı (lineer). Varsayılan: 153 adam-gün × 0,550 = 84 gün. Parametreler Sheets `PARAMETRELER` sayfasındadır; değişince plan ve web otomatik ölçeklenir.

## Geliştirme

Rutin değer değişiklikleri Sheets üzerinden yapılır (elle veya Claude + Zapier becerisi "hrmshakedis sheet güncelle" ile hücre-hücre canlı). Çalışma kitabını YAPISAL değişiklikte yeniden üretmek için: `python3 tools/build_xlsx.py` → Sheets'e **Dosya > İçe aktar > E-tabloyu değiştir** → index.html içindeki FB yedek nesnesini eşitle. Hangi bilginin nereden aktığı ve isim değişikliği prosedürü için: `docs/data-map.md`.

## Notlar

- Müşteri adı ticari gizlilik gereği "İnşaat firması" olarak anonimleştirilmiştir.
- Rapor bilgilendirme amaçlıdır; resmî SGK hesabı yerine geçmez.
