# ScanAndCook: Kochbuch-Rezepte für die Bring! App

## 📖 Projektbeschreibung

Dieses Repository dient als Sammlung statischer Rezeptdateien, die speziell für die Integration mit der **Bring! Einkaufslisten-App** über QR-Codes entwickelt wurden. Jedes Rezept wird als einfache HTML-Datei gespeichert, die strukturierte Daten (JSON-LD) enthält, welche die Bring! App parsen kann. Dies ermöglicht es Benutzern, einen QR-Code in einem physischen Kochbuch (oder von einem Bildschirm) zu scannen und alle Zutaten sofort zu ihrer Bring! Einkaufsliste hinzuzufügen.

## ✨ Funktionsweise

Der Prozess nutzt Standard-Webtechnologien und die Deep-Linking-Fähigkeiten der Bring! App:

1.  **Rezept-HTML-Dateien:** Jedes Rezept ist eine individuelle `.html`-Datei.
2.  **Strukturierte Daten (JSON-LD):** Innerhalb jeder HTML-Datei sind die Zutaten und Metadaten des Rezepts mithilfe des [Schema.org Recipe JSON-LD-Formats](https://schema.org/Recipe) eingebettet. Dies ist entscheidend, damit Bring! den Rezeptinhalt verstehen kann.
3.  **GitHub Pages Hosting:** Diese HTML-Dateien werden öffentlich über GitHub Pages gehostet, was eine stabile und zugängliche URL für jedes Rezept bereitstellt.
4.  **Bring! Deeplink:** Für jedes Rezept wird eine spezielle URL (ein "Deeplink") konstruiert, die auf die GitHub Pages-URL des Rezepts verweist. Dieser Deeplink weist die Bring! App an, das Rezept abzurufen und zu parsen.
5.  **QR-Code-Generierung:** Der Bring! Deeplink wird dann in einen QR-Code umgewandelt. Beim Scannen mit einer Smartphone-Kamera öffnet dieser QR-Code die Bring! App und importiert die Zutaten.

## 🚀 Erste Schritte: Ein neues Rezept hinzufügen

Befolge diese Schritte, um ein neues Rezept zu dieser Sammlung hinzuzufügen und den entsprechenden QR-Code zu generieren:

### Schritt 1: Erstelle die Rezept-HTML-Datei mit JSON-LD

1.  **Öffne einen einfachen Texteditor** (z.B. Notepad, TextEdit, VS Code).
2.  **Kopiere die folgende Vorlage** und füge sie in den Editor ein.
    *   **Wichtig:** Ersetze den Platzhalterinhalt (`"name"`, `"recipeIngredient"`, `"description"`, `"recipeYield"`) durch deine tatsächlichen Rezeptdetails.
    *   Stelle sicher, dass deine Zutaten klar innerhalb des `recipeIngredient`-Arrays aufgeführt sind.

    ```html
    <!DOCTYPE html>
    <html lang="de">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Dein Rezeptname</title>
        
        <!-- Schema.org JSON-LD für das Rezept -->
        <script type="application/ld+json">
        {
          "@context": "http://schema.org",
          "@type": "Recipe",
          "name": "Dein Rezeptname Hier",
          "recipeIngredient": [
            "Menge Zutat 1",
            "Menge Zutat 2",
            "Menge Zutat 3"
            // Füge hier alle Zutaten hinzu
          ],
          "description": "Eine kurze Beschreibung deines Rezepts.",
          "recipeYield": "4 Portionen" // Passe die Portionsanzahl an
        }
        </script>
    </head>
    <body>
        <!-- Optional: Sichtbarer Inhalt für den Browser (gut für die Lesbarkeit) -->
        <h1>Dein Rezeptname Hier</h1>
        <p>Eine kurze Beschreibung deines Rezepts.</p>
        <h2>Zutaten:</h2>
        <ul>
            <li>Menge Zutat 1</li>
            <li>Menge Zutat 2</li>
            <li>Menge Zutat 3</li>
        </ul>
        <!-- Hier könnten auch Zubereitungsschritte in normalem HTML hinzugefügt werden -->
    </body>
    </html>
    ```
3.  **Speichere die Datei** mit einem aussagekräftigen Namen und der Endung `.html` (z.B. `mein-lecker-kuchen.html`). Verwende Bindestriche anstelle von Leerzeichen für eine bessere URL-Kompatibilität.

### Schritt 2: Lade die HTML-Datei in dieses GitHub-Repository hoch

1.  Gehe zu deinem Repository auf GitHub: `https://github.com/ScanAndCook/Cookbook-Recipes`
2.  Klicke auf **"Add file"** und dann auf **"Upload files"**.
3.  Ziehe deine neu erstellte `.html`-Datei per Drag & Drop in den Upload-Bereich oder verwende die Schaltfläche "choose your files".
4.  Füge eine prägnante **Commit-Nachricht** hinzu (z.B. "Add new recipe: Mein Lecker Kuchen").
5.  Klicke auf den grünen Button **"Commit changes"**.

### Schritt 3: Rufe die GitHub Pages URL für dein Rezept ab

Nach dem Hochladen wird GitHub Pages deine Datei automatisch bereitstellen. Dies dauert in der Regel einige Minuten.

1.  Gehe in deinem Repository zu **"Settings"** und klicke dann in der linken Seitenleiste auf **"Pages"**.
2.  Bestätige, dass GitHub Pages so konfiguriert ist, dass es "Deploy from a branch" (normalerweise der `main`-Branch, Ordner `/ (root)`) verwendet.
3.  Die Basis-URL für deine GitHub Pages-Website wird dort angezeigt (z.B. `https://scancook.github.io/Cookbook-Recipes/`).
4.  Die direkte URL deines Rezepts lautet dann:
    `https://scancook.github.io/Cookbook-Recipes/DEIN_REZEPTDATEINAME.html`
    (z.B. `https://scancook.github.io/Cookbook-Recipes/mein-lecker-kuchen.html`)

    **Wichtig:** Es ist entscheidend, die **GitHub Pages URL** (z.B. `https://scancook.github.io/...`) und **NICHT** die `raw.githubusercontent.com`-URL zu verwenden, da erstere den korrekten `Content-Type`-Header für die Verarbeitung der HTML-Datei durch Bring! bereitstellt.

### Schritt 4: Generiere den Bring! Deeplink

Konstruiere nun die spezielle URL, die Bring! verwenden wird.

1.  **URL-kodieren deine GitHub Pages URL des Rezepts.**
    Du kannst dafür einen [Online-URL-Encoder](https://www.urlencoder.org/) verwenden.
    *   **Beispiel (für `mein-lecker-kuchen.html`):**
        Original: `https://scancook.github.io/Cookbook-Recipes/mein-lecker-kuchen.html`
        Kodiert: `https%3A%2F%2Fscancook.github.io%2FCookbook-Recipes%2Fmein-lecker-kuchen.html`

2.  **Setze den vollständigen Bring! Deeplink zusammen:**
    Kombiniere die Bring! API-Basis-URL mit deiner kodierten Rezept-URL und dem Parameter `source=web`.

    ```
    https://api.getbring.com/rest/bringrecipes/deeplink?url=DEINE_KODIERTE_REZEPT_URL&source=web
    ```
    *   **Beispiel:**
        ```
        https://api.getbring.com/rest/bringrecipes/deeplink?url=https%3A%2F%2Fscancook.github.io%2FCookbook-Recipes%2Fmein-lecker-kuchen.html&source=web
        ```

### Schritt 5: Erstelle den QR-Code

1.  Gehe zu einem [Online-QR-Code-Generator](https://www.qrcode-monkey.com/) (oder einem anderen deiner Wahl).
2.  Füge den **vollständigen Bring! Deeplink** (aus Schritt 4) in das Feld des Generators ein.
3.  Generiere den QR-Code.

## ✅ Testen

**Bevor du dein Kochbuch druckst, teste immer jeden generierten QR-Code!**

1.  Scanne den QR-Code mit der Kamera-App deines Smartphones.
2.  Bestätige, dass die Bring! App geöffnet wird.
3.  Überprüfe, ob alle Zutaten korrekt in deine Einkaufsliste importiert werden.

## 📝 Lizenz

Dieses Projekt ist Open-Source und unter der [MIT-Lizenz](LICENSE) verfügbar. (Falls du eine Lizenz hinzufügen möchtest, ansonsten diesen Abschnitt entfernen).
