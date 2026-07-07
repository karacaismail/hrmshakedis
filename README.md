# hrmshakedis — Asgari İşçilik & Hakediş Uyum Platformu

Python tabanlı açık kaynak bir uygulama çatısı üzerinde, tamamen vibecoding ile (AI kodu yazar, insan doğrular) inşa edilen **headless** SGK asgari işçilik ve hakediş uyum ürününün stratejik yol haritası.

**Canlı rapor:** https://karacaismail.github.io/hrmshakedis/
**Canlı teklif formu (A4 yazdırılabilir):** https://karacaismail.github.io/hrmshakedis/teklif.html

## Canlı veri mimarisi

Rapor ve teklif sayfası, projelendirme çalışma kitabının Google Sheets kopyasındaki `WEB_PARAM` sayfasını her açılışta okur (gviz JSON ucu). Sheets'te değişen her şey — geliştirici sayısı, AI hız çarpanı, ECA velocity kuralları, sprint tarihleri, mevzuat parametreleri, teklif formu girdileri — sayfa yenilendiğinde web'e yansır. Tek veri kaynağı bu Sheets dosyasıdır; çalışma kitabı başka hiçbir yerde yayınlanmaz.

## Sayfalar

- `index.html` — stratejik yol haritası: vizyon/misyon/değerler, kültür, mevzuat çerçevesi (2026/16), mimari, hız (velocity) modeli, SMART hedefler, canlı gantt, MoSCoW backlog, risk + unk-unk çerçevesi, gap analizi, test stratejisi, kaynakça.
- `teklif.html` — koşullara göre kendini ayarlayan hesap/teklif formu çıktısı; ayrı sekmede açılır, A4 yazdırma stilleri hazırdır.

## Teknoloji

Tailwind CSS (CDN) · Apache ECharts 5 · Phosphor Icons · Roboto · mobile-first, taban yazı boyutu 1rem. Derleme adımı yoktur; GitHub Pages doğrudan sunar.

## Notlar

- Müşteri adı ticari gizlilik gereği "İnşaat firması" olarak anonimleştirilmiştir.
- Projelendirme çalışma kitabı (xlsx) müşteri verisi içerdiği için bu depoda yer almaz; yalnız Google Sheets üzerinde yaşar.
- Rapor bilgilendirme amaçlıdır; resmi SGK hesabı yerine geçmez.
