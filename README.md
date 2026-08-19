# Podcasts AM — Folgendaten

Dieses Repo ist **kein Programmcode und keine Webseite**, sondern die ausgelieferten
Daten für die App *Podcasts AM*: je Podcastfolge eine JSON-Datei mit Einzeiler,
Kurzfassung, Stichpunkten, Kapiteln, Shownotes und — wo möglich — Byte-Bereichen für
kurze Audioausschnitte.

**Nichts hier wird von Hand geändert.** Alles entsteht aus dem Repo
`podcastam-pipeline` über `werkzeuge/veroeffentlichen.py` und wird als Ganzes ersetzt.

## Aufbau

```
/v1/index.json              Liste aller Shows
/v1/show/<sha1>.json        Verzeichnis einer Show, mit allen ihren Folgen
/v1/episode/<sha1>.json     eine Folge
```

`<sha1>` ist der SHA-1 der normalisierten GUID (Unicode-NFC, getrimmt, UTF-8), bei
Shows der der Feed-Adresse. Das Versionssegment `/v1/` wandert mit `schema_version`
aus dem Vertrag; steigt sie, entsteht `/v2/` daneben und ältere App-Fassungen lesen
weiter `/v1/`.

Der Vertrag zwischen Pipeline und App ist `schema.json` im Repo `podcastam-pipeline`.
**Änderungen nur über `schema_version`, nie still.**

## Was hier ausdrücklich nicht liegt

**Kein Audio.** Die Ausschnitte werden nicht geschnitten und nicht gehostet — die App
holt sie per HTTP-`Range` direkt vom CDN des Podcasters. Hier stehen nur Zahlen:
Startzeit, Endzeit, Byte-Bereich. Das ist die tragende Konstruktion des ganzen
Features, und sie hat keine Ausnahme.
