# M4 · Mevzuat parametre yönetimi

**Efor:** 15 adam-gün · **Faz:** F3 · **Durum:** Teklif kapsamında.

**Katman:** MVP · Faz 1 — müşteri Excel'i + SGK Genelge 2026/16. Güncel oran/birim-maliyet/dönem tabloları (Genelge değerleri) MVP'dir; çünkü doğru hesap bu tablosuz olmaz. Geçmiş hesabı kendi dönemine sabitleyen "dönem kilidi/snapshot" Faz 2 · Gap'tir (bkz. [gap-analizi](../gap-analizi.md)).

> Excel'in formüllerine gömülü bütün sabitleri — 6,75; 0,345; 0,375; 38,5; 18.200; 26.005,50 — tek bir düzenlenebilir tabloya taşır. Yeni tebliğ çıktığında güncelleme, on beş dakikalık bir form işlemi olur.

## Bu modül hangi işi devralıyor?

Müşterinin Excel'inde mevzuat değerleri formüllerin içine yazılmış durumda. "Çarpı 6,75 bölü 100" ifadesi yüzlerce hücrede tekrar ediyor. Eksiğin lira karşılığı bir sayfada 0,345 ile, başka sayfada 0,375 ile, bir başkasında 38,5 ile çarpılıyor; üçü birden doğru olamaz ve bugün üçü de günceldışı. Asgari ücret hücresinde hâlâ 2025 değeri (26.005,50) duruyor. Birim fiyat, "2025/1 varsayımı" notuyla 18.200'e sabitlenmiş. Bir kural değiştiğinde birinin bütün sayfaları elden geçirmesi gerekiyor ve bir hücre hep unutuluyor. Bu modül, bu değerlerin tamamını kaynağıyla birlikte tek tabloya taşır. Formüller değeri tablodan okur. Geçmiş hesaplar, kendi dönemlerinin değerine kilitli kalır; bugünkü güncelleme dünkü hesabı değiştiremez.

## Excel'deki karşılığı, hücre hücre

| Bugün Excel'de | Ne yapıyor? | Üründe nasıl olacak? |
|---|---|---|
| Yüzlerce hücrede "×6,75/100" | İşçilik oranı formüllere gömülü; tebliğ değişirse hepsini elle bulmak gerekiyor. | Oran, iş koluna göre tek tablodan gelecek. Tebliğ değişince tek satır güncellenecek. |
| Z sütunu ×0,345 · İCMAL D22 ×0,375 · PRİME ESAS D68 ×38,5 | Aynı kavram üç sayfada üç farklı çarpanla hesaplanıyor; üçü de eski. | Tek dönemsel oran tablosu olacak: Eylül 2024'e kadar yüzde 34,5; sonrasında 34,75; 2026'dan itibaren 35,75. Hesap, tarihine bakıp doğru oranı kendisi seçecek. |
| İCMAL D11: 26.005,50 | 2025 asgari ücreti elle yazılmış; 2026'da güncellenmemiş. | Asgari ücret dönem tablosunda duracak (2026: 33.030,00). Kota hesabı doğru değeri kendisi alacak. |
| RUHSAT B5: 18.200 "2025/1 varsayımı" | Birim fiyat tek yıla sabitlenmiş. | Yıl ve yapı sınıfına göre tam tablo olacak; kaynak olarak Resmî Gazete tarihi ve sayısı yazacak. |

## Kullanıcı hikâyeleri

- **SGK uzmanı olarak**, yeni tebliğ çıktığında değerleri kendim güncellemek istiyorum. Böylece geliştirici beklemem ve hesaplar hiç eskimez.
- **Genel müdür olarak**, geçmiş bir hesabın o günkü resmî değerle yapıldığının kanıtını görmek istiyorum. Böylece denetimde "sonradan mı değiştirdiniz" şüphesi hiç doğmaz.
- **Mali işler yöneticisi olarak**, hangi dönemde hangi oranın geçerli olduğunu tek tablodan görmek istiyorum. Böylece üç sayfada üç farklı çarpan kâbusu bir daha yaşanmaz.

## Kullanım yolculuğu

1. Resmî Gazete'de yeni tebliğ yayımlanır. SGK uzmanı "parametre güncelle" formunu açar.
2. Uzman yeni değerleri girer; kaynak alanına Resmî Gazete tarihini ve sayısını yazar.
3. Sistem yayınlamadan önce önizleme gösterir: hangi değer neyden neye değişecek. Uzman onaylar.
4. Yeni hesaplar yeni değeri kullanır. Geçmiş hesaplar kendi dönemlerinin değerinde kilitli kalır.
5. Denetçi sorduğunda uzman geçmişi açar: hangi değer, ne zaman, kim tarafından, hangi dayanakla girilmiş — hepsi ekranda.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Parametre tabloları | Üç tabloyu kurar: yıl ve sınıfa göre birim fiyatlar, iş koluna göre oranlar, döneme göre asgari ücret ve prim oranları. Her satır kaynağıyla durur. | 5 |
| 2 | Dönem kilidi ve sürümleme | Her değerin geçerlilik aralığını tutar. Hesapları, yapıldıkları andaki değer setine bağlar. | 4 |
| 3 | Hızlı güncelleme formu | Tek form ve dosya yüklemeyle güncellemeyi on beş dakikanın altına indirir; önizleme gösterir. | 3 |
| 4 | Doğrulama test paketi | Dönem seçimini ve "güncelleme geçmişi bozmaz" kuralını her sürümde yeniden sınar. | 3 |
| **Toplam** | | | **15** |

## Kabul kriterleri

- Yeni bir tebliğin girilmesi, baştan sona on beş dakikayı geçmemelidir.
- Güncellemeden sonra geçmiş dönem hesapları, yeniden açıldığında aynı kalmalıdır.

## Mevzuat dayanağı

Yıllık birim maliyet tebliğleri · Oran tebliği · 7524 ve 7566 sayılı Kanunlar · SGK Genelgesi 2026/16.
