# M6 · Taşeron sicili, raporlar & KVKK

**Efor:** 25 adam-gün · **Faz:** F4–F6 · **Durum:** Teklif kapsamında.

> Excel'deki "TAŞERON 1&2-3 ETAP" sicil sayfasının işini devralır ve iki eksiğini tamamlar: kişisel veriler korumaya alınır, denetçiye verilecek dökümler tek tuşla hazırlanır.

## Bu modül hangi işi devralıyor?

Müşterinin taşeron sicili bugün bir Excel sayfası: her taşeronun SGK kodu, yirmi altı haneli işyeri numarası, vergi numarası, kimin altında çalıştığı, dosyasının açık mı kapalı mı olduğu ve evrak durumu (teminat mektubu, vekâletname, iş güvenliği sorumlusu, şantiye şefi) sütunlarda duruyor. Sayfa işini görüyor; ama iki büyük açığı var. Birincisi: bu sayfada kişi adları, vergi ve kimlik numaraları korumasız duruyor ve dosya e-postayla dolaşıyor. Bu, kişisel verilerin korunması kanunu açısından risktir. İkincisi: SGK denetçisi geldiğinde bu dağınık bilgiden derli toplu bir döküm çıkarmak saatler alıyor. Bu modül sicili sisteme taşır, erişimi rollere bağlar, kişisel alanları maskeler ve dört hazır denetim raporunu yarım dakikada üretir.

## Excel'deki karşılığı, hücre hücre

| Bugün Excel'de | Ne yapıyor? | Üründe nasıl olacak? |
|---|---|---|
| TAŞERON sayfası, A–B sütunları | SGK taşeron kodunu (001, 002…) ve 26 haneli işyeri numarasını elle tutuyor. | Aynı bilgiler kayıt alanı olacak; biçim denetimiyle yanlış numara girilemeyecek. |
| C sütunu: "Osman Camcı", "Elif İnşaat" | Alt-taşeronun kimin altında çalıştığını serbest metinle tutuyor. | Bu ilişki tanımlı bağ olacak ve M3'teki "bildirimi üste say" kuralını besleyecek. |
| J sütunu: "AKTİF", "KAPALI DOSYA" | Dosya durumunu elle yazılmış etiketle izliyor. | Durum, tarihli bir alan olacak; kapanan dosyanın geçmişi korunacak. |
| K–P sütunları: dilekçe, teminat, vekâletname, İSG, şantiye şefi | Evrak takibi "VAR / KAPALI / GEREK YOK" notlarıyla yürüyor. | Her evrak, durumu ve tarihiyle izlenecek; eksik evrak listesi tek tıkla alınacak. |
| Aynı sayfadaki kişi adları ve vergi numaraları | Kişisel veriler korumasız; dosyayı alan herkes hepsini görüyor. | Kişisel alanlar varsayılan olarak maskeli olacak; maskesiz görüntüleme yalnız yetkili role açık ve kayıtlı olacak. |

## Kullanıcı hikâyeleri

- **Genel müdür olarak**, SGK denetçisi geldiğinde istediği dökümü dakikalar içinde vermek istiyorum. Böylece denetim günü kriz günü olmaktan çıkar.
- **İnsan kaynakları sorumlusu olarak**, kişisel verileri yalnız yetkili kişilerin görmesini istiyorum. Böylece kanuni yükümlülüğümüzü fiilen yerine getiririz.
- **Şantiye yöneticisi olarak**, yalnız kendi projemin taşeronlarını görmek istiyorum. Böylece bilgi, ihtiyacı olanda kalır.
- **SGK uzmanı olarak**, evrakı eksik taşeronları tek listede görmek istiyorum. Böylece hakediş gününden önce eksikleri tamamlatırım.

## Kullanım yolculuğu

1. Sistem yöneticisi, ekipteki herkese dört rolden birini verir: Yönetici, SGK Uzmanı, Şantiye, Salt-Okur.
2. Şantiye yöneticisi girer; yalnız kendi projesini görür. Kimlik ve vergi numaraları onun ekranında yıldızlıdır.
3. SGK uzmanı "eksik evrak" listesini açar; hangi taşeronun teminatı veya vekâletnamesi eksikse tek ekranda görür.
4. Denetim günü uzman "denetim paketi" düğmesine basar. Dört rapor — işyeri özeti, taşeron dökümü, dönem farkları, kesinti listesi — yarım dakikada PDF olur.
5. Denetçi eski bir hesabı sorar. Uzman kaydı açar: girdiler, kullanılan resmî değerler, tarih ve işlemi yapan kişi ekrandadır; hiçbiri sonradan değiştirilemez.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Taşeron sicili ve evrak takibi | Sicildeki bütün sütunları kayda taşır: kodlar, işyeri numarası, hiyerarşi, dosya durumu ve evrak durumları. Eksik evrak listesini üretir. | 7 |
| 2 | Rol bazlı erişim ve maskeleme | Dört rolü ve izin matrisini kurar. Kişisel alanları varsayılan maskeler; maskesiz görüntülemeyi kayda geçirir. | 6 |
| 3 | Dört denetim raporu | İşyeri özeti, taşeron dökümü, dönem farkları ve kesinti listesini kurumsal şablonla, yarım dakikanın altında PDF üretir. | 8 |
| 4 | KVKK paketi | Veri envanterini, saklama sürelerini, aydınlatma metni taslağını ve sızıntı müdahale planını hazırlar; erişim kayıtlarını raporlanabilir yapar. | 4 |
| **Toplam** | | | **25** |

## Kabul kriterleri

- Hiçbir rol, tanımı dışındaki veriyi görememelidir; izin matrisi testlerden geçmelidir.
- Dört rapor, gerçek pilot verisiyle otuz saniyenin altında üretilmelidir.
- Örnek bir denetim sorusu, iki dakika içinde ekrandan belgeyle yanıtlanabilmelidir.
