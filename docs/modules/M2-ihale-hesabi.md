# M2 · İhale & sözleşme hesabı + kısmi araştırma

**Efor:** 20 adam-gün · **Faz:** F3–F4 · **Durum:** Teklif kapsamında.

**Katman:** MVP · Faz 1 — müşteri Excel'i + SGK Genelge 2026/16. Sözleşme/istihkak hesabı ve Genelge'nin getirdiği kısmi araştırma MVP'dir; kırık Etap-2 bağlarının kalıcı onarımı, mahsup akışının izlenmesi ve giriş denetimi Faz 2 · Gap'tir (bkz. [gap-analizi](../gap-analizi.md)).

> Excel'deki "GENEL HESAPLAMA" sayfasının işini devralır: sözleşme bedeli veya toplam hakediş üzerinden beklenen işçiliği hesaplar. Üstüne, 2026'da gelen yeni hakkı ekler: iş bitmeden, ödenen kısım üzerinden ön hesap.

## Bu modül hangi işi devralıyor?

Excel'in "GENEL HESAPLAMA" sayfası iki soruyu yanıtlıyor. Birincisi: "Toplam hakedişe göre ne bildirmeliydik?" Sayfa, hakediş toplamını 0,0675 ile çarpıyor ve yatırılanla karşılaştırıyor. İkincisi: "Sözleşme bedeline göre ne bildirmeliydik?" Aynı çarpım, bu kez 3 milyar 89 milyon liralık sözleşme bedeli üzerinden yapılıyor. Mantık doğru; ama sayfanın yarısı çalışmıyor: Etap-2 bloğundaki hücreler, silinmiş bir sayfaya bağlandığı için hata veriyor ve iki etabın durumu aylardır görünmüyor. Ayrıca eksiğin lira karşılığı 0,345 ile çarpılıyor; bu çarpan eski. Döviz sözleşmelerde de kur, elle çevrilip yazılmış. Bu modül aynı iki soruyu, kırılmayan bağlarla ve güncel oranlarla yanıtlar; üstüne mevzuatın yeni verdiği "kısmi araştırma" hakkını süreç olarak ekler.

## Excel'deki karşılığı, hücre hücre

| Bugün Excel'de | Ne yapıyor? | Üründe nasıl olacak? |
|---|---|---|
| GENEL HESAPLAMA, B2–B6 satırları | Hakediş toplamını başka sayfadan çekiyor, 0,0675 ile çarpıyor, yatırılanla karşılaştırıyor. | Aynı karşılaştırma yapılacak; veriler kayıttan gelecek, bağ kopması diye bir şey olmayacak. |
| B9–B13 satırları | Sözleşme bedeli üzerinden aynı hesabı kuruyor; eksiği 0,345 ile çarpıyor. | Sözleşme bazlı hesap korunacak. Eksiğin lira karşılığı, dönemin resmî oranıyla çarpılacak. |
| B20–B31 bloğu (Etap-2) | Hücreler "#REF!" hatası veriyor; silinen sayfaya bağlıydı. Etap-2 aylardır hesaplanamıyor. | Etaplar kayıt olarak tutulacak. Bir etabı silmek diğerinin hesabını bozamayacak. |
| İCMAL, D5 ve D6 satırları | Hakedişi iki ayrı seri tutuyor: fiyat farkı dahil ve hariç. | İki seri de alan olarak saklanacak; hesap hangisini kullandığını raporda söyleyecek. |
| PRİME ESAS KAZÇ, E8–E11 hücreleri | Döviz sözleşmelerde kur elle çevrilmiş ("EUR 427.703,97" notu ve yanına lira yazılmış). | Döviz tutar ve kur, tarihli alan olarak kaydedilecek; çevrim kendiliğinden ve izlenebilir olacak. |

## Kullanıcı hikâyeleri

- **Mali işler yöneticisi olarak**, teminatın çözülmesini beklerken parayı boşta tutmak istemiyorum. Kısmi hesap hakkını kullanmak istiyorum. Böylece nakit akışını aylar önce rahatlatırım.
- **SGK uzmanı olarak**, hangi tutar üzerinden hesap yapıldığını ve nelerin mahsup edildiğini adım adım görmek istiyorum. Böylece toplam bedel bildirildiğinde kaldığım yerden devam ederim.
- **Proje yöneticisi olarak**, iş feshedilse bile o güne kadarki ödemeler üzerinden durumu görmek istiyorum. Böylece kapanış görüşmesine hazırlıklı giderim.

## Kullanım yolculuğu

1. SGK uzmanı, ihale işini tanıtır: idare, sözleşme bedeli ve bugüne kadar ödenen hakediş.
2. Uzman hesap tipini seçer. Toplam bedel belliyse "nihai" hesap; henüz belli değilse "kısmi" hesap.
3. Sistem beklenen işçiliği hesaplar, bildirilenle karşılaştırır; farkı ve prim karşılığını gösterir.
4. Kısmi hesapta sistem açıkça uyarır: bu hesapla borç ödenebilir; ama ilişiksizlik belgesi, toplam bedel bildirilince verilir.
5. İdare toplam bedeli bildirdiğinde uzman yalnız yeni tutarı girer. Sistem önceki hesabı kendiliğinden düşer ve kalan üzerinden nihai sonucu üretir.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Sözleşme ve istihkak kayıtları | Her işi idaresi ve bedeliyle kaydeder. Fiyat farkı dahil ve hariç serileri ayrı tutar. Döviz sözleşmelerde tutarı ve kuru tarihli saklar. | 5 |
| 2 | Kısmi hesap ve mahsup akışı | "Ödenenden hesapla, borcu öde, toplam gelince öncekini düş, kalanla bitir" zincirini yönetir. Fesihte o güne kadarki ödemelerle kapanış hesabı yapar. | 6 |
| 3 | Hesap servisi | Beklenen işçiliği ve farkı hesaplar. SGK biriminin incelemesinde oranın dörtte bir indirimli, müfettiş incelemesinde indirimsiz uygulandığını bilir. | 4 |
| 4 | Doğrulama test paketi | Genelgedeki iki örneği ve müşterinin verisinden bir senaryoyu her güncellemede yeniden hesaplar. | 3 |
| 5 | Form ve rapor bağlantısı | Sonuçları teklif formuna ve denetim raporlarına taşır. | 2 |
| **Toplam** | | | **20** |

## Kabul kriterleri

- Üç doğrulama senaryosu kuruşu kuruşuna tutmalıdır.
- Kısmi hesaptan nihai hesaba geçişte mahsup, elle müdahale olmadan doğru düşülmelidir.
- Bir etabın silinmesi veya değişmesi, başka bir etabın hesabını bozamamalıdır.

## Mevzuat dayanağı

5510 sayılı Kanun, madde 85 · Sosyal Sigorta İşlemleri Yönetmeliği, madde 110 · SGK Genelgesi 2026/16, bölüm 3.1.
