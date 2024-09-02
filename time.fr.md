# Gestion du temps

## Fuseau français métropolitain

Dans le fuseau français métropolitain `Europe/Paris`, on distingue deux périodes :
- l'heure d'hiver :
  - décalage horaire `+01:00` par rapport au temps universel (UTC)
  - désigné par CET pour _Central Europe Time_
  - passage à l'heure d'hiver :
    - a lieu en automne, le dernier dimanche d'octobre
    - à 3H00 du matin, l'horloge est retardée d'une heure
    - il est alors de nouveau 2H00 du matin, la plage 2H-3H existe 2 fois
    - on peut dire qu'on : "recule d'une heure" / "gagne une heure"
- l'heure d'été :
  - décalage horaire `+02:00` par rapport au temps universel (UTC)
  - désigné par CEST pour _Central Europe Summer Time_
  - = décalage Europe/Paris standard (+01:00) + 1h
  - en anglais, on parle de _daylight saving time_ (DST)
  - passage à l'heure d'été :
    - a lieu au printemps, le dernier dimanche de mars
    - à 2H00 du matin, l'horloge est avancée d'une heure
    - il est alors 3H00 du matin, la plage 2H-3H n'existe pas
    - on peut dire qu'on : "avance d'une heure" / "perd une heure"

Historique des dates de changement d'heure, de 2019 et à 2024 :

| hiver → été | été → hiver |
|-------------|-------------|
| 31/03/2019  | 27/10/2019  |
| 29/03/2020  | 25/10/2020  |
| 28/03/2021  | 31/10/2021  |
| 27/03/2022  | 30/10/2022  |
| 26/03/2023  | 29/10/2023  |
| 31/03/2024  | 27/10/2024  |


## UTC / GMT / Z

**UTC (temps universel coordonné) :**
- pas un fuseau
- standard international utilisé pour gérer le temps

**GMT (_Greenwich Mean Time_) :**
- fuseau correspondant au décalage nul (`+00:00`)
- Un décalage en heure d'été est théoriquement possible dans ce fuseau,
  mais les Britanniques semblent dans ce cas préférer se considérer dans le fuseau BST (_British Summer Time_).

**Heure Zoulou (_Zulu Time_) :**
- d'origine militaire
- correspond à l'absence de décalage par rapport à UTC
- se note `Z` à la fin d'un horodatage, et non `+00:00`

Selon le contexte, on pourra trouver des confusions entre UTC, GMT et Zoulou,
pour désigner de manière générale l'absence de décalage par rapport au temps de référence.
 
