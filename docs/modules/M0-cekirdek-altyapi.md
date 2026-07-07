# M0 · Çekirdek Altyapı & CI (zorunlu)

**Efor:** 20 adam-gün · **Faz:** F2–F3 · **Durum:** Zorunlu modül. Kapsamdan çıkarılamaz.

> Bu modül, ürünün üzerinde çalışacağı güvenli zemini kurar. Excel'in hiç sahip olmadığı şeyleri ekler: yedeklilik, kalite kontrolü ve kurulumun tekrarlanabilir olması.

## Bu modül hangi işi devralıyor?

Bu modülün Excel'de bir karşılığı yok; sorun da tam olarak bu. Bugün bütün iş tek bir dosyada yaşıyor. O dosya bozulursa, silinirse veya yanlış sürümü e-postayla dolaşırsa, iş durur. Kimse "bu dosyanın dünkü hâli neydi" sorusuna cevap veremez. Bu modül, işi tek dosyanın kaderinden kurtarır: sistem iki ayrı ortamda çalışır, her gece kendini yedekler ve yapay zekânın yazdığı hiçbir kod, otomatik kontrollerden geçmeden ürüne giremez.

## Kullanıcı hikâyeleri

- **Genel müdür olarak**, yapay zekânın yazdığı kodun denetimsiz şekilde ürüne girmediğinden emin olmak istiyorum. Böylece hız kazanırken güvenlikten vazgeçmediğimizi bilirim.
- **Geliştirici olarak**, her kod değişikliğinin testlerden ve güvenlik taramalarından kendiliğinden geçmesini istiyorum. Böylece hatalı kod, ben fark etmeden kapıda durdurulur.
- **Mali işler yöneticisi olarak**, sistemin tek bir kişiye bağımlı olmamasını istiyorum. Böylece o kişi yarın ayrılsa bile sistemi bir başkası iki saatte kurabilir.

## Kullanım yolculuğu

1. Geliştirici, yapay zekâ ajanına bir özellik yazdırır. Ajan kodu ayrı bir dalda hazırlar ve birleştirme isteği açar.
2. Sistem bu isteği kendiliğinden sınar. Testleri koşar, kod kalitesine bakar, şifre sızıntısı arar ve kullanılan paketlerin gerçek olduğunu doğrular.
3. Bütün kontroller yeşilse geliştirici değişikliği onaylar. Tek bir kontrol kırmızıysa kod ürüne giremez.
4. Onaylanan kod önce deneme ortamına çıkar. Orada sorun görülmezse geliştirici onu tek tuşla gerçek ortama alır.
5. Sistem her gece kendini yedekler. Ekip ayda bir, yedekten geri dönme provası yapar. Böylece "yedek varmış ama çalışmıyormuş" sürprizi hiç yaşanmaz.

## Alt bileşenler ve efor

| # | Bileşen | Bu bileşen ne yapar? | Efor (a-g) |
|---|---------|----------------------|-----------:|
| 1 | Kod deposu ve kalite kapıları | Kodun tek adresini kurar. Ana dalı korumaya alır. Her değişiklikte testleri, kalite kontrolünü, sır taramasını ve paket denetimini kendiliğinden çalıştırır. | 6 |
| 2 | Sunucu ortamları | Müşterinin sunucusunda deneme ve gerçek ortamlarını kurar. Güvenli bağlantıyı ayarlar. Gecelik yedekleri dış depoya yazar. | 6 |
| 3 | İskelet uygulama ve kimlik | Ürünün boş ama çalışan ilk hâlini ayağa kaldırır. Kullanıcı girişini ve rol altyapısını hazırlar. | 5 |
| 4 | Güvenlik taraması ve sır yönetimi | Kodu bilinen açıklara karşı tarar. Yapay zekânın uydurabileceği sahte paket adlarını yakalar. Şifrelerin koda yazılmasını engeller. | 3 |
| **Toplam** | | | **20** |

## Kabul kriterleri

- Kırmızı bir kontrol varken kodu ana dala birleştirmek teknik olarak mümkün olmamalıdır.
- Yedekten geri dönüş provası başarılmalıdır: en fazla bir günlük veri kaybı, en fazla dört saatte ayağa kalkış.
- Projeyi hiç bilmeyen bir kişi, rehberi izleyerek sistemi temiz bir sunucuya iki saat içinde kurabilmelidir.
