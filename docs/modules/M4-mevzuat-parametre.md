# M4 · Mevzuat Parametre Yönetimi

**Efor:** 15 adam-gün (insan-eşdeğeri) · **Faz:** F3 · **Durum:** Teklif kapsamında

> Mevzuat değerlerini koddan ayırır: birim maliyetler, işçilik oranları ve dönem parametreleri (asgari ücret, fark prim oranı) **veri** olarak yönetilir. Yeni tebliğ → 15 dakikada canlı.

## Neden var? (iş değeri)

Bu alanda en büyük risk mevzuat hızıdır: 2024'te KVSK oranı değişti (%34,5→%34,75), 2026'da MYÖ ve tavan değişti (%35,75; 9 kat), 2026/16 hesap yöntemini değiştirdi. Kural kodda gömülü olursa her değişiklik "yazılım projesi" olur; parametre olursa bir form işlemi. Dönem kilitleme sayesinde geçmiş hesaplar yeni parametreden etkilenmez — denetimde "o gün hangi değer geçerliydi" sorusunun kanıtı hazırdır.

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | Parametre veri nesneleri | Birim maliyet (yıl × sınıf-grup, RG referanslı), AİTK işçilik oranları (tam tebliğ eki), dönem parametreleri (asgari ücret, tavan, fark prim oranı) | 5 |
| 2 | Versiyonlama + dönem kilitleme | Her değerin geçerlilik aralığı ve kaynağı; hesaplar hesap anındaki parametre setine sabitlenir; değişiklik denetim izinde | 4 |
| 3 | Hızlı güncelleme akışı | Tek form + CSV içe aktarma; yayın öncesi fark önizlemesi; hedef: tebliğ → canlı ≤ 15 dk | 3 |
| 4 | Test paketi | Dönem seçimi (P1: 30.04.2025 → %34,75; 15.01.2026 → %35,75), regresyon: parametre güncellemesi eski hesabı değiştirmez | 3 |
| **Toplam** | | | **15** |

## Girdiler → Çıktılar

- **Girdi:** Resmî Gazete tebliğ/genelge değerleri (elle veya CSV).
- **Çıktı:** Tüm hesap modüllerinin (M1–M3) beslendiği tek doğruluk kaynağı; RG referanslı parametre geçmişi.

## Kabul kriterleri

- Yeni tebliğ girişi uçtan uca ≤ 15 dk; işlem denetim izinde kim/ne zaman ile görünür.
- Regresyon: güncelleme sonrası eski dönem hesapları bit düzeyinde değişmez.

## Bağımlılıklar ve varsayımlar

- Mevzuat izleme otomasyonu (RG takibi) kapsam dışıdır; n8n ile sonradan eklenebilir (uyarı → bu modülün formu).

## Mevzuat dayanağı

Birim maliyet tebliğleri (RG 31.01.2025/32799 · 03.02.2026/33157) · AİTK Oran Tebliği (son değ. RG 22.03.2023/32140) · 7524 ve 7566 sayılı Kanunlar (prim oranı/tavan) · SGK Genelgesi 2026/16
