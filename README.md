# 🐭 WHOOPI · Live Dashboard

Eine schlanke, mobile-first Web-App, die **live Herzfrequenz, RR-Intervalle und Batteriestand** von einem
abonnementfreien Whoop 4.0 ausliest – komplett im Browser, ohne App, ohne Server, ohne Cloud.

Alles steckt in **einer einzigen `index.html`**: Dark-Mode-Dashboard, selbst gezeichnete Live-Charts
(kein externes CDN), Verlauf in IndexedDB und CSV-Export.

> Die App **liest** nur Standard-Bluetooth-Daten. Sie verändert nichts am Gerät und sendet nichts ins Internet –
> deine Messwerte bleiben ausschließlich lokal in deinem Browser.

---

## ⚠️ Voraussetzungen (bitte zuerst lesen)

**1. Browser mit Web-Bluetooth-Unterstützung**

| Plattform | Funktioniert | Funktioniert **nicht** |
|-----------|--------------|------------------------|
| iPhone / iPad | **Bluefy** oder **BLE Link** (eigener Bluetooth-Stack) | Safari, Chrome, Edge (Apple sperrt Web Bluetooth in WebKit) |
| Android | Chrome, Edge | Firefox |
| Desktop | Chrome, Edge | Firefox, Safari |

**2. Das Whoop muss seine Herzfrequenz per Bluetooth senden.**
Die App kann das nicht aktivieren – das Gerät muss im Broadcast-Modus laufen bzw. die entsprechende
Firmware (Name beginnt mit `WHOOPI`) verwenden. Standard-Whoops müssen den HR-Broadcast aktiviert haben.

---

## ▶️ Nutzung

1. Die Seite über **HTTPS** öffnen (z. B. die GitHub-Pages-URL – Web Bluetooth funktioniert nur im sicheren Kontext).
2. **Connect WHOOPI** tippen und das Gerät aus der Liste wählen.
3. Werte laufen live ein, die Session wird automatisch aufgezeichnet.
4. **Finish & Export Session** erzeugt eine `.csv` mit `Timestamp`, `Heart Rate (BPM)` und `RR-Interval (ms)`.

Kein Gerät zur Hand? **Demo**-Button drücken – dann läuft das Dashboard mit simulierten Daten.

---

## ✨ Features

- Großer, im Puls glühender **BPM-Zähler**
- **Zwei Live-Charts**: Herzfrequenz + RR-Intervalle (offline, ohne Bibliothek)
- Karten für **Status, Batterie, RR/HRV, Workout-Stoppuhr**
- **Verlauf** vergangener Sessions (IndexedDB) mit Einzel-Export & Löschen
- **CSV-Export** mit iOS-Share-Fallback
- Sauberes Handling von Verbindungsabbrüchen und fehlendem Web-Bluetooth-Support

---

## 📈 Hinweis zu RR-Intervallen / HRV

RR-Intervalle (Bit 4 im Standard-HR-Profil) liefern vor allem Brustgurte zuverlässig. Ob ein optischer
Handgelenk-Sensor wie das Whoop im Live-Stream RR-Daten mitschickt, hängt vom Gerät/der Firmware ab.
Die App zeigt RR-Werte, **sobald** welche ankommen – andernfalls erscheint `n/a`. Das ist kein App-Fehler.

---

## 🔧 Technik

- Standard-BLE-Profile: **Heart Rate `0x180D` / `0x2A37`**, **Battery `0x180F` / `0x2A19`**
- HR-Parsing nach Bluetooth-SIG-Spec (UINT8/UINT16, Energy-Expended-Skip, RR in 1/1024 s → ms)
- Reines HTML/CSS/JS, keine Build-Tools, keine Abhängigkeiten

## 🙏 Credits

Die Reverse-Engineering-Vorarbeit zum Whoop 4.0 stammt von
[bWanShiTong/reverse-engineering-whoop](https://github.com/bWanShiTong/reverse-engineering-whoop)
und [openwhoop](https://github.com/bWanShiTong/openwhoop).

*Inoffizielles Hobby-Projekt, nicht mit WHOOP verbunden. Keine medizinische Verwendung.*
