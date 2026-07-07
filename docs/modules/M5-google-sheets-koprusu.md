# M5 · Google Sheets Köprüsü

**Efor:** 18 adam-gün (insan-eşdeğeri) · **Faz:** F3–F5 · **Durum:** Teklif kapsamında

> Ekibin bugünkü çalışma alışkanlığını (Google Sheets) korur: sistemdeki veriler Sheets'te canlı görünür, yetkili girişler Sheets üzerinden sisteme akar. "Yazılıma geçtik ama kimse kullanmıyor" riskine karşı köprü.

## Neden var? (iş değeri)

Saha ve muhasebe ekipleri yıllardır tabloyla çalışıyor; bu teklifin canlı raporu bile aynı desenle (Sheets → web) çalışıyor. M5, geçişi dayatmak yerine kademelendirir: okuma anında, yazma kontrollü. Böylece ürün ilk günden ekibin mevcut aracının içinde yaşar.

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | Okuma köprüsü | Sistem verilerinin (fark tabloları, kota durumu, parametreler) Sheets'e periyodik yayını (≤ 5 dk gecikme) | 5 |
| 2 | Yazma akışı | Sheets'teki kontrollü giriş alanlarından (ör. aylık SPEK, hakediş) sisteme doğrulamalı alım; hatalı satır raporu | 6 |
| 3 | Kimlik + kota yönetimi | Servis kimliği, oran sınırlama (rate limit), yeniden deneme; hangi sayfa/aralık yetkili tanımı | 4 |
| 4 | Test + izleme | Senkron gecikmesi ve hata oranı ölçümü; kopukluk uyarısı | 3 |
| **Toplam** | | | **18** |

## Girdiler → Çıktılar

- **Girdi:** Yetkilendirilmiş Google e-tablo kimlikleri ve alan eşlemeleri.
- **Çıktı:** Çift yönlü, doğrulamalı, izlenebilir Sheets entegrasyonu; kullanıcı eğitim notu.

## Kabul kriterleri

- Okuma gecikmesi ≤ 5 dk; yazmada hata oranı < %1 ve her ret gerekçeli.
- Sheets erişimi kesildiğinde sistem çalışmaya devam eder (köprü "görüntü katmanı"dır, veri sahibi sistemdir).

## Bağımlılıklar ve varsayımlar

- Google Workspace/hesap yetkilendirmesini müşteri sağlar (Apps Script dağıtımı veya servis hesabı paylaşımı).
- Excel'in makrosuz olması korunur; köprü Sheets tarafında çalışır.
