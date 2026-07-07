# M3 · Aylık Bildirim Matrisi, İcmal Paneli ve Adam-Ay Kota

**Efor:** 30 adam-gün · **Faz:** F3–F4 · **Durum:** Teklif kapsamında. En kapsamlı modül budur; çünkü Excel'in kalbi burasıdır.

> Excel'deki "ASGARİ İŞÇİLİK 1&2 ETAP" matrisinin ve "İCMAL" panelinin işini devralır: her taşeron her ay yeterli bildirim yaptı mı, eksiği kaç lira, hakedişinden ne kesilmeli ve sahada kaç işçi eksik?

## Bu modül hangi işi devralıyor?

Excel'in en büyük sayfası, taşeron başına bir satır ve ay başına bir sütun olan dev bir matristir: Mayıs 2023'ten Ocak 2026'ya, kırktan fazla firma. Her satırda aynı zincir kurulu: kümülatif hakedişin yüzde 6,75'i "olması gereken"; ayların toplamı "bildirilen"; ikisinin farkı çarpı 0,345 "hakedişten kesilecek tutar". Bu zincir çalışıyor; ama üç kırılganlığı var. Birincisi, düzeltmeler formül içine gömülü: bir ay hücresinde "=1.034.940,72+25.524,64" gibi toplamalar duruyor ve kimse hangi kalemin ne olduğunu bilmiyor. İkincisi, alt-taşeron ilişkileri formüllere elle işlenmiş: bir satırın toplamına, başka bir satırın hücreleri eklenmiş; çünkü alt-taşeronun bildirimi üst firmanın hesabına sayılıyor. Bu kural hiçbir yerde yazmıyor; formülün içinde saklı. Üçüncüsü, "İCMAL" panelindeki kritik alanlar elle: kalan adam/ay değeri klavyeyle yazılmış ve iki etabın özeti kopuk bağlar yüzünden hesaplanamıyor. Bu modül aynı matrisi ve paneli kurar; ama düzeltmeler kalem olur, istisna kuralları tanım olur, panel kendini hesaplar.

## Excel'deki karşılığı, hücre hücre

| Bugün Excel'de | Ne yapıyor? | Üründe nasıl olacak? |
|---|---|---|
| ASGARİ İŞÇİLİK 1&2, K sütunu | Kümülatif hakedişi 6,75/100 ile çarpıp "gereken" tutarı buluyor. | Aynı hesap; oran sabit değil, dönem tablosundan gelecek. |
| Ay hücreleri, örneğin M3: "=1034940,72+25524,64" | Düzeltme kalemleri formülün içine gömülmüş; kalemlerin adı yok. | Her düzeltme, açıklamasıyla ayrı kalem olacak; ay toplamı bu kalemlerden oluşacak. |
| AS6 hücresi: "=SUM(L6:AR6)+O7" | Alt-taşeronun (7. satır) bildirimi, üst firmanın (6. satır) toplamına elle eklenmiş. | "Bu firmanın bildirimi şu firmaya sayılır" ilişkisi, tanımlı bir kural olacak; formül cambazlığı bitecek. |
| AT ve AU sütunları | Farkı buluyor, 0,345 ile çarpıp kesilecek tutarı yazıyor. | Fark aynı; çarpan dönemin resmî oranı olacak (2026 için 0,3575). |
| AV sütunu: "HAKEDİŞ İSTE", "KESİLECEK" notları | İş akışı, serbest metin notlarla yürüyor. | Bu notlar durum alanı olacak; "hakediş istendi" gibi adımlar izlenebilecek. |
| İCMAL, D10 ve F10: "KALAN ADAM/AY" | Değer elle yazılmış (6945). Kimse nasıl bulunduğunu göremiyor. | Kalan adam/ay, eksik tutar bölü dönemin asgari ücreti olarak kendiliğinden hesaplanacak. |
| İCMAL, D18 ve D19 satırları | Aynı işi iki yöntemle (hakedişe göre, alana göre) hesaplayıp yan yana koyuyor. | Bu akıllıca karşılaştırma korunacak ve üç yönteme çıkarılacak: alan, hakediş, sözleşme. |
| İCMAL, F9 ve H9: "#REF!" | İki etabın "bildirilen" toplamı, silinen sayfaya bağlandığı için hesaplanamıyor. | Etap özetleri kayıtlardan hesaplanacak; kopacak bağ kalmayacak. |

## Kullanıcı hikâyeleri

- **Şantiye yöneticisi olarak**, hangi taşeronun bu ay eksikte olduğunu ay kapanmadan görmek istiyorum. Böylece hakediş ödenmeden önce taşerona düzelttiririm.
- **Mali işler yöneticisi olarak**, her taşeronun hakedişinden ayıracağım karşılığı net bir rakam olarak görmek istiyorum. Böylece ödemeyi doğru tutarla yaparım.
- **Genel müdür olarak**, üç etabın durumunu tek panelde, üç yöntemle karşılaştırılmış hâlde görmek istiyorum. Böylece hangi rakama güveneceğimi toplantıda tartışmam.
- **SGK uzmanı olarak**, bildirim verilerini toplu yüklemek istiyorum. Böylece vaktimi kopyala-yapıştıra değil, farkların takibine harcarım.

## Kullanım yolculuğu

1. SGK uzmanı, ay kapanınca bildirim verilerini tek dosya olarak yükler. Sistem her satırı denetler; bozuk olanları gerekçesiyle geri verir.
2. Sistem, her taşeronun gerekenini ve bildirdiğini karşılaştırır. Alt-taşeron kuralları tanımlıysa, bildirimleri doğru firmaya sayar.
3. Panelde taşeronlar üç renkte dizilir: uyumlu, izlenecek, kritik.
4. Kritik eksik oluştuğu anda ilgililere e-posta gider: hangi taşeron, kaç lira eksik, önerilen kesinti ne kadar.
5. Ay sonunda uzman, etap panelini açar: üç yöntemin sonucu yan yana, kalan adam/ay kendiliğinden hesaplanmış hâlde durur. Tek tuşla dönem raporu alınır.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Aylık bildirim matrisi | Taşeron-ay matrisini kayıt olarak tutar. Düzeltmeleri, gömülü formül yerine adlı kalemler olarak alır. | 7 |
| 2 | Alt-taşeron sayım kuralları | "Bu firmanın bildirimi şuna sayılır" ilişkisini tanım hâline getirir ve hesapta otomatik uygular. | 5 |
| 3 | Fark ve kesinti hesaplayıcı | Taşeron bazında farkı bulur; dönemin oranıyla çarpıp hakedişten ayrılacak karşılığı önerir. | 6 |
| 4 | İcmal paneli | Etap bazında üç yöntemi yan yana hesaplar; kopmaz bağlarla, kendini güncelleyen tek ekran sunar. | 5 |
| 5 | Adam-ay kota ve uyarılar | Eksiği "kaç işçi" diline çevirir; eşik aşımında kendiliğinden e-posta gönderir. | 4 |
| 6 | Doğrulama ve mutabakat | Sistem toplamlarını, müşterinin mevcut tablosunun toplamlarıyla karşılaştırır; fark sıfırlanana kadar geçiş bitmez. | 3 |
| **Toplam** | | | **30** |

## Kabul kriterleri

- Pilot mutabakatında, sistem ile mevcut tablo arasında açıklanamayan fark kalmamalıdır.
- Alt-taşeron kuralı tanımlandığında, Excel'deki çapraz satır formüllerinin sonuçları birebir yeniden üretilmelidir.
- Örnek bir ihlalde uyarı beş dakika içinde ulaşmalıdır.

## Mevzuat dayanağı

5510 sayılı Kanun, madde 88 ve 90 · SGK Genelgesi 2011/13, bölüm 3 · SGK Genelgesi 2026/16.
