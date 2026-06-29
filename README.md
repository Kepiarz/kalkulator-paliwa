# Kalkulator Paliwa — aplikacja (PWA)

Aplikacja webowa, która działa offline, instaluje się na ekranie głównym telefonu
i przelicza koszt paliwa na trasie (km/mile, l/100 km lub MPG) z podziałem na osoby.

## Pliki
- `index.html` — cała aplikacja (interfejs + logika)
- `manifest.webmanifest` — dane instalacji (nazwa, ikona, kolory)
- `service-worker.js` — obsługa trybu offline
- `icons/` — ikony aplikacji

---

## A. Użyć od ręki (bez APK)
1. Skopiuj folder na telefon i otwórz `index.html` w Chrome,
   **albo** wrzuć go na dowolny hosting HTTPS (patrz niżej).
2. Menu Chrome (⋮) → „Dodaj do ekranu głównego". Gotowe — działa offline.

## B. Zrobić prawdziwy plik .apk (za darmo, bez Android Studio)
Najprościej przez **PWABuilder**:
1. Wrzuć ten folder na **GitHub Pages** (darmowy hosting HTTPS):
   - załóż repozytorium, wgraj pliki, włącz Pages (Settings → Pages → branch `main`, katalog `/`).
   - dostaniesz adres typu `https://twojlogin.github.io/paliwo/`.
2. Wejdź na **https://www.pwabuilder.com**, wklej ten adres, kliknij **Start**.
3. Zakładka **Android** → **Generate Package**. Pobierzesz paczkę z:
   - podpisanym `.apk` (do zainstalowania na telefonie) oraz `.aab` (do Google Play),
   - plikiem `signing.keystore` + hasłami — **zachowaj je**, są potrzebne do aktualizacji.
4. Przerzuć `.apk` na telefon i zainstaluj (włącz „instalowanie z nieznanych źródeł").

## C. Wariant natywny (Android Studio)
Jeśli wolisz pełną kontrolę, opakuj apkę w **Capacitor**:
```
npm create @capacitor/app
# wrzuć index.html, manifest, service-worker.js, icons/ do folderu www/
npx cap add android
npx cap open android      # build .apk w Android Studio
```
Wymaga Android SDK (Android Studio pobiera je sam).

---

### Logika przeliczeń
- 1 mila = 1,609344 km
- MPG (US) → l/100 km: 235,214583 / MPG
- zużycie [l] = dystans[km] / 100 × spalanie[l/100km]
- koszt = zużycie × cena; kwota od osoby = koszt / liczba osób
