# M0 · Çekirdek Altyapı & CI (zorunlu)

**Efor:** 20 adam-gün (insan-eşdeğeri) · **Faz:** F2–F3 · **Durum:** Zorunlu — kapsamdan çıkarılamaz

> Ürünün üzerinde koşacağı zemin: sunucu ortamları, kalite kapıları ve iskelet uygulama. Bu modül olmadan hiçbir modül üretime çıkamaz.

## Neden var? (iş değeri)

Tamamen vibecoding ile geliştirilen bir üründe güvence, koddan değil kapılardan gelir: AI'ın yazdığı her satır, testlerden ve güvenlik taramalarından geçmeden birleştirilemez. M0, bu disiplinin otomatik altyapısını kurar ve "tek geliştirici" riskini (bus factor 1) kurulumun 2 saatte tekrarlanabilir olmasıyla dengeler.

## Alt bileşenler

| # | Bileşen | Ne yapar? | Efor (a-g) |
|---|---------|-----------|-----------:|
| 1 | Depo + CI kalite kapıları | GitHub deposu, korumalı main; her PR'da lint, tip kontrolü, test, sır taraması (gitleaks), bağımlılık denetimi (pip-audit) | 6 |
| 2 | Docker ortamları | Hetzner (Debian) üzerinde staging + prod; Traefik ile TLS; imaj bazlı sürümleme; S3 uyumlu gecelik yedek | 6 |
| 3 | İskelet uygulama + kimlik | Python framework v16 üzerinde `hakedis_core` app iskeleti; token/OAuth2 kimlik; rol iskeleti | 5 |
| 4 | Güvenlik taraması + sır yönetimi | SAST (bandit), bilinmeyen paket kontrolü (slopsquatting önlemi), ortam değişkeni/sır hijyeni | 3 |
| **Toplam** | | | **20** |

## Girdiler → Çıktılar

- **Girdi:** Sunucu erişimi (Hetzner), GitHub organizasyon/depo yetkisi, alan adı.
- **Çıktı:** Çalışan staging + prod ortamı; yeşil CI hattı; sıfırdan kurulum runbook'u (≤ 2 saat).

## Kabul kriterleri

- PR kapıları: lint/tip/test/sır/bağımlılık kontrollerinin tamamı otomatik koşuyor; kırmızıyken birleştirme engelli.
- Yedekten geri dönüş tatbikatı başarılı (RPO ≤ 24 sa, RTO ≤ 4 sa kanıtı).
- Temiz makinede runbook ile kurulum ≤ 2 saat.

## Bağımlılıklar ve varsayımlar

- Barındırma müşteri sunucusundadır; bulut hesabı açılması gerekmez.
- AI ajanları yalnız dalda çalışır; main'e doğrudan yazamaz (insan onayı zorunlu).
