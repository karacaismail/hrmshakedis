# Google Sheets'i Claude'dan Canlı Düzenleme — Kurulum Rehberi

Amaç: "Dosya > İçe aktar" adımını tarihe gömmek. Bağlayıcı kurulunca Claude, mevcut e-tabloyu (ID: `1VXwPEh-...GPJIYw`) hücre-hücre, delta olarak canlı düzenler.

Önemli gerçek: Google yazma yetkisi OAuth ister; onay ekranına yalnız hesap sahibi basabilir. Bu yüzden aşağıdaki her yolda ~2 dakikalık bir "izin ver" adımı sende.

## Yol 1 — Zapier bağlayıcısı (kayıt defterinden, önerildi)

1. Sohbette gönderilen **Zapier → Bağlan** kartına tıkla (veya Ayarlar > Bağlayıcılar > Zapier).
2. Zapier hesabında **Google Sheets** uygulamasını yetkilendir.
3. Zapier MCP araç setine Sheets aksiyonlarını ekle (lookup/update/append row).

Ne yapar: satır bazlı okuma/güncelleme/ekleme — WEB_PARAM ve TEKLİF GİRDİ güncellemeleri için yeterli.
Ne yapmaz: biçimlendirme, sayfa ekleme, serbest hücre aralığı yazma (bunlar için Yol 2/3).

## Yol 2 — Composio Google Sheets (özel bağlayıcı, hücre düzeyi)

1. composio.dev → Google Sheets toolkit → hesap aç, Google OAuth'u tamamla.
2. Sana verilen **MCP sunucu URL'sini** kopyala.
3. Claude > Ayarlar > Bağlayıcılar > **Özel bağlayıcı ekle** → URL'yi yapıştır.

Ne yapar: `values.get/update/append`, sayfa yönetimi — tam hücre/aralık kontrolü.
Rehber: composio.dev/toolkits/googlesheets/framework/claude-cowork

## Yol 3 — Servis hesabı + açık kaynak MCP (enterprise; xing5/mcp-google-sheets veya freema/mcp-gsheets)

1. Google Cloud'da proje aç → **Google Sheets API**'yi etkinleştir.
2. Servis hesabı oluştur → JSON anahtar indir.
3. E-tabloyu servis hesabının e-postasıyla **Düzenleyen** olarak paylaş (tek dosya = dar kapsam, en güvenlisi).
4. Sunucuyu çalıştır: `uvx mcp-google-sheets@latest` (env: `SERVICE_ACCOUNT_PATH`, `DRIVE_FOLDER_ID` ops.) ve Claude'a özel bağlayıcı olarak tanıt.

Ne yapar: kişisel OAuth'suz, denetlenebilir, CI/n8n'den de kullanılabilir yazma.
Ne yapmaz: kurulum en uzun yol budur (~15 dk).

## Yol 4 — n8n bağlayıcısı (senin stack'in; otomasyonla birleşik)

1. Sohbette gönderilen **n8n → Bağlan** kartıyla n8n hesabını bağla.
2. n8n'de Google Sheets credential'ı oluştur (OAuth bir kez).
3. "update-sheet" adında parametreli bir workflow aç (Sheets: update cells).

Ne yapar: Claude `execute_workflow` ile güncellemeyi tetikler; ileride RG izleme/bildirim otomasyonlarıyla aynı yerde yaşar.

## Kurulum sonrası (hangi yol olursa)

Bana "bağlandı" yaz; sıra bende: değişiklikleri **delta** uygularım (yalnız değişen hücreler, Sheets sürüm geçmişi korunur), tam yeniden üretim yalnız yapısal revizyonlarda kalır.
