-----------------------------------------------------------------------

<table>
<tr>
<td><img src="Polytechnique_signature-RGB-gauche_FR.png" alt="Logo de Polytechnique Montréal"></td>
<td><h2>INF3500 - Conception et réalisation de systèmes numériques
<br><br>Automne 2020
<br><br>Laboratoire #2
<br>Banc d'essai pour un module combinatoire
</h2></td>
</tr>
</table>

------------------------------------------------------------------------

# Le problème du musée

------------------------------------------------------------------------

Ce laboratoire s'appuie sur le matériel suivant :
1. Les concepts couverts dans le laboratoire #1.
2. La matière du cours des semaines 2 (Technologies de logique programmable) et 3 (Modélisation et vérification de circuits combinatoires).

À la fin de ce laboratoire, vous devrez être capable de :

* concevoir un banc d'essai pour vérifier qu'un module combinatoire rencontre ses spécifications;
* corriger la conception d'un module combinatoire pour qu'il rencontre ses spécifications; et,
* faire la synthèse et l'implémentation du module, et programmer un FPGA pour en vérifier le fonctionnement.

## Partie 0 : Préparation

* Lancez Active-HDL, créez un espace de travail (workspace) et créez un projet (design).
* Créez un répertoire "inf3500\labo2" dans lequel vous mettrez tous les fichiers de ce laboratoire.
* Importez tous les fichiers du laboratoire à partir de l'entrepôt Git

## Partie 1 : Conception d'un banc d'essai

Le musée des beaux arts de St-Denis-de-Brompton expose une vaste collection de photos du tournoi de pêche à la barbotte au lac Bowker. Les photos sont réparties dans 15 salles d'exposition numérotées de 0 à 14 inclusivement. À cause de la valeur inestimable de la collection, chaque salle est munie d’un détecteur de mouvement et on engage un gardien de nuit pour patrouiller le musée. Vous devez concevoir le module de contrôle du système d’alarme. Le système doit avoir deux modes de fonctionnement : normal et patrouille. Le gardien active le mode patrouille à l'aide d'un commutateur avant de débuter sa ronde, et il le désactive en rentrant au poste de garde. En mode normal, l'alarme doit être déclenchée si au moins un des détecteurs de mouvement rapporte un intrus. En mode patrouille, une alarme doit être déclenchée si au moins deux détecteurs de mouvement sont actifs, indiquant que le gardien est dans une salle et au moins un intrus est dans une autre. En mode patrouille, une 2e alarme doit aussi être déclenchée dans le cas spécifique où aucun détecteur de mouvement n’est actif, indiquant que le gardien s'est perdu ou bien s’est endormi.

Considérez la description partielle de banc d'essai disponible dans le fichier [musee_labo_2_tb.vhd](musee_labo_2_tb.vhd). Complétez le banc d'essai pour qu'il vérifie le comportement d'un module selon la spécification qui est donnée. Votre banc d'essai doit faire un test exhaustif du module, c'est à dire qu'il doit le stimuler avec tous les cas possibles. Pour pratiquer, vous pouvez appliquer votre banc d'essai au module [musee_labo_2.vhd](musee_labo_2.vhd). Ce module comporte plusieurs erreurs.

## Partie 2 : Correction de la conception du module

Corrigez le module [musee_labo_2.vhd](musee_labo_2.vhd) pour qu'il rencontre les spécifications données à la partie 1. Vérifiez son bon fonctionnement grâce à votre banc d'essai.

## Partie 3 : Synthèse et implémentation sur la planchette

Confirmez que vous avez bien importé les fichiers suivants à votre répertoire de projet inf3500\labo2 :
* [basys_3_top_labo_2.vhd](basys_3_top_labo_2.vhd)
* [basys-3-top.xdc](basys-3-top.xdc)
* [inf3500_utilitaires_pkg.vhd](inf3500_utilitaires_pkg.vhd)

Suivez les étapes suivantes pour faire la synthèse et l'implémentation de votre code :

1. Sous votre répertoire "inf350\labo2", créez un répertoire "synthese-implementation".
2. Lancez une fenêtre d'invite de commande ("cmd" sous Windows) et naviguez au répertoire "inf350\labo2\synthese-implementation".
3. De ce répertoire, lancez Vivado en mode script avec la commande  
`{repertoire-d-installation-d-Vivado}\bin\vivado -mode tcl`  
où {repertoire-d-installation-d-Vivado} est probablement C:\Xilinx\Vivado\2020.1 si votre système d'exploitation est Windows.
4. Dans la fenêtre, à l'invite de commande Vivado%, entrez les commandes que vous trouverez dans le fichier [labo-2-synth-impl.tcl](labo-2-synth-impl.tcl). 

Vérifiez le fonctionnement correct de votre système sur la planchette.

## Partie 4: Bonus - au-delà du A

**Mise en garde**. *Compléter correctement les parties 1, 2 et 3 peut donner une note de 17 / 20 (85%), ce qui peut normalement être interprété comme un A. La partie 4 demande du travail supplémentaire qui sort normalement des attentes du cours. Il n'est pas nécessaire de la compléter pour réussir le cours ni pour obtenir une bonne note. Il n'est pas recommandé de s'y attaquer si vous éprouvez des difficultés dans un autre cours. La partie 4 propose un défi supplémentaire pour les personnes qui souhaitent s'investir davantage dans le cours INF3500 en toute connaissance de cause.*

### 4a. Afficher le numéro de la salle la plus près où il y a du mouvement
Modifiez votre fichier musee_labo_2.vhd pour afficher, sur l'affichage à sept segments de la planchette, le numéro de la salle où du mouvement est détecté. Si plus d'un détecteur de mouvement est actif, il faut afficher le numéro de la salle la plus proche du poste de garde, soit le numéro le plus près de 0.

Si vous complétez cette partie, ne remettez qu'un seul fichier musee_labo_2.vhd qui contient les modifications de la partie 1 et de la partie 4.

### 4b. Étude de l'utilisation des ressources de votre module selon le nombre d'entrées

Faites plusieurs synthèses (et non l'implémentation au complet) de votre module musee_labo_2.vhd uniquement (et non le module basys-3-top.vhd) et obtenez un rapport des ressources utilisées avec les commandes suivantes :

`synth_design -top musee_labo_2 -generic N=**un-nombre-ici** -part xc7a35tcpg236-1 -assert`  
`report_utilization -file monrapport.txt` (pour créer un nouveau fichier) ou `report_utilization -file monrapport.txt -append` (pour ajouter au fichier à chaque itération)

Changez le nombre de détecteurs à chaque fois (paramètre N). Vous pouvez programmer une boucle (`help for`) dans Ivado afin d'automatiser le processus.

Étudiez la progression de la complexité du circuit quand le nombre de détecteurs varie. Présentez vos résultats sous forme tabulaire et graphique, faites une analyse et présentez une discussion  dans un [rapport-ressources-labo-2.md](rapport-ressources-labo-2.md).

## Remise

La remise se fait directement sur votre entrepôt Git. Faites un 'push' régulier de vos modifications, et faites un 'push' final avant la date limite de la remise. Placez tous les fichiers dans la racine de l'entrepôt. Consultez le barème de correction pour la liste des fichiers à remettre.

**Directives spéciales :**
* Ne modifiez pas les noms des fichiers, les noms des entités, les listes des *generics*, les listes des ports ou les noms des architectures.
* Remettez du code de très bonne qualité, lisible et bien aligné, bien commenté. Indiquez clairement la source de tout code que vous réutilisez ou duquel vous vous êtes inspiré/e.
* Modifiez le fichier [carte.md](carte.md) pour spécifier quelle carte vous utilisez. Si ce n'est pas la Basys 3, remettez aussi votre fichier *.xdc, par exemple un fichier nexys-a7-top.xdc.

## Barème de correction

Le barème de correction est progressif. Il est relativement facile d'obtenir une note de passage (> 10) au laboratoire et il faut mettre du travail pour obtenir l'équivalent d'un A (17/20). Obtenir une note plus élevée (jusqu'à 20/20) nécessite plus de travail que ce qui est normalement demandé dans le cadre du cours et plus que les 9 heures que vous devez normalement passer par semaine sur ce cours.

Critères | Points
-------- | ------
Partie 1 : votre banc d'essai complet dans le fichier musee_labo_2_tb.vhd | 8
Partie 2 : votre module final dans le fichier musee_labo_2.vhd | 5
Partie 3 : votre fichier basys-3-top.bit | 2
Qualité, lisibilité et élégance du code : alignement, choix des identificateurs, qualité et pertinence des commentaires, respect des consignes de remise incluant les noms des fichiers, orthographe, etc. | 2
Pleine réussite du labo | 17

Bonus | Points
----- | ------
Partie 4a : ne remettez qu'un seul fichier musee_labo_2.vhd (de la partie 2) qui inclut le code pour la partie 4a. On en tiendra compte à la correction | 1
Partie 4b : remettez un fichier de rapport [rapport-ressources-labo-2.md](rapport-ressources-labo-2.md) incluant vos données sous forme tabulaire et graphique, une analyse et une discussion | 2
Maximum possible sur 20 points | 20

## Références pour creuser plus loin

Les liens suivants ont été vérifiés en septembre 2020.

* Aldec Active-HDL User Guide : accessible en faisant F1 dans l'application, et accessible [à partir du site de Aldec](https://www.aldec.com/en/support/resources/documentation/manuals/).
* Tous les manuels de Xilinx :  <https://www.xilinx.com/products/design-tools/vivado.html#documentation>
* Vivado Design Suite Tcl Command Reference Guide : <https://www.xilinx.com/support/documentation/sw_manuals/xilinx2019_2/ug835-vivado-tcl-commands.pdf>
* Vivado Design Suite User Guide - Design Flows Overview : <https://www.xilinx.com/support/documentation/sw_manuals/xilinx2019_2/ug892-vivado-design-flows-overview.pdf>
* Vivado Design Suite User Guide - Synthesis : <https://www.xilinx.com/support/documentation/sw_manuals/xilinx2019_2/ug901-vivado-synthesis.pdf>
* Vivado Design Suite User Guide - Implementation : <https://www.xilinx.com/support/documentation/sw_manuals/xilinx2019_2/ug904-vivado-implementation.pdf>
