# Parcours IA — EAFC Charlemagne

Dashboard pédagogique gamifié connecté à Moodle via l'API REST.

## Architecture

```
Moodle (instance configurée dans config.js)
    ↑ API REST (token étudiant·e)
index.html (GitHub Pages)
    → Dashboard gaming temps réel
```

## Configuration

### 1. URL Moodle et ID de cours

Copie `config.example.js` → `config.js` et renseigne les valeurs :

```js
const MOODLE_URL = 'https://your-moodle-instance.com';
const COURSE_ID  = 0; // ← ID visible dans l'URL du cours Moodle
```

### 2. Lier les activités Moodle aux salles

Pour chaque salle dans `SALLES_DEF`, renseigne les `activity_ids` :

```js
{
  id: 1,
  activity_ids: [12345, 12346], // ← IDs des activités (visibles dans l'URL Moodle : ?id=XXXX)
  ...
}
```

**Comment trouver un ID d'activité :**
1. Va dans Moodle sur l'activité concernée
2. Regarde l'URL : `…/mod/assign/view.php?id=XXXX`
3. `XXXX` est le `cmid` à renseigner

### 3. Lier les scores du carnet de notes

Les scores sont cherchés par fragment de nom :

```js
const scoreDefi1 = getGradeForItem('défi 1');
```

Le nom doit correspondre partiellement au nom de l'item dans le carnet Moodle.

## Utilisation étudiant·e

1. Aller sur l'URL de déploiement (GitHub Pages)
2. Ouvrir Moodle → **Mes préférences → Sécurité → Clés de service**
3. Copier la clé **Moodle mobile web service**
4. La coller dans le dashboard → Connecter

Le token est sauvegardé en localStorage — une seule saisie nécessaire.

## Déploiement

```bash
git add .
git commit -m "update"
git push origin main
```

GitHub Pages publie automatiquement depuis la branche `main`.

## Structure

```
parcours-ia-eafc/
├── index.html   # Dashboard complet (HTML/CSS/JS en un seul fichier)
└── README.md
```
