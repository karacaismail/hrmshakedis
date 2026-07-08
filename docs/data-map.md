# Veri Akış Haritası — Sheets hücresi → WEB_PARAM → Web bileşeni

Bu belge, sistemin sözleşmesidir: hangi veri nerede doğar, nereden geçer, ekranda nereye düşer ve kim, nasıl günceller. Paralel denetimle (07.07.2026) doğrulanmıştır.

## Zincirin tamamı

```
Google Sheets (girdi hücreleri)  →  WEB_PARAM sayfası (tümü metin protokolü)  →  gviz JSON  →  index.html / teklif.html (60 sn'de bir + sekmeye dönüşte)
GitHub deposu (docs/modules/*.md) →  modül kartı modalları
GitHub deposu (index/teklif içindeki sabit bloklar) →  statik bölümler (repo push ister)
```

Kural: bir bilgi ya Sheets'ten gelir (canlı) ya depodan gelir (statik). İkisinden birden gelmez; gelirse çelişki doğar.

## 1) Canlı alanlar: üretim → tüketim

| Sheets kaynağı (girdi) | WEB_PARAM satırı | index.html hedefi | teklif.html hedefi |
|---|---|---|---|
| PARAMETRELER B5 (geliştirici) | KV dev | Hero #kDev · Hız #vDev · #whatif vurgusu | — |
| PARAMETRELER B6, B7 (AI hızı, payı) | KV ai_hiz, ai_pay | Hız #vAi #vPay | — |
| PARAMETRELER B8 (formül) | KV amdahl | Hız #vAmdahl | — |
| PARAMETRELER B12:C16 (ECA) → D17 | KV eca | Hız #vEca | — |
| PARAMETRELER B18 (formül) | KV carpan | Hero #kCarpan · Hız #vCarpan · what-if hesabı | v4 doğrulama anahtarı |
| TEKLİF GİRDİ C14:C20 (EVET/HAYIR) → D22 | KV efor | Hero #kEfor · Kapsam #kEfor2 · Ticari #tEfor · karşılaştırma barı | Ticari #f_efor |
| PARAMETRELER B31 (formül) | KV sure | Hero #kSure · Hız #vGun · bar | #f_sure |
| PARAMETRELER B33 (başlangıç, girdi) | KV baslangic | what-if GA hesabı, faz zinciri yedeği | — |
| WATERFALL PLAN F12 / PARAMETRELER B34-B35 | KV ga, tampon | Hero #kGA · Hız #vGA #vTampon · timeline GA işareti | #f_ga #f_tampon |
| PARAMETRELER B38 (girdi) | KV gunluk_ucret | Ticari #tUcret | #f_ucret |
| PARAMETRELER B39-B41 (formül) | KV bedel, kdv, toplam | Hero #kBedel · Ticari #tBedel #tKdv #tToplam · ödeme yedek hesabı | #f_bedel #f_kdv #f_toplam |
| PARAMETRELER C52, B52 | KV asgari_ucret_2026, fark_prim_2026 | (yedek; görünür kaynak DONEM satırları) | — |
| WEB_PARAM C2, C3 (formül) | KV surum, guncelleme | Footer v-etiketi #vSurum · durum satırı "Sheets kaydı" | — |
| TEKLİF GİRDİ B14:B20 + C + D + E + F (katman) | MODUL ×7 (ad, seçim, efor, açıklama, katman=MVP/GAP/ENT → EK3/F) | Kapsam #modCards üç grup (MVP/Faz 2 Gap/Enterprise) + #katmanOzet + modal | Kapsam bandı #f_kapsam (katman gruplu) |
| WATERFALL PLAN A5:F10 (formül tarihler) | FAZ ×6 (ad, gün, başlangıç, bitiş) | Plan #timeline + #chartFaz | Plan tablosu #f_plan |
| PARAMETRELER A49:C52 (dönem tablosu) | DONEM ×4 | Mevzuat #tblDonem | — |
| PARAMETRELER A55:C62 (maliyet tablosu) | MALIYET ×8 | Mevzuat #chartMaliyet | — |
| TEKLİF GİRDİ C5:C10 → TEKLİF FORMU | TEKLIF ×9 (form_no, tarih, geçerlilik, müşteri, yüklenici, proje, ödeme1-3) | Ticari #tNo #tGecerlilik #tOdeme | Başlık + Taraflar + Ödeme alanları |

Önemli isim kuralı: modül adı değişecekse TEKLİF GİRDİ B14:B20 ile PARAMETRELER A21:A27 **birlikte ve birebir aynı** yazılmalıdır; aksi hâlde D kolonundaki eşleştirme (VLOOKUP) bozulur ve efor #N/A olur.

## 2) Statik bloklar (Sheets'ten güncellenmez; depo push ister)

| Bölüm / blok | Kaynak dosya | Not |
|---|---|---|
| Hero metinleri, 01 Ürün kartları, "İhtiyacın kaynağı" | index.html | Ürün anlatısı değişirse buradan |
| Faz teslimat açıklamaları (timeline altındaki cümleler) | index.html → FAZ_TESLIM sözlüğü | Faz ADLARI Sheets'ten; teslimat METİNLERİ buradan |
| Kabul kriterleri (4 madde) ve varsayım notu | index.html + teklif.html | İki dosyada da aynı metin; birlikte güncellenir |
| 06 Mevzuat üç yükümlülük kartı + "günceldışı çarpan" notu | index.html | Mevzuat değişirse elden geçirilir |
| 07 Risk kartları (5 adet) + unk-unk notu | index.html → RISKS dizisi | |
| Kaynakça bağlantıları | index.html footer | |
| Statik yedek veri seti (Sheets'e ulaşılamazsa görünen) | index.html → FB nesnesi | Sheets'te kalıcı değer değişikliğinden sonra FB de eşitlenmeli (bkz. bakım kuralı 3) |
| Modül detayları (modal içerikleri) | docs/modules/M0…M6.md | Kart adları Sheets'ten, detaylar depodan; kod öneki (M0…M6) eşleştirir |
| Teklif formundaki kabul/varsayım/hariçler ve imza bloğu | teklif.html | |

## 3) Güncelleme yolları (kim, neyi, nasıl)

| Değişiklik | Yol | Araç |
|---|---|---|
| Sayısal parametre (geliştirici, AI hızı, ücret, tarih, kapsam EVET/HAYIR, kimlik) | Sheets'te ilgili girdi hücresi | Elle veya Claude + Zapier becerisi "hrmshakedis sheet güncelle" |
| Modül adı/açıklaması | İki aralık birlikte: GİRDİ B/E + PARAMETRELER A | Zapier becerisi (tek batchUpdate) |
| Modül katmanı (MVP/GAP/ENT) | TEKLİF GİRDİ F14:F20 girdi; WEB_PARAM F23:F29 formülle çeker | Zapier becerisi (batchUpdate) |
| Modül detay metni (modal) | docs/modules/*.md düzenle | Depo push (Pages ~1 dk'da yayınlar) |
| Statik web metni, risk kartı, kabul kriteri | index.html / teklif.html | Depo push |
| Yapısal değişiklik (yeni sayfa, yeni satır düzeni, yeni modül satırı) | tools/build_xlsx.py güncelle → xlsx üret → Sheets'e "E-tabloyu değiştir" ile içe aktar → FB'yi eşitle | Depo + içe aktarma |

## 4) Bakım kuralları

1. **Tek doğruluk kaynağı:** değerler Sheets'te, anlatı depoda. Bir değeri asla web metnine gömme; kv'den bağla.
2. **İsim değişikliği prosedürü:** GİRDİ B + PARAMETRELER A birlikte → md H1 aynı ada çekilir → tools/build_xlsx.py mods[] ve mod_ef[] eşitlenir. Üçü de yapılmadan iş bitmiş sayılmaz.
3. **FB eşitleme:** Sheets'te kalıcı bir değer değiştiyse (ör. bedel, tarihler), index.html içindeki FB yedek nesnesi de aynı değere çekilir; yoksa Sheets erişilemediği gün eski rakam görünür.
4. **Metin protokolü:** WEB_PARAM'a eklenecek her yeni satır metin olarak dışa verilir (`=""&…` veya `TEXT(…,"yyyy-mm-dd")`); aksi hâlde gviz kolon tipini bozar ve alanlar boş düşer.
5. **Yasaklı kelimeler:** ürün yüzeylerinde teknoloji markası ve gerçek müşteri adı geçmez ("Python framework", "İnşaat firması" kullanılır).
6. **Katman boyutu:** modül katmanı TEKLİF GİRDİ F sütununda (MVP/GAP/ENT); WEB_PARAM EK3 (F) formülle çeker; index.html/teklif.html `c[5]` olarak okur; build_xlsx.py `mods[]` 4. elemanı ve index.html `FB.modul` `m[4]` ile senkron kalır. Katman anlamları ve gap kalemleri: `docs/gap-analizi.md`.
