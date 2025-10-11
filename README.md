# Déploiement

- firebase login

- firebase deploy

# Lancement en local

- firebase emulators:start

# Gérer les Séances

Pour ajouter ou modifier une séance, vous devez travailler avec les fichiers situés dans le dossier `public/workouts`.

## Ajouter une séance

1.  **Créez un nouveau fichier JSON** dans le dossier `public/workouts` (par exemple, `maNouvelleSeance.json`).
2.  **Structurez ce fichier** en vous basant sur le modèle des autres séances. Il doit contenir un objet principal avec une clé `name` (le nom de la séance) et une clé `plan` (un tableau listant les exercices).
3.  **Référencez votre nouveau fichier** en ajoutant son nom dans le fichier `public/workouts/manifest.json`.

    ```json
    [
        "falseGripRapid.json",
        "seanceClassique.json",
        "seanceEmom.json",
        "maNouvelleSeance.json"
    ]
    ```

## Modifier une séance

Pour modifier une séance existante, il suffit d'éditer directement le fichier JSON correspondant dans le dossier `public/workouts`. Les changements seront automatiquement pris en compte au prochain chargement de l'application.

## Structure d'un exercice

Le `plan` est un tableau d'objets, où chaque objet représente un exercice. Voici la structure d'un objet exercice :

### Propriétés communes

| Propriété          | Type    | Description                                                                 |
| ------------------ | ------- | --------------------------------------------------------------------------- |
| `nom`              | String  | Le nom de l'exercice qui sera affiché.                                      |
| `type`             | String  | Le type d'exercice. Valeurs possibles : `serie`, `EMOM`.                   |
| `pause_after`      | Number  | Temps de pause en secondes après la fin de l'exercice.                      |
| `countdown_before` | Number  | Temps de préparation en secondes avant le début de l'exercice.              |

---

### Type: `serie`

Cet exercice est basé sur un nombre de séries. L'utilisateur valide manuellement la fin de chaque série.

**Propriétés spécifiques :**

| Propriété | Type   | Description                                  |
| --------- | ------ | -------------------------------------------- |
| `number`  | Number | Le nombre total de séries à effectuer.       |
| `rest`    | Number | Le temps de repos en secondes entre chaque série. |

**Exemple complet :**

```json
{
    "nom": "Dips",
    "type": "serie",
    "number": 3,
    "rest": 180,
    "pause_after": 120,
    "countdown_before": 10
}
```

---

### Type: `EMOM` (Every Minute On the Minute)

Cet exercice consiste à répéter une action au début de chaque intervalle de temps pour une durée totale définie.

**Propriétés spécifiques :**

| Propriété | Type   | Description                                                                                                                               |
| --------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `temps`   | Object | Un objet décrivant la durée totale et l'intervalle de chaque round. `{ "every": 60, "during": 480 }` (toutes les 60s pendant 480s).         |
| `repeat`  | Object | (Optionnel) Permet de répéter le bloc EMOM plusieurs fois. `{ "number": 3, "pause_between": 30 }` (3 fois avec 30s de pause entre chaque). |

**Exemple complet :**

```json
{
    "nom": "EMOM Tractions",
    "type": "EMOM",
    "temps": { "every": 60, "during": 480 },
    "pause_after": 30,
    "countdown_before": 30
}
```