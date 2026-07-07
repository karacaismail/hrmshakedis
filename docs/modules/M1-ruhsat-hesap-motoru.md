# M1 · Ruhsat Hesap Motoru

**Efor:** 25 adam-gün (insan-eşdeğeri) · **Faz:** F3–F4 · **Durum:** Teklif kapsamında

> Özel bina inşaatlarında SGK'nın aradığı asgari işçiliği, yapı ruhsatındaki bilgilerden kuruş hassasiyetiyle hesaplar: **yüzölçümü × birim maliyet × oran × 0,75**.

## Neden var? (iş değeri)

İlişiksizlik belgesi (SGK'nın "borç kalmadı" yazısı) sürecinin ilk sorusu budur. Genelge 2026/16 birim maliyet kuralını değiştirdi (yıllara sâri işlerde **aritmetik ortalama**, bitiş yılı hariç); mevcut tablolar tek yıl bedeliyle hesapladığı için sonuçlar artık mevzuata aykırı. M1, kuralı parametrik uygular ve her hesabı kanıtıyla saklar.

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | Ruhsat veri modeli | Ruhsat kaydı: yüzölçümü, yapı sınıf-grubu, başlangıç/bitiş, tadilat bağı; çok ruhsatlı dosyada ruhsat başına ayrı hesap (2026/16 §5) | 4 |
| 2 | Birim maliyet ortalama motoru | Tek yılda biten işte bitiş yılı bedeli; yıllara sâri işte bitiş yılı hariç yılların aritmetik ortalaması; yıl içinde birden çok tebliğ varsa sonuncusu | 6 |
| 3 | Hesap servisi + API ucu | Gereken SPEK, fark SPEK, dönem prim oranıyla fark prim, adam-ay eşdeğeri; girdi-çıktı anlık görüntüsü (snapshot) ile denetim izi | 5 |
| 4 | Altın senaryo test paketi | Genelge örnekleri (R1: 13.866,67 · R2: 182.250 · R3: 6.318.000) + müşteri verisi (R4: 295.567.947,68) + kenar durumlar (tek yıl, tescilsiz işte %25 indirimsiz) her sürümde otomatik koşar | 6 |
| 5 | Sonuç ekranı + form bağı | Hesap sonucunun ekranda ve A4 teklif/rapor formunda gösterimi | 4 |
| **Toplam** | | | **25** |

## Girdiler → Çıktılar

- **Girdi:** Ruhsat bilgileri (m², sınıf-grup, tarihler), bildirilen toplam SPEK, tahakkuk dönemi.
- **Çıktı:** Bildirilmesi gereken SPEK, fark SPEK, fark prim borcu, adam-ay eşdeğeri; kalıcı hesap kaydı.

## Kabul kriterleri

- 6 altın senaryoda birebir sonuç; sapma < 0,01 TL.
- Aynı girdiyle tekrar hesap: sonuç değişmez; parametre güncellemesi eski hesapları etkilemez (dönem kilitleme).

## Bağımlılıklar ve varsayımlar

- M4 (parametre yönetimi) birim maliyet ve oran tablolarını sağlar.
- Tadilatla sınıf değişimi çok satırlı ortalamayla desteklenir (Genelge Örnek-2).

## Mevzuat dayanağı

5510 sayılı Kanun md. 85 · SSİY md. 111 (değ. RG 16.05.2026/33255) · SGK Genelgesi 2011/13 + 2026/16 · Birim maliyet tebliğleri (RG 31.01.2025/32799, RG 03.02.2026/33157)
