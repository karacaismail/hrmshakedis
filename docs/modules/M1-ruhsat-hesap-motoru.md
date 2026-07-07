# M1 · Ruhsat ve Alan Bazlı Hesap

**Efor:** 25 adam-gün · **Faz:** F3–F4 · **Durum:** Teklif kapsamında.

> Excel'deki "RUHSAT HESAPLAMASI" sayfasının işini devralır: inşaatın metrekaresinden ve yapı sınıfından, SGK'nın beklediği asgari işçiliği hesaplar. Aynı işi yapar; ama güncel kuralla, giriş hatasına kapalı ve kanıtlı biçimde.

## Bu modül hangi işi devralıyor?

Müşterinin Excel'inde bu hesap "RUHSAT HESAPLAMASI" sayfasında yapılıyor. Sayfa, üç ruhsatın her biri için aynı zinciri kuruyor: birim fiyat çarpı alan eşittir maliyet; maliyetin yüzde 6,75'i eşittir bildirilmesi gereken tutar; bundan ödenenler düşülünce kalan borç çıkıyor. Zincir doğru; ama üç sorunu var. Birincisi, birim fiyat tek yıla sabitlenmiş (18.200 lira, "2025/1 varsayımı" notuyla); oysa 2026/16 sayılı genelge, yıllara yayılan inşaatlarda yılların ortalamasını istiyor. İkincisi, bir hücreye yanlış türde veri girilebiliyor; nitekim bir maliyet hücresinde, maliyet yerine 4,3 milyar liralık hakediş toplamı duruyor. Üçüncüsü, hesabın "o gün hangi değerle yapıldığı"nın kaydı yok. Bu modül aynı zinciri kurar; ama değerleri resmî tablodan çeker, girişleri denetler ve her hesabı kanıtıyla saklar.

## Excel'deki karşılığı, hücre hücre

| Bugün Excel'de | Ne yapıyor? | Üründe nasıl olacak? |
|---|---|---|
| RUHSAT HESAPLAMASI, B5–D5 hücreleri | 2025 birim fiyatını (18.200 / 17.100) elle tutuyor. | Birim fiyat, yıl ve yapı sınıfına göre resmî tablodan kendiliğinden gelecek. Yıllara yayılan işte ortalama kuralı uygulanacak. |
| B7 hücresi | Maliyet yazılması gereken yere 4.299.294.896,58 liralık hakediş toplamı yazılmış. | Sistem, alan çarpı birim fiyat sonucunu kendisi hesaplayacak. Elle maliyet girilemeyecek; bu hata sınıfı kapanacak. |
| B8–E9 satırları | Maliyeti 0,0675 ile çarpıp gereken tutarı buluyor. | Aynı çarpım yapılacak; ama oran, tebliğ tablosundan dönemine göre seçilecek. |
| A10–E12 satırları | Ana yüklenicinin ve taşeronların ödediklerini elle topluyor, kalanı buluyor. | Ödenenler kayıttan gelecek; kalan kendiliğinden güncellenecek. |
| PRİME ESAS KAZÇ, D68 hücresi | Prim karşılığını yüzde 38,5 ile çarpıyor. Bu çarpan hatalı. | Prim karşılığı, dönemin resmî oranıyla (2026 için yüzde 35,75) hesaplanacak. |

## Kullanıcı hikâyeleri

- **SGK uzmanı olarak**, ruhsat bilgilerini bir kez girmek istiyorum. Böylece birim fiyatı her yıl elle güncellemek zorunda kalmam; sistem doğru yılın değerini kendisi bulur.
- **Mali işler yöneticisi olarak**, eksik bildirimin kaç lira prim borcu doğuracağını iş bitmeden görmek istiyorum. Böylece bütçeye zamanında karşılık koyarım.
- **Genel müdür olarak**, her hesabın hangi resmî değerle yapıldığını görmek istiyorum. Böylece denetimde "bu sayıya nasıl ulaştınız" sorusuna belgeyle cevap veririm.

## Kullanım yolculuğu

1. SGK uzmanı, ruhsattaki üç bilgiyi girer: metrekare, yapı sınıfı, başlangıç ve bitiş yılı.
2. Sistem, ilgili yılların birim fiyatlarını tablosundan bulur. İnşaat birden çok yıla yayıldıysa, bitiş yılı hariç yılların ortalamasını alır.
3. Sistem, bildirilmesi gereken tutarı hesaplar ve bugüne kadar bildirilenin yanına koyar.
4. Ekranda üç sonuç görünür: eksik tutar, bu eksiğin prim borcu karşılığı ve eksiğin kaç işçilik bildirime denk geldiği.
5. Uzman raporu tek tuşla alır. Hesap, girdileriyle birlikte arşivlenir; yıllar sonra bile aynı kanıt yerinde durur.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Ruhsat kaydı ve giriş denetimi | Her ruhsatı ayrı kayıtta tutar. Alan ve sınıf girişlerini denetler; maliyet alanına elle veri girilmesine izin vermez. | 4 |
| 2 | Ortalama maliyet hesaplayıcı | Tek yılda biten işte o yılın fiyatını kullanır. Yıllara yayılan işte, bitiş yılı hariç yılların ortalamasını alır. | 6 |
| 3 | Ödemeler ve kalan takibi | Ana yüklenicinin ve taşeronların bildirimlerini ayrı ayrı izler; kalan yükümlülüğü kendiliğinden günceller. | 4 |
| 4 | Hesap servisi ve kanıt kaydı | Sonuçları hesaplar ve her hesabı, girdilerinin fotoğrafıyla birlikte değiştirilemez şekilde saklar. | 5 |
| 5 | Doğrulama test paketi | Genelgedeki örnekleri ve müşterinin gerçek verisini her güncellemede yeniden hesaplar; tek kuruş sapmada yayını durdurur. | 6 |
| **Toplam** | | | **25** |

## Kabul kriterleri

- Genelgedeki dört örnek ve müşteri verisinden iki senaryo, kuruşu kuruşuna tutmalıdır.
- Parametre tablosu güncellendiğinde, geçmiş hesaplar değişmeden kalmalıdır.

## Mevzuat dayanağı

5510 sayılı Kanun, madde 85 · Sosyal Sigorta İşlemleri Yönetmeliği, madde 111 · SGK Genelgeleri 2011/13 ve 2026/16 · Yıllık birim maliyet tebliğleri.
