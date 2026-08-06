# rune-releases

Le manifeste de version et les paquets de **Rune**. Rien d'autre.

Le code vit dans un dépôt privé. Ce dépôt-ci est public parce qu'il doit
l'être : Rune lit `manifest.json` au démarrage pour savoir si une version plus
récente existe, et `raw.githubusercontent.com` refuse la lecture d'un dépôt
privé sans jeton — un jeton qu'il faudrait embarquer dans l'exécutable, donc
livrer à quiconque sait lire un binaire.

## manifest.json

```json
{
  "version": "0.1.0",
  "url": "https://github.com/TomaTV/rune-releases/releases/download/v0.1.0/Rune-v0.1.0.zip",
  "sha256": "…",
  "notes": "Ce qui a changé, en une phrase.",
  "files": {
    "_internal/rune/app.py": "…"
  }
}
```

`version` se compare à celle du paquet installé. `sha256` est vérifié après
téléchargement — un zip corrompu ne s'installe pas. `files` est optionnel :
avec lui, Rune ne remplace que les fichiers dont l'empreinte a changé, ce qui
évite de retélécharger dix gigaoctets pour corriger une ligne.
