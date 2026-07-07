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
│   ├── modules/                # Modül kapsam sözleşmeleri (rapor kartlarındaki modallar buradan beslenir)
│   │   ├── M0-cekirdek-altyapi.md
│   │   ├── M1-ruhsat-hesap-motoru.md
│   │   ├── M2-ihale-hesabi.md
│   │   ├── M3-hakedis-izleme-kota.md
│   │   ├── M4-mevzuat-parametre.md
│   │   ├── M5-google-sheets-koprusu.md
│   │   └── M6-denetim-raporlari-kvkk.md
│   └── setup/
│       └── google-sheets-mcp.md  # Sheets'i Claude'dan canlı düzenleme: 4 kurulum yolu
└── tools/
    └── build_xlsx.py           # Çalışma kitabı üretici (v4): teklif + waterfall + parametreler + WEB_PARAM
```

## Mimari akış

Google Sheets = tek doğruluk kaynağı (kapsam seçimi, hız modeli, fiyat, mevzuat parametreleri) → `WEB_PARAM` sayfası tüm değerleri **metin protokolüyle** dışa verir (gviz tip karışması önlemi) → `index.html` ve `teklif.html` her açılışta + 60 sn'de bir okur → grafikler, waterfall zaman çizelgesi ve teklif kendini günceller. Modül kartına tıklanınca ilgili `docs/modules/*.md` dosyası modal içinde açılır (alt bileşenler + efor kırılımı + kabul kriterleri).

## Hız (velocity) modeli

Tamamen vibecoding: AI kodu ultra hızlı yazar, insan doğrular. Takvim çarpanı = Amdahl oranı × ECA kuralları ÷ geliştirici sayısı (lineer). Varsayılan: 153 adam-gün × 0,550 = 84 gün. Parametreler Sheets `PARAMETRELER` sayfasındadır; değişince plan ve web otomatik ölçeklenir.

## Geliştirme

Çalışma kitabını yeniden üretmek için: `python3 tools/build_xlsx.py` (çıktı: `hrmshakedis_projelendirme_v4.xlsx`; Sheets'e **Dosya > İçe aktar > E-tabloyu değiştir** ile yüklenir). Sheets'i Claude üzerinden hücre-hücre canlı düzenlemek için `docs/setup/google-sheets-mcp.md` rehberindeki bir yolu bir kez kurun; sonrası delta güncellemedir.

## Notlar

- Müşteri adı ticari gizlilik gereği "İnşaat firması" olarak anonimleştirilmiştir.
- Rapor bilgilendirme amaçlıdır; resmî SGK hesabı yerine geçmez.
