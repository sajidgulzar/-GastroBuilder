# GastroBuilder Pro – erster lauffähiger Prototyp

Dies ist ein **Frontend-Prototyp** einer SaaS-Plattform, mit der mehrere Restaurants ihre Online-Shops verwalten können.

## So startest du ihn

1. Lade die ZIP-Datei herunter und entpacke sie.
2. Öffne den Ordner `gastrobuilder-prototype`.
3. Doppelklicke auf `index.html`. Es öffnet sich im Browser.
4. Du brauchst dafür keine Installation und keinen Server.

Für komfortableres Entwickeln kannst du den Ordner in Visual Studio Code öffnen und die Erweiterung **Live Server** verwenden.

## Was funktioniert bereits?

- Dashboard mit Beispiel-Kennzahlen
- Mehrere Demo-Restaurants über die Auswahl links
- Webseiten-Editor mit Live-Vorschau
- Anpassung von Restaurantname, Farben, Überschrift und Text
- Bereiche per Drag-and-drop sortieren sowie ein-/ausblenden
- Speisekarte: Gerichte hinzufügen, suchen, filtern, Verfügbarkeit ändern und löschen
- Bestellübersicht: Status ändern und CSV exportieren
- Einstellungs- und Abo-Vorschau
- Responsive Oberfläche für Desktop, Tablet und Mobil
- Speichern der Prototyp-Einstellungen im Browser (`localStorage`)

## Was ist noch NICHT produktionsbereit?

- Es gibt noch keinen Server, keine Benutzerkonten und keine sichere Mandantentrennung.
- Restaurant-, Menü- und Bestelldaten sind nur Demo-Daten im jeweiligen Browser.
- Onlinezahlungen sind nicht angebunden. Keine echten Kartendaten eingeben.
- Es werden keine echten Bestellungen an eine Küche gesendet.
- Es gibt keine echte Veröffentlichung eigener Restaurant-Domains.
- Rechtstexte, Datenschutz, Steuern, Rechnungen und Sicherheitsprüfungen müssen vor einem echten Start ergänzt werden.

## Empfohlene Architektur für die nächste Version

- **Frontend:** React + TypeScript, danach visueller Editor mit Drag-and-drop
- **Backend:** Node.js + TypeScript (REST API)
- **Datenbank:** PostgreSQL mit Mandanten-ID (`tenant_id`) in allen restaurantbezogenen Tabellen
- **Login & Rollen:** sichere Sitzungen, Inhaber-/Mitarbeiterrollen, Passwort-Reset
- **Dateien:** S3-kompatibler Objektspeicher für Food-Fotos
- **Zahlungen:** Zahlungsanbieter wie Stripe/PayPal über serverseitig bestätigte Webhooks; Barzahlung bleibt eine separate Zahlungsart
- **Hosting:** Frontend/CDN plus API und verwaltete PostgreSQL-Datenbank
- **Installierbare Kunden-App:** responsive Web-App als PWA (Manifest + Service Worker); später optional native Apps

## Datenmodell (erste Skizze)

- `tenants`: SaaS-Kunden / Restaurant-Unternehmen
- `users`: Benutzerkonten und Rollen
- `restaurants`: Name, Adresse, Kontakt, Öffnungszeiten, Design, Domain
- `pages`: Seiten pro Restaurant; Reihenfolge und Konfiguration der Inhaltsblöcke als JSON
- `menu_categories`: Kategorien mit Sortierung
- `menu_items`: Gerichte, Beschreibung, Preis, Verfügbarkeit, Bild
- `modifier_groups` / `modifier_options`: Extras, Größen und Zutatenwahl
- `customers`: Kundendaten
- `orders`: Status, Liefer-/Abholdaten, Summen, Zahlungsart
- `order_items` / `order_item_modifiers`: bestellte Gerichte und Extras als Preis-Snapshot
- `payments`: Zahlungsanbieter-Referenz, Betrag, Status
- `subscriptions` / `invoices`: SaaS-Abo und Rechnungen
- `domains`: Restaurant-Subdomains und eigene Domains
- `delivery_zones`: Liefergebiet und Mindestbestellwert
- `audit_logs`: wichtige Änderungen für Nachvollziehbarkeit

**Wichtig:** Preise, Berechtigungen und Zahlungsstatus müssen später immer serverseitig validiert werden. `tenant_id` darf niemals allein aus einer ungeprüften Browser-Eingabe vertraut werden.
