# Karbon FPV

FPV yarış ve freestyle drone parçaları satan bir e-ticaret sitesi için arayüz tasarımı. Tek dosyalık, bağımlılıksız statik prototip (`index.html`).

**Canlı:** https://ysfce.github.io/karbon-fpv/

## Ne var

- **Kaydırmalı montaj sahnesi** — ana sayfada pinlenmiş bir sahnede quad gerçek CSS 3D katmanlarıyla üst üste kuruluyor: gövde → motorlar → ESC → uçuş kontrol → VTX → kamera → alıcı & anten → pervaneler → batarya. Sağdaki montaj listesi doldukça kalkış ağırlığı (AUW) ve sepet toplamı canlı olarak akıyor. En sonda kataloğa giden buton ve "bu build'i sepete ekle" seçeneği var.
- **Katalog** — 12 kategori, filtre rayı (kategori, marka, boyut, hücre, stack montaj deseni, stok), sıralama, aktif filtre çipleri, arama.
- **Ürün sayfası** — varyant seçimi, adet, teknik özellik tablosu, uyumluluk listesi, kargo/iade sekmesi, uyumlu ürün önerileri.
- **Sepet çekmecesi** — adet güncelleme, ücretsiz kargo ilerleme çubuğu, `localStorage` ile kalıcılık.
- **Rehber** — sınıf/pervane/motor/KV/batarya/AUW uyumluluk tablosu ve üç adımlı build sırası.

## Tasarım kararları

- Tek taahhütlü koyu dünya: FPV gözlüğünün OSD/telemetri katmanı ve havacılık patlatılmış montaj çizimi.
- Vurgu rengi `#FF5A1F` (hazard turuncu) yalnızca eylem ve aktif katman için; `#3FE0BF` (telemetri turkuazı) yalnızca veri ve stok durumu için.
- Tipografi: Archivo (variable, `wdth` ekseni ile genişletilmiş başlıklar), IBM Plex Sans (gövde), IBM Plex Mono (telemetri, gramaj, fiyat).
- Tüm görseller inline SVG — hiçbir resim dosyası yok, sayfa tek istekte yükleniyor.
- `prefers-reduced-motion`, `prefers-reduced-transparency` ve `prefers-contrast` desteklenir; JavaScript kapalıyken de tüm içerik görünür kalır.

## Shopify eşlemesi

Prototip bir Shopify temasına şu şekilde taşınır:

| Prototipteki bölüm | Shopify karşılığı |
| --- | --- |
| Montaj sahnesi | `sections/build-scroll.liquid` — 9 parça `blocks` ile yönetilir (parça adı, gramaj, ürün referansı) |
| Kategori ızgarası | `sections/collection-list.liquid` |
| Katalog + filtreler | `templates/collection.json` + metafield filtreleri (`montaj_deseni`, `hucre`, `boyut`) |
| Ürün sayfası | `templates/product.json`, varyantlar KV / kapasite / renk olarak |
| Hazır kit "sepete ekle" | çoklu `/cart/add.js` çağrısı |
| Sepet çekmecesi | `snippets/cart-drawer.liquid` + Cart AJAX API |

Ürün verisi `index.html` içindeki `P` dizisinde duruyor; Shopify'a geçerken bu dizi `{{ collection.products }}` döngüsüyle değiştirilir.

## Çalıştırma

Bağımlılık yok. `index.html` dosyasını tarayıcıda açmak yeterli.
