# Ürün fotoğrafları

Bu klasöre kendi ürün çekimlerinizi (ya da distribütörünüzün size kullanım
hakkı verdiği medya kitini) koyun. Site bunları otomatik alır — kod
değiştirmenize gerek yok.

## Nasıl çalışır

1. Fotoğrafları bu klasöre koyun. Adlandırma serbest, ama ürün kodunu
   kullanmak en pratiği:  `b2-1.jpg`, `b2-2.jpg`, `b2-3.jpg` …
2. `index.json` dosyasına ürün kodunu ve dosyalarını yazın:

```json
{
  "b1": ["b1-1.jpg", "b1-2.jpg"],
  "b2": ["b2-1.jpg", "b2-2.jpg", "b2-3.jpg", "b2-4.jpg"],
  "b9": ["b9-1.jpg"]
}
```

3. Kaydedin. Fotoğrafı olan ürünlerde katalog kartı, sepet ve ürün
   sayfası galerisi artık 3D render yerine bu fotoğrafları gösterir.
   Fotoğrafı olmayan ürünler render'da kalır — karışık kullanabilirsiniz.

Ürün sayfası galerisi en fazla 4 fotoğraf gösterir. Tam adres de
yazabilirsiniz (`https://cdn.magazaniz.com/...`); `http` ile başlamayan
her şey bu klasöre göre çözülür.

## Ürün kodları

Kodları `index.html` içindeki ürün listesinde `id:` alanında bulabilirsiniz.
Ana sayfadaki build'in parçaları: `b1` gövde, `b2` motor, `b3` ESC,
`b4` uçuş kontrol kartı, `b5` VTX, `b6` kamera, `b7` alıcı, `b8` pervane,
`b9` batarya. Hazır kitler `kit1`–`kit3`.

## Çekim önerisi

- Düz, tek renk arka plan (tercihen beyaz ya da çok koyu gri)
- Kare kadraj, ürün ortada, kenarlarda ~%10 boşluk
- 1600×1600 px yeterli; JPEG kalite 80 civarı
- İlk fotoğraf 3/4 açı olsun — katalog kartında o görünüyor

## Telif

Buraya yalnızca kullanım hakkına sahip olduğunuz görselleri koyun.
Başka satıcıların sitesinden alınan fotoğraflar onların telifindedir;
üreticiler genelde bayilerine ayrı bir medya kiti verir, onu isteyin.