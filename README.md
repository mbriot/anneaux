
Je voudrai faire une page index.html, avec un text area.
Ce que je vais copier dedans sera un json descriptif de ma séance de musculation.
Par exemple :

{
  "nom": "echauffement",
  "type": "temps_complet",
  "temps": {
    "minutes": 6
  },
  "pause_after": 60,
  "countdown_before": 10
}

il faudra alors afficher sur la page le champ nom en majuscule.
Lancer un compte a rebour qui démarre a temps.minutes 
nom: tractions
type: emom
temps: {
  "every": 1,
  "during": 8,
  series: {
    "repetitions": 5,
    "pause": 40
  }
},
pause_after: 60
countdown_before: 10

nom: rowing,
type: serie,
series: [
  {
    "repetitions": 10,
    "pause": 45,
  },
  {
    "repetitions": 10,
    "pause": 45,
  }
],
pause_after: 60
countdown_before: 10
