# GeoJSON Peta Kampus

Repositori ini berisi data spasial kampus dalam format **GeoJSON**. Dataset dapat
digunakan untuk menampilkan lokasi bangunan dan elemen lingkungan kampus pada
peta digital atau aplikasi Sistem Informasi Geografis (SIG).

## Isi repositori

| File | Deskripsi |
| --- | --- |
| [`714240036.geojson`](./714240036.geojson) | Dataset fitur spasial kampus |

Dataset terdiri dari:

- **39 fitur** berjenis `Polygon` dan `LineString`
- Informasi nama bangunan pada properti `Gedung` atau `nama`
- Properti tampilan seperti `fill` dan `fill-opacity` pada sebagian fitur
- Koordinat geografis dalam urutan **longitude, latitude** (WGS 84)

Beberapa fitur yang tersedia antara lain Auditorium, Vokasi, Anggrek, Rektorat,
Masjid, GOR, Kantin, Perpustakaan, Transportasi, dan Sarana Prasarana.

## Format data

File menggunakan struktur standar GeoJSON:

```text
FeatureCollection
└── features
    ├── geometry: Polygon atau LineString
    └── properties: informasi nama dan gaya tampilan
```

Contoh properti fitur:

```json
{
  "Gedung": "Auditorium",
  "fill": "rgba(0, 0, 0, 1)",
  "fill-opacity": 0.7
}
```

## Penggunaan

Dataset dapat dibuka menggunakan aplikasi yang mendukung GeoJSON, seperti
QGIS, ArcGIS, geojson.io, atau pustaka pemetaan berbasis web.

Contoh pemuatan menggunakan Leaflet:

```html
<script>
  fetch("./714240036.geojson")
    .then((response) => response.json())
    .then((data) => {
      L.geoJSON(data, {
        onEachFeature: (feature, layer) => {
          const properties = feature.properties || {};
          const name = properties.Gedung || properties.nama;
          if (name) {
            layer.bindPopup(name);
          }
        }
      }).addTo(map);
    });
</script>
```

Pastikan variabel `map` sudah dibuat dan pustaka Leaflet sudah dimuat sebelum
menjalankan contoh tersebut.

## Validasi

Untuk memeriksa bahwa file merupakan JSON yang valid, gunakan salah satu cara
berikut:

```powershell
Get-Content .\714240036.geojson -Raw | ConvertFrom-Json
```

atau buka file menggunakan validator GeoJSON seperti geojson.io.

## Lisensi dan sumber data

Informasi lisensi dan sumber resmi dataset belum dicantumkan dalam repositori.
Tambahkan keterangan tersebut apabila dataset akan dibagikan atau digunakan
untuk kebutuhan publik.
