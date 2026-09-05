# Systeme de detection d'obstacle par ultrasons avec alarme

Systeme embarque de detection d'obstacles en temps reel, base sur un Arduino Uno et un capteur ultrason HC-SR04. Le principe s'inspire des systemes d'aide au stationnement automobile : le capteur mesure en continu la distance a un objet et declenche une alarme visuelle (LED) et sonore (buzzer) quand un obstacle passe sous les 20 cm.

Projet realise dans le cadre de mon apprentissage en electronique embarquee, L2 Physique et Applications, Universite d'Antananarivo.

## Apercu

| Photo 1 | Photo 2 | Photo 3 |
|---|---|---|
| ![Montage 1](photo1.jpg) | ![Montage 2](photo2.jpg) | ![Montage 3](photo3.jpg) |

[Video de demonstration](video.mp4)

## Fonctionnement

Le HC-SR04 emet une impulsion ultrasonique et mesure le temps de retour de l'echo pour calculer la distance (principe du sonar) :

1. Le microcontroleur declenche une impulsion de 10 microsecondes sur la broche TRIG.
2. Le capteur emet une salve ultrasonique a 40 kHz.
3. La broche ECHO passe a l'etat haut pendant la duree de l'aller-retour de l'onde.
4. La duree mesuree par `pulseIn()` permet de calculer la distance.
5. Si la distance est inferieure a 20 cm, la LED s'allume et le buzzer s'active. Sinon le systeme reste au repos.
6. La distance est affichee en continu sur le port serie, utile pour suivre les mesures en direct.

## Cablage

| Composant | Broche du composant | Broche Arduino Uno |
|---|---|---|
| HC-SR04 | VCC | 5V |
| HC-SR04 | GND | GND |
| HC-SR04 | TRIG | D9 |
| HC-SR04 | ECHO | D10 |
| LED | Anode (+) | D11 |
| LED | Cathode (-) | GND (via resistance 220 ohms) |
| Buzzer | (+) | D13 |
| Buzzer | (-) | GND |

Une resistance de 220 a 330 ohms est recommandee en serie avec la LED pour limiter le courant.

## Materiel requis

- 1 Arduino Uno (ou compatible)
- 1 capteur ultrason HC-SR04
- 1 LED
- 1 buzzer actif 5V
- 1 resistance 220-330 ohms
- Cables de connexion
- 1 breadboard

## Code

Le programme complet est dans [`ultrasonic_alarm.ino`](ultrasonic_alarm.ino).

Un timeout de 30 ms est applique a `pulseIn()` pour eviter que le programme se bloque si aucun echo ne revient (objet hors de portee).

## Installation

1. Cabler le circuit selon le schema ci-dessus.
2. Cloner le depot :
```bash
git clone https://github.com/SERGIO-OLIVIER-wink/ARDUINO-HC-SR04-ALARM.git
```
3. Ouvrir `ultrasonic_alarm.ino` dans l'IDE Arduino.
4. Selectionner la carte (Arduino Uno) et le port serie.
5. Televerser le programme.
6. Ouvrir le moniteur serie (9600 bauds) pour voir les mesures de distance en direct.

## Ameliorations possibles

Le systeme actuel fonctionne en tout ou rien (alarme declenchee ou non). Quelques pistes pour aller plus loin :

- Detection par paliers avec deux LED supplementaires : vert (> 30 cm), jaune (10-30 cm), rouge + buzzer (< 10 cm)
- Affichage de la distance sur un ecran LCD 16x2
- Reglage du seuil de detection via un potentiometre
- Ajout d'un servo-moteur pour faire pivoter le capteur
- Journalisation des detections avec horodatage

## Auteur

Sergio Olivier Rakotondravao
Etudiant en L2 Physique et Applications, Universite d'Antananarivo, Madagascar
[GitHub](https://github.com/SERGIO-OLIVIER-wink)

## Licence

Projet distribue sous licence [MIT](LICENSE).
