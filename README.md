# YouTube-GPX lejátszó

Videó tekerése egy GPS-nyomvonalon: az idősáv helyett a térképen kattintasz vagy
húzod a pontot, és a videó odaugrik. Lejátszás közben a pont követi a videót.

**Élő oldal:** https://kofferakos.github.io/youtube-gpx-lejatszo/

> Prototípus. A mintaként betöltött nyomvonal (Grand Wexl Tour) és a
> próbavideó nem ugyanarról a menetről szól, ezért a pont és a kép csak
> nagyjából fedi egymást. A működés bemutatására szolgál.

## Mit tud

- **Videóforrás:** YouTube-link, helyi videófájl vagy beépített tesztvideó.
- **Tekerés a térképen:** kattintás a nyomvonalra, vagy a piros pont húzása.
- **Fejezetek:** számozott jelölők a nyomvonalon, a listából átnevezhetők,
  törölhetők, és YouTube-leírásba másolható formában exportálhatók
  (`0:00 Rajt` formátum, a YouTube fejezetszabályainak ellenőrzésével).
- **Térképkártya:** lakat (a háttértérkép rögzítése), követés be/ki,
  tájolás négy égtáj szerint, és „Auto” mód, amely a legnagyobb nézetet adó
  irányt választja.
- **Saját GPX:** betölthető fájlból. Ha a GPX-ben van időbélyeg, a pozíció
  valós idő alapján számolódik, eltolással (offset) igazítható.

## Szinkron

| GPX | Hogyan számol |
|---|---|
| Időbélyeggel (rögzített track) | GPX-idő = videóidő + eltolás |
| Időbélyeg nélkül (tervezett útvonal) | a videó hosszát arányosan vetíti a távra, állandó sebességet feltételezve |

A pontos eredményhez olyan felvétel kell, amelyhez ugyanarról a menetről van
rögzített GPS-track (például Strava, Garmin vagy a kamera saját GPS-e).

## Korlátok

- A fejezetek csak a látogató saját böngészőjében tárolódnak; más nem látja őket.
- Egy ponthoz egy fejezet köthető, oda-vissza útvonalon ez kevés lehet.
- Elforgatott térképen a feliratok is elfordulnak.

## Felhasznált összetevők

- [Leaflet](https://leafletjs.com/) 1.9.4 (BSD-2-Clause)
- [leaflet-rotate](https://github.com/Raruto/leaflet-rotate) 0.2.8 (GPL-3.0)
- Térkép: © [OpenStreetMap](https://www.openstreetmap.org/copyright) közreműködők
- YouTube IFrame Player API
- Minta-nyomvonal: Grand Wexl Tour, [Wiener Alpen](https://www.wieneralpen.at/en/wechselland/touren/grand-wexl-tour)
- Próbavideó: [UpHill Trail – Wexl Trails](https://www.youtube.com/watch?v=X0cIlLJvOKw)

## Felépítés

Statikus oldal, szerver és build nélkül:

- `index.html`: az oldal (HTML, CSS, JavaScript egy fájlban)
- `track.js`: a minta-nyomvonal pontjai
- `.nojekyll`: a GitHub Pages változtatás nélkül szolgálja ki a fájlokat

Helyi futtatás: bármilyen statikus szerverrel, például
`python -m http.server 8765`, majd `http://localhost:8765`. Fájlként megnyitva
(`file://`) a YouTube-beágyazás nem működik.
