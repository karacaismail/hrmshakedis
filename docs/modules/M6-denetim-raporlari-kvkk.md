# M6 · Denetim Raporları + KVKK/RBAC

**Efor:** 25 adam-gün (insan-eşdeğeri) · **Faz:** F4–F6 · **Durum:** Teklif kapsamında

> Ürünü "hesap makinesi"nden **kurumsal uyum sistemine** çeviren katman: kim neyi görebilir (RBAC), kişisel veri nasıl korunur (KVKK), denetçiye ne sunulur (4 hazır rapor + denetim izi).

## Neden var? (iş değeri)

Bugünkü tabloda kişi adları, vergi/kimlik numaraları ve ücret verileri korumasız dolaşıyor — KVKK riski. SGK denetiminde ise soru hep aynıdır: "Bu tutara nasıl ulaştınız, kim, ne zaman, hangi parametreyle?" M6 bu iki soruyu ürün özelliği yapar: erişim rol bazlı ve maskeli; her hesap, girdi anlık görüntüsüyle saklı; denetim dosyası tek tuşla PDF.

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | RBAC + maskeleme | 4 rol (Yönetici, SGK Uzmanı, Şantiye, Salt-Okur); kişisel alanlar (kimlik, ücret) varsayılan maskeli; izin matrisi testli | 8 |
| 2 | Denetim izi ekranı | Kim-neyi-ne zaman değiştirdi; hesap snapshot geçmişi; örnek denetim sorusuna ≤ 2 dk'da yanıt | 5 |
| 3 | 4 denetim raporu (PDF) | İşyeri özeti · taşeron dökümü · dönem farkları · kesinti listesi; her biri ≤ 30 sn'de üretim | 8 |
| 4 | KVKK paketi | Veri envanteri ve saklama süreleri, aydınlatma metni taslağı, sızıntı müdahale runbook'u; erişim logu | 4 |
| **Toplam** | | | **25** |

## Girdiler → Çıktılar

- **Girdi:** Rol-kişi eşlemesi (müşteriden), rapor şablon onayları.
- **Çıktı:** Yetki matrisi canlı; denetime hazır rapor seti; KVKK dokümantasyonu.

## Kabul kriterleri

- İzin matrisi testleri yeşil; maskesiz veri yalnız yetkili rolde.
- 4 rapor gerçek pilot verisiyle ≤ 30 sn; denetim izi sorusu ≤ 2 dk.

## Bağımlılıklar ve varsayımlar

- M0'ın kimlik altyapısı üzerine kurulur; raporlar M1–M3 verilerini kullanır.
- KVKK hukuki görüşü (metinlerin onayı) müşteri tarafındadır; taslakları biz üretiriz.
