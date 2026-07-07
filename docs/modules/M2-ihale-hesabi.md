# M2 · İhale Hesabı + Kısmi Araştırma

**Efor:** 20 adam-gün (insan-eşdeğeri) · **Faz:** F3–F4 · **Durum:** Teklif kapsamında

> Kamu ihalesi işlerinde asgari işçiliği **toplam istihkak (KDV hariç) × tebliğ oranı × 0,75** ile hesaplar; 2026/16'nın getirdiği **kısmi araştırma** (ödenen hakediş üzerinden) ve mahsup akışını yönetir.

## Neden var? (iş değeri)

Kesin teminatın iadesi ilişiksizlik belgesine bağlıdır. 2026/16 ile artık toplam istihkak bildirilmeden, ödenen hakediş üzerinden sınırlı araştırma isteme hakkı var — doğru kullanılırsa teminat/nakit akışını aylarca öne çeker. M2 bu hakkı süreçleştirir: hangi tutar üzerinden araştırma yapıldı, ne mahsup edildi, ilişiksizliğe ne kaldı — hepsi izlenir.

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | İstihkak veri modeli | İhale kaydı, idare, sözleşme; istihkak kalemleri (KDV hariç, fiyat farkı dahil ayrımı) | 4 |
| 2 | Kısmi araştırma + mahsup durum makinesi | "Ödenen hakediş üzerinden kısmi hesap → sonradan toplam istihkak bildirimi → önceki tutarın mahsubu → nihai ilişiksizlik" akışı; fesih/yarım kalan iş durumları | 6 |
| 3 | Hesap servisi + API ucu | Gereken SPEK, fark, dönem oranıyla fark prim; ünite araştırması / müfettiş-YMM incelemesi ayrımı (%25 indirim yalnız ünitede) | 4 |
| 4 | Altın senaryo test paketi | Genelge böl. 3.1 örnekleri: I1 (60.812,50 TL), I2 (23.456,25 TL) + müşteri verisi I3 (290.202.405,52 TL) | 4 |
| 5 | Form/rapor bağı | Sonucun teklif/denetim formlarına akışı | 2 |
| **Toplam** | | | **20** |

## Girdiler → Çıktılar

- **Girdi:** İstihkak/ödenen hakediş tutarı, tebliğ oranı, bildirilen SPEK, araştırma tipi (kısmi/nihai).
- **Çıktı:** Fark prim borcu, ilişiksizlik durumu ("kısmi — belge verilmez / nihai — mahsuplu"), kalıcı kayıt.

## Kabul kriterleri

- 3 altın senaryo birebir; kısmi→nihai geçişte mahsup farksız.
- Fazla bildirim senaryosunda fark 0 ve sonraki hesapta mahsup izlenebilir.

## Bağımlılıklar ve varsayımlar

- M4 oran tablolarını sağlar; idarece malzeme verilen işlerde oran AİTK kararıyla elle girilir.

## Mevzuat dayanağı

5510 md. 85 · SSİY md. 110 · AİTK Oran Tebliği (RG 12.05.2010/27579, son değ. 22.03.2023/32140) · SGK Genelgesi 2026/16 §3.1
