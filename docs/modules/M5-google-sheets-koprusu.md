# M5 · Google Sheets köprüsü & veri teyidi

**Efor:** 18 adam-gün · **Faz:** F3–F5 · **Durum:** Teklif kapsamında.

**Katman:** Faz 2 · Gap analizi — Excel'de/Genelge'de olmayan; ekibin alıştığı tabloyu koruyan denetimli veri köprüsü ve izlenen teyit. MVP çekirdek hesabı (M1–M4) bu köprü olmadan da çalışır; köprü, veri girişini güvenli ve izlenebilir kılan Faz 2 iyileştirmesidir.

> Excel'deki "MANUEL ELLE YAZILACAK ALAN" etiketlerinin ve "TEYİT EDİLDİ" notlarının işini devralır: ekip alıştığı tabloda çalışmaya devam eder; veriler denetimden geçerek sisteme akar, güncel sonuçlar tabloya geri yazılır.

## Bu modül hangi işi devralıyor?

Müşterinin İCMAL sayfası, veri toplama sürecini kendisi itiraf ediyor. Satır başlarında "MANUEL ELLE YAZILACAK ALAN" yazıyor. Bir satırda "SGK ekranından çekilecek veri" notu var; yani biri her ay kurumun sitesine girip rakamı gözle okuyup elle yazıyor. Yanlarda "TEYİT EDİLDİ", "TEKNİK OFİSTEN İSTENECEK" notları duruyor; teyit süreci, hücre kenarına yazılmış hatırlatmalarla yürüyor. Bu yöntem iki hata üretiyor: rakamlar bazen metin olarak yapışıyor (bir hücrede "234,827,01" yazılmış ve hiçbir toplama girmiyor) ve kimin neyi teyit ettiği belli olmuyor. Bu modül alışkanlığı korur: ekip yine tabloda çalışır. Ama tablodaki giriş alanları denetimlidir; bozuk veri gerekçesiyle geri döner, teyit bir not değil izlenen bir durum olur ve sistemdeki güncel sonuçlar tabloya kendiliğinden yansır.

## Excel'deki karşılığı, hücre hücre

| Bugün Excel'de | Ne yapıyor? | Üründe nasıl olacak? |
|---|---|---|
| İCMAL, A sütunu: "MANUEL ELLE YAZILACAK ALAN" | Hangi hücrenin elle doldurulacağını etiketle hatırlatıyor. | Tabloda ayrılmış giriş alanları olacak; sistem yalnız oraları okuyacak ve her girişi denetleyecek. |
| İCMAL, A9: "SGK ekranından çekilecek veri" | Bildirilen toplamlar, kurum sitesinden gözle okunup elle yazılıyor. | Aynı veri, dosya yüklemeyle toplu alınacak; satır satır doğrulanacak. |
| E4, G4, I5 hücreleri: "TEYİT EDİLDİ", "TEKNİK OFİSTEN İSTENECEK" | Teyit süreci, hücre kenarındaki notlarla yürüyor. | Teyit bir durum alanı olacak: kim, ne zaman, neyi onayladı — kayıtla görünecek. |
| PRİME ESAS, I2: "234,827,01" | Rakam metin olarak yapışmış; hiçbir toplama girmiyor ve kimse fark etmiyor. | Böyle bir giriş kapıda yakalanacak; "bu bir sayı değil" uyarısıyla gerekçeli geri dönecek. |

## Kullanıcı hikâyeleri

- **Muhasebe çalışanı olarak**, yeni bir programın ekranlarını öğrenmeden, her gün kullandığım tablodan çalışmaya devam etmek istiyorum. Böylece işime hiç ara vermem.
- **Şantiye yöneticisi olarak**, tutarları alıştığım tabloya girmek istiyorum; denetimi sistem yapsın. Böylece hız kaybetmem ve bozuk veri içeri sızmaz.
- **Genel müdür olarak**, tabloda gördüğüm rakamla sistemdeki rakamın aynı olduğundan emin olmak istiyorum. Böylece toplantıda herkes aynı sayıyı konuşur.

## Kullanım yolculuğu

1. Muhasebe çalışanı sabah her zamanki tabloyu açar. Dünkü kapanışın sonuçları, sistem tarafından gece yansıtılmış hâlde yerindedir.
2. Şantiyeden yeni tutar gelir. Yönetici, tutarı tablodaki giriş alanına yazar.
3. Sistem girişi birkaç dakika içinde alır ve denetler. Tutar bozuksa veya taşeron tanımsızsa, satır gerekçesiyle "hata" listesine düşer.
4. Kabul edilen veri, tabloda "sistem onayladı" işaretiyle geri görünür. Giriş yapan kişi, verisinin işlendiğini tablodan ayrılmadan görür.
5. Bağlantı koparsa sistem bunu kendisi bildirir ve bağlantı gelince kaldığı yerden eşitler. Veri kaybolmaz.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Okuma köprüsü | Sistemdeki güncel sonuçları, en geç beş dakika arayla tablonun ilgili sayfalarına yazar. | 5 |
| 2 | Denetimli giriş alanları | Tablodaki ayrılmış alanları izler. Her girişi biçim ve tutarlılık denetiminden geçirir; bozuk satırı gerekçesiyle geri verir. | 6 |
| 3 | Teyit akışı | "Teyit edildi" notlarını durum alanına çevirir: kim, ne zaman, neyi onayladı. Eksik teyitleri listeler. | 4 |
| 4 | İzleme ve dayanıklılık | Gecikmeyi ve hata oranını ölçer. Kopuklukta haber verir; bağlantı gelince kendiliğinden eşitler. | 3 |
| **Toplam** | | | **18** |

## Kabul kriterleri

- Sistemdeki bir değişiklik, en geç beş dakika içinde tabloda görünmelidir.
- "234,827,01" gibi bozuk bir giriş sisteme asla işlenmemeli; gerekçeli olarak geri dönmelidir.
- Tabloya erişim kesilse bile sistem çalışmaya devam etmelidir. Tablo görüntü katmanıdır; verinin sahibi sistemdir.
