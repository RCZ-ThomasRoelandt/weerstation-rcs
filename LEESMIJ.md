# Weerstation Richtpunt campus Ninove-Zottegem
Door **Xeno Becaus** en **Thomas Roelandt**

```
[Sensoren] → [Pico W] --wifi--> [Adafruit IO] <--leest-- [Website op GitHub Pages]
```

## Mappen

| Bestand | Wat? | Aanpassen? |
|---|---|---|
| `index.html` | Home: huidig weer + trends (24 u / 7 d / 30 d) | nee |
| `dashboard.html` | Alle live metingen, dak-analyse, systeemstatus | nee |
| `over-ons.html` | Jullie team + uitleg over het project | tekst mag |
| `css/style.css` | Huisstijl (goud #D6AD00 uit het Richtpunt-logo) | optioneel |
| `js/config.js` | 👉 **Koppeling met Adafruit IO (website)** | ✅ JA |
| `js/common.js` | Ophalen van data, demo-modus, iconen | nee |
| `js/home.js`, `js/dashboard.js` | Logica per pagina | nee |
| `pico/secrets.py` | 👉 **Wifi + Adafruit key (Pico)** | ✅ JA |
| `pico/main.py` | Leest alle sensoren en stuurt ze door | pinnen/factoren |

## Stap 1: Adafruit IO feeds
Maak op https://io.adafruit.com → **Feeds → New Feed** deze feeds (let op de **Key**):

`buiten-temp` · `luchtvochtigheid` · `luchtdruk` · `gasweerstand` · `windsnelheid`
`windrichting` · `neerslag` · `bme-temp` · `groen-dak` · `gewoon-dak` · `grijs-dak`

⚠️ Een gratis account laat maar **10 feeds** toe. `grijs-dak` is de 11e: die vraagt Adafruit IO+.
Zonder IO+: zet in `pico/main.py` de regel `"grijs": "grijs-dak"` in commentaar en zet in
`js/config.js` `grijsDak: ""`. De site verbergt grijs dak dan vanzelf (de waarde blijft op de SD-kaart).

Zet elke feed op **Public** (feed → ⚙️ → Privacy → Public), dan heeft de website geen key nodig.

## Stap 2: De Pico W
Kopieer de **hele inhoud van de map `pico/`** naar de Pico (Thonny → Bestand → Opslaan als → Raspberry Pi Pico),
inclusief de submap `lib/`. Vul `pico/secrets.py` in. Daarna start `main.py` automatisch.

## Stap 3: De website
1. `AIO_USERNAME` in `js/config.js` staat al ingevuld (XenoBecaus). Zo ziet de site echte data i.p.v. DEMO.
2. Test door `index.html` te openen in je browser.

## Stap 4: Online met GitHub Pages
1. Maak een repository op GitHub en upload alles **behalve `pico/secrets.py`**
   (het meegeleverde `.gitignore` houdt dat bestand al tegen als je met git werkt).
2. **Settings → Pages → Branch: main → / (root) → Save**
3. Na ± 1 minuut: `https://JOUWNAAM.github.io/REPONAAM/`

## Problemen?
- **"ontbrekende feeds: …"** op het dashboard → die feed key bestaat niet of staat niet op Public.
- **PICO LINK: NIET ACTIEF** → de Pico heeft al meer dan 5 minuten niets gestuurd (Thonny-console bekijken).
- **Trends leeg** → er is nog geen data in die periode; wacht even na de eerste metingen.
- Browser: **F12 → Console** toont de precieze fout.
