# Yönetici Kılavuzu — hrmshakedis Sistemini İşletmek

Bu kılavuz, yazılım tarafını yöneten kişi içindir. Sistemin parçalarını, günlük işlemleri ve bozulmayı önleyen kuralları anlatır. Müşteriye verilecek sade kılavuz ayrıdır: `musteri-kilavuzu.md`.

## Sistem üç parçadan oluşur

1. **Google Sheets çalışma kitabı** — bütün değişken değerlerin evi: kapsam seçimi, hız modeli, fiyat, tarihler, mevzuat parametreleri. Adres tektir ve değişmez: docs.google.com/spreadsheets/d/1VXwPEh-eEIYXqRpxRO3MoN3cib-R5jBjkNRU-GPJIYw
2. **GitHub deposu** — anlatının evi: web sayfaları, modül detay dokümanları, kılavuzlar ve çalışma kitabını üreten betik. github.com/karacaismail/hrmshakedis
3. **GitHub Pages** — müşterinin gördüğü yüzey: canlı rapor (index.html) ve A4 teklif formu (teklif.html). Sayfalar, Sheets'i her açılışta ve 60 saniyede bir okur.

Hangi bilginin nereden aktığının tam listesi `docs/data-map.md` dosyasındadır. Tereddütte önce oraya bakın.

## Günlük işlemler (Sheets üzerinden, kod gerektirmez)

Aşağıdaki işlemlerin hepsini iki yolla yapabilirsiniz: Sheets'i elle düzenleyerek veya Claude'a söyleyerek (Zapier bağlantısı kuruludur; "hrmshakedis sheet güncelle" becerisi hangi hücrelerin güvenli olduğunu bilir).

| İstediğiniz şey | Değiştireceğiniz yer | Sonuç |
|---|---|---|
| Geliştirici sayısını 3 yapmak | PARAMETRELER B5 | Takvim üçe bölünür; fazlar, GA ve web anında yeniden hesaplanır |
| AI hız varsayımını değiştirmek | PARAMETRELER B6 (hız), B7 (pay) | Amdahl oranı ve çarpan güncellenir |
| Bir ECA kuralını açmak ("mevzuat değişti → yavaşla") | PARAMETRELER B12:B16'da ilgili satırı EVET yapmak | Çarpan ve bütün tarihler otomatik esner |
| Kapsamdan modül çıkarmak/eklemek | TEKLİF GİRDİ C14:C20 (EVET/HAYIR) | Efor, süre, bedel ve teklif formu anında değişir |
| Günlük ücreti veya başlangıç tarihini değiştirmek | PARAMETRELER B38 / B33 | Bedel ve plan güncellenir |
| Teklif kimliğini değiştirmek (no, tarih, geçerlilik, hazırlayan) | TEKLİF GİRDİ C5:C10 | Teklif formu ve webdeki ticari özet güncellenir |

Doğrulama alışkanlığı: değişiklikten sonra raporu açın; sağ üstteki nokta yeşil ve "Sheets canlı" olmalı, durum satırındaki "Sheets kaydı" saati ilerlemeli.

## Dikkat: modül adı değiştirmek üç adımlık iştir

1. Sheets'te iki aralığı birlikte ve birebir aynı yazın: TEKLİF GİRDİ B14:B20 ve PARAMETRELER A21:A27. Tek tarafı değiştirirseniz efor kolonu #N/A olur.
2. Depoda ilgili `docs/modules/*.md` dosyasının başlığını aynı ada çekin (modal başlığıyla kart adı aynı kalsın).
3. `tools/build_xlsx.py` içindeki mods[] ve mod_ef[] listelerini aynı ada eşitleyin. Bu yapılmazsa betik bir gün çalıştırıldığında Sheets'i eski adlara döndürür.

## Anlatı değişiklikleri (depo üzerinden)

Modül detayları (`docs/modules/`), statik web metinleri, risk kartları, kabul kriterleri ve kılavuzlar depodadır. Düzenleyin, `main` dalına gönderin; Pages bir dakika içinde yayınlar. İki metin çifttir ve birlikte güncellenir: kabul kriterleri/varsayımlar hem index.html'de hem teklif.html'de geçer.

## Yapısal değişiklik (yeni sayfa, yeni satır düzeni)

Sheets'in iskeletini değiştirecekseniz kaynak, `tools/build_xlsx.py` betiğidir: betiği güncelleyin, `python3 tools/build_xlsx.py` ile dosyayı üretin, formülleri yeniden hesaplatıp sıfır hata görün ve Sheets'te **Dosya > İçe aktar > E-tabloyu değiştir** ile aynı adrese yükleyin. Ardından index.html içindeki FB (statik yedek) nesnesini yeni değerlerle eşitleyin. WEB_PARAM'a ekleyeceğiniz her satır metin protokolüne uymalıdır (`=""&…`, tarihler `TEXT(…,"yyyy-mm-dd")`); aksi hâlde web alanları boş düşer.

## Sorun giderme

- **Rapor "STATİK" rozetine düştü:** Sheets'e ulaşılamıyor veya WEB_PARAM bozuldu. Sheets'in "bağlantıya sahip herkes" paylaşımını ve WEB_PARAM sayfasının varlığını kontrol edin.
- **Efor kolonunda #N/A:** modül adı iki aralıkta farklı yazılmış. İki aralığı birebir eşitleyin.
- **Teklif alanları "—":** TEKLİF GİRDİ hücreleri boş veya WEB_PARAM TEKLIF satırları silinmiş.
- **Webde eski rakam görünüyor ama Sheets doğru:** tarayıcı 60 saniyeyi beklememiş olabilir; sekmeye dönünce kendini yeniler. Kalıcıysa FB yedeğine bakın.

## Güvenlik notları

Yazma erişimi Zapier üzerinden sizin Google onayınızla çalışır; beceri, formül alanlarına ve yıkıcı aksiyonlara kapalıdır. GitHub yazması repo token'ıyla yapılır; token'ı yalnız gerektiğinde üretin ve işiniz bitince iptal edin. Ürün yüzeylerinde gerçek müşteri adı ve teknoloji markaları geçmez ("İnşaat firması", "Python framework").
