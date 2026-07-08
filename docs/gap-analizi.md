# Faz 2 · Gap Analizi — Excel + Genelge MVP'sinin dışında kalanlar

Bu belge ürünün kapsamını üç katmana ayırır ve **Faz 2 · Gap** katmanını ayrıntılandırır. Tek cümlelik amacı: "MVP tam olarak neyi kapsıyor, neyi kapsamıyor" sorusunu net yanıtlamaktır. Katman ataması Google Sheets `TEKLİF GİRDİ!F14:F20` hücrelerinde (MVP/GAP/ENT) canlıdır; `WEB_PARAM` bunu web raporuna taşır ve rapor üç grubu ayrı gösterir.

## Üç katman

**MVP · Faz 1.** Kapsam = müşterinin Excel'i + SGK Genelge 2026/16. Aracın, bugün Excel'in yaptığı ruhsat/ihale/hakediş hesabını güncel mevzuatla doğru yapması. Modüller: M1, M2, M3, M4 — toplam 90 adam-gün.

**Faz 2 · Gap.** Excel'de ve Genelge'de olmayan ama olması gereken iyileştirmeler. Ayrı izlenen modül M5 (18 adam-gün) ile M1–M4'ün içine gömülü kesişen kalemlerden oluşur.

**Enterprise.** Excel'in hiç sahip olmadığı kurumsal katman. Modüller: M0 (20) + M6 (25) = 45 adam-gün.

## MVP sınırı: neyi kapsar, neyi kapsamaz

MVP **ne yapar:** ruhsattan (alan × birim maliyet × oran, yıllara sâri işte aritmetik ortalama), ihaleden (istihkak/sözleşme bazlı hesap + Genelge'nin getirdiği kısmi araştırma) ve hakedişten (taşeron bazında aylık SPEK, İcmal, adam-ay kota) beklenen asgari işçiliği hesaplar. Bütün oranları döneme göre resmi tablodan seçer (2026 için %6,75 işçilik, %35,75 fark prim); eski 0,345/0,375/0,385 çarpanlarını kullanmaz.

MVP **ne yapmaz:** girişleri denetlemez (yalnız doğru formülle hesaplar), düzeltmeleri ayrı kalem tutmaz, iş akışı durumu izlemez, geçmiş hesabı kendi dönemine kilitlemez, tabloyla çift yönlü köprü kurmaz. Bu dört madde Faz 2'dir.

## Faz 2 · Gap kalemleri

Aşağıdaki kalemler, Excel'i güncel Genelge ile birebir taşısak bile elde edemeyeceğimiz; hesabı güvenli, dayanıklı ve izlenebilir kılan iyileştirmelerdir. Kaynak modülleri, Excel'de neden bulunmadıkları ve ne getirdikleri:

| Gap kalemi | Kaynak modül | Excel/Genelge'de neden yok | Ne getirir |
|---|---|---|---|
| Giriş denetimi | M1 · M2 · M3 | Excel yanlış tür veriye izin verir; bir maliyet hücresinde 4,3 milyar liralık hakediş toplamı duruyor | Hatalı girişi kapıda durdurur; "bu bir sayı değil" gibi gerekçeyle geri döndürür |
| Düzeltmelerin kalemlenmesi | M3 | Düzeltmeler formülün içine gömülü ("=1.034.940,72+25.524,64"); kalemin adı yok | Her düzeltme açıklamasıyla ayrı kalem olur; ay toplamı bu kalemlerden oluşur |
| Kırık bağların onarımı + etap bağımsızlığı | M2 · M3 | Etap-2 hücreleri silinmiş sayfaya bağlı, "#REF!" veriyor; etap aylardır hesaplanamıyor | Etaplar kayıt olur; bir etabı silmek diğerinin hesabını bozamaz |
| Alt-taşeron kuralının tanımlanması | M3 | İlişki formüle elle işlenmiş ("=SUM(L6:AR6)+O7"); kural hiçbir yerde yazmıyor | "Bu firmanın bildirimi şu firmaya sayılır" tanımlı bir kural olur |
| İş akışı durumları | M3 | Süreç serbest metin notlarla yürüyor ("HAKEDİŞ İSTE", "KESİLECEK") | Notlar izlenen durum alanına döner; adımlar takip edilebilir |
| Dönem kilidi / snapshot | M4 | Hesabın "o gün hangi değerle yapıldığı" kaydı yok | Geçmiş hesap kendi dönemine kilitlenir; bugünkü güncelleme dünkü hesabı değiştiremez |
| Denetimli veri köprüsü + izlenen teyit | M5 (ayrı modül) | "MANUEL ELLE YAZILACAK ALAN" ve "TEYİT EDİLDİ" hücre kenarına yazılı notlar | Denetimli giriş alanları, teyit bir durum (kim/ne zaman/neyi), dosya yüklemeyle toplu alma |

## Efor ve fazlama notu

MVP modülleri M1–M4'ün taban eforu (90 adam-gün) hem çekirdek hesabı hem yukarıdaki gömülü iyileştirmeleri kapsar; kesişen kalemler ayrı fiyatlanmaz, ilgili modülle birlikte teslim edilir. Ayrı bir modül olarak izlenen tek Faz 2 kalemi M5'tir (18 adam-gün). Bu ayrım, "önce Excel + Genelge çekirdeğini doğru kur, sonra çevresini güçlendir" sırasını korumak içindir; MVP çekirdek hesabı M5 köprüsü olmadan da doğru sonuç üretir.

## Enterprise katmanı (özet)

Bu katman çekirdek hesaptan bağımsızdır; ürünün kurumsal seviyede güvenli ve uyumlu çalışması içindir.

M0 · Çekirdek altyapı & CI, Excel'in hiç yapamadığını ekler: yedeklilik, kalite kapıları (CI = kod gönderildiğinde testleri otomatik çalıştıran süreç), iki saatte kurulabilirlik ve güvenlik taraması. Teknik olarak zorunludur.

M6 · Taşeron sicili, raporlar & KVKK, sicilin kendisini Excel'den devralır; üstüne KVKK maskeleme, rol bazlı erişim (RBAC) ve dört denetim raporunu (PDF) ekler. Sicil çekirdeği MVP'ye yakın olsa da, kişisel veri koruması ve raporlar Excel'in hiç sahip olmadığı kurumsal katmandır.

## Kaynak ve bakım

Katman değerleri tek doğruluk kaynağında, `TEKLİF GİRDİ!F14:F20` girdi hücrelerinde tutulur (Zapier "hrmshakedis sheet güncelle" becerisiyle canlı düzenlenebilir). `WEB_PARAM!F23:F29` bu değeri metin protokolüyle web'e verir. Modül ayrıntıları: `docs/modules/M0…M6.md`. Kapsam→web akışı: `docs/data-map.md`.
