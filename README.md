# Déploiement

- firebase login

- firebase deploy

# Documentation des Séances

Pour ajouter une nouvelle séance d'entraînement, vous devez modifier le fichier `public/index.html` et ajouter un nouvel objet à la variable `workouts` dans la section `<script>`.

Chaque séance est un objet avec une clé unique (par exemple, `maNouvelleSeance`) et une valeur contenant les propriétés `name` et `plan`.

```javascript
const workouts = {
    // ... autres séances
    maNouvelleSeance: {
        name: "Nom de ma nouvelle séance",
        plan: [
            // ... liste des exercices
        ]
    }
};
```

## Structure d'un exercice

Le `plan` est un tableau d'objets, où chaque objet représente un exercice. Voici la structure d'un objet exercice :

### Propriétés communes

| Propriété          | Type    | Description                                                                 |
| ------------------ | ------- | --------------------------------------------------------------------------- |
| `nom`              | String  | Le nom de l'exercice qui sera affiché.                                      |
| `type`             | String  | Le type d'exercice. Valeurs possibles : `full_time`, `serie`, `EMOM`.       |
| `pause_after`      | Number  | Temps de pause en secondes après la fin de l'exercice.                      |
| `countdown_before` | Number  | Temps de préparation en secondes avant le début de l'exercice.              |

---

### Type: `full_time`

Cet exercice dure un temps défini.

**Propriétés spécifiques :**

| Propriété | Type   | Description                               |
| --------- | ------ | ----------------------------------------- |
| `temps`   | Object | Un objet contenant la durée de l'exercice. |

**Exemple `temps` :**

```json
{ "secondes": 60 }
```

**Exemple complet :**

```json
{
    "nom": "Maintien à l'appui",
    "type": "full_time",
    "temps": { "secondes": 30 },
    "pause_after": 15,
    "countdown_before": 5
}
```

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