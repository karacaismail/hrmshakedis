# M3 · Hakediş İzleme + Adam-Ay Kota

**Efor:** 30 adam-gün (insan-eşdeğeri) · **Faz:** F3–F4 · **Durum:** Teklif kapsamında — en büyük modül

> Müşterinin bugün Excel'de elle yürüttüğü işin ürünleşmiş hâli: taşeron bazında aylık hakediş ↔ bildirilen SPEK karşılaştırması, eksikte kesinti önerisi ve **adam-ay kotası** uyarıları.

## Neden var? (iş değeri)

Eksik bildirim iş bittiğinde fark prim + gecikme cezası olarak döner; alt-taşeronun eksiği sözleşme gereği ana yüklenicinin hakedişinden kesilir. Bugün bu takip tek Excel'de, kırık başvurularla ve ayda bir elle yapılıyor. M3 her ay otomatik sorar: "Bu taşeron bu ay yeterli SPEK bildirdi mi; bildirmediyse hakedişinden ne kadar karşılık ayırmalıyız; sahada en az kaç işçi görünmeliydi?"

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | Taşeron sicili + hiyerarşi | Firma, vergi no, SGK taşeron kodu, üst taşeron bağı; evrak durumu (teminat, vekaletname, İSG, şantiye şefi) | 5 |
| 2 | SPEK matrisi içe aktarma | Aylık bildirilen SPEK verisinin CSV/ekran kopyasından doğrulamalı alımı; reddedilen satır listesi; mutabakat raporu | 7 |
| 3 | Fark/kesinti motoru | Kümülatif hakediş × indirimli oran − bildirilen SPEK = fark; dönem prim oranıyla kesinti/karşılık önerisi | 6 |
| 4 | Adam-ay kota + eşik uyarıları | Fark ÷ dönem asgari ücreti = adam-ay açığı; proje bazlı eşikler; ihlalde e-posta/webhook uyarısı | 6 |
| 5 | Test paketi | Kota çevrimi (K1: 3,5M ÷ 33.030 = 106 adam-ay), fazla bildirimde UYUMLU durumu, dönem oranı seçimi | 4 |
| 6 | İzleme ekranı | Etap × dönem ısı görünümü; taşeron risk sıralaması | 2 |
| **Toplam** | | | **30** |

## Girdiler → Çıktılar

- **Girdi:** Taşeron listesi, aylık hakedişler (KDV hariç), aylık bildirilen SPEK, oranlar.
- **Çıktı:** Taşeron/dönem bazlı fark tablosu, kesinti önerileri, kota ihlal uyarıları, denetime hazır izleme kaydı.

## Kabul kriterleri

- Pilot mutabakatı: müşterinin mevcut tablosunun toplamlarıyla açıklanamayan fark 0.
- Örnek ihlalde uyarı e-postası ≤ 5 dk içinde düşer; yanlış alarm oranı < %5.

## Bağımlılıklar ve varsayımlar

- SGK'nın halka açık API'si yoktur; bildirilen SPEK verisi müşteriden CSV/ekran ile gelir (M5 köprüsü bu akışı kolaylaştırır).
- Adam-ay çevrimi resmî SGK hesabı değildir; yönetim/kota aracıdır ve raporlarda böyle etiketlenir.

## Mevzuat dayanağı

5510 md. 88/90 (hakedişten kesinti, borcu yoktur kontrolü) · SGK Genelgesi 2011/13 böl. 3 · 2026/16 §3.1
