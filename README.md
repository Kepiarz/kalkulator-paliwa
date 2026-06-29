# Kalkulator Paliwa — aplikacja (PWA)

Aplikacja webowa, która działa offline, instaluje się na ekranie głównym telefonu
i przelicza koszt paliwa na trasie (km/mile, l/100 km lub MPG) z podziałem na osoby.

## Pliki
- `index.html` — cała aplikacja (interfejs + logika)
- `manifest.webmanifest` — dane instalacji (nazwa, ikona, kolory)
- `service-worker.js` — obsługa trybu offline
- `icons/` — ikony aplikacji

---

### Logika przeliczeń
- 1 mila = 1,609344 km
- MPG (US) → l/100 km: 235,214583 / MPG
- zużycie [l] = dystans[km] / 100 × spalanie[l/100km]
- koszt = zużycie × cena; kwota od osoby = koszt / liczba osób
