# Comparateur Températures — Prévisions Météo Multisites

Application météo mono-fichier (HTML/CSS/JS, sans backend) permettant de comparer en direct les températures de plusieurs villes du monde, via l'API [Open-Meteo](https://open-meteo.com/) (gratuite, sans clé API).

## Sélection des villes

- Recherche de n'importe quelle ville au monde (géocodage Open-Meteo), plusieurs villes en simultané.
- Altitude précise optionnelle par ville (utile pour une station de ski, un point en montagne) — corrige la température prévue pour ce point exact.
- Une même ville peut être ajoutée à plusieurs altitudes différentes (le panneau de saisie reste ouvert après validation, pour enchaîner les ajouts).
- Villes retirables individuellement via les chips (bouton ×).

## Graphique de comparaison

- 5 périodes disponibles : aujourd'hui, demain, après-demain, 3 jours, 7 jours.
- Une courbe par ville, plus deux lignes de seuil en pointillés : canicule (35 °C) et gel (0 °C).
- Une croix (×) marque le pic de chaque courbe.
- Clic sur une ville dans la légende pour masquer/afficher sa courbe (le bulletin et les cartes se mettent à jour en conséquence).
- Tooltip au survol avec icône météo par ville.

## Cartes par ville

Pour chaque ville sélectionnée :

- Température actuelle (ou à midi pour demain/après-demain), icône météo, heure locale mise à jour en direct.
- Humidité, vent (vitesse + direction), heure du soleil au plus haut, min/max de la période.
- **AQI moyen (7 jours)** : cliquable, affiché en rouge si supérieur à 60. Le clic déplie :
  - le détail par **polluant** — PM2.5, PM10, Ozone, NO₂, SO₂ — en rouge si le seuil santé OMS (moyenne 24h) est dépassé, avec description complète au survol de chaque puce ;
  - le détail par **pollen** — bouleau, graminées, olivier, ambroisie, aulne, armoise — en rouge au-delà d'un repère indicatif de risque allergique (données disponibles pour l'Europe uniquement).
- **Extrêmes sur 365 jours** (archives Open-Meteo, mesurées à l'emplacement exact de la ville) : nombre de jours de canicule (≥35 °C), de gel (≤0 °C), de vent fort (rafales ≥60 km/h) et de mauvaise qualité d'air (AQI ≥60).

## Bulletin de la période

- Ville la plus chaude et ville la plus fraîche pour la période affichée.
- Alertes automatiques si une ville dépasse le seuil canicule ou descend sous le seuil de gel.
- Historique de pollution des 7 derniers jours complets, par ville (puces journalières, en évidence si AQI ≥60).

## Extrêmes mondiaux

- Deux bandeaux calculés en direct : le point le plus chaud et le point le plus froid du monde, parmi une sélection de lieux connus pour leurs extrêmes (déserts, régions polaires, stations records) — ce n'est pas une recherche exhaustive de toutes les villes du monde.

## Confort d'usage

- Interface bilingue FR/EN et unité °C/°F (préférences mémorisées).
- Lien de partage qui conserve la sélection de villes (bouton natif de partage ou copie du lien).
- Accès direct par URL avec coordonnées GPS, pour un usage en raccourci ou depuis une appli mobile :
  ```
  ?lat=45.9237&lon=6.8694&alt=1035&nom=Chamonix
  ```
  Plusieurs points d'un coup, séparés par `;` :
  ```
  ?points=45.9237,6.8694,1035,Chamonix;48.8566,2.3522,,Paris
  ```
- Rafraîchissement automatique des données toutes les 15 minutes.

## Sources de données

- Prévisions horaires et géocodage : `api.open-meteo.com`, `geocoding-api.open-meteo.com`
- Qualité de l'air (AQI, polluants, pollens) : `air-quality-api.open-meteo.com`
- Archives 365 jours (extrêmes) : `archive-api.open-meteo.com`

## Notes techniques

- Fichier unique, aucune dépendance serveur — Chart.js chargé depuis un CDN pour le graphique.
- Toutes les requêtes API sont mises en cache en mémoire (par ville/coordonnées) pour limiter les appels redondants.
- Le résumé des fonctionnalités ci-dessus est aussi affiché directement dans le site, dans un panneau repliable juste avant le pied de page.
