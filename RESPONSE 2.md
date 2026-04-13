# BabyEPITACTF - Response

## Authentification 1

### [ch-11] [EASY]

Il faut juste tester le mot de passe basic:

admin / admin

### [ch-12] [EASY]

Il faut regarder dans le code source de la page et chercher le test d'authentification:

admin / TheMoreSecureNumberIs42!!!

### [ch-13] [MEDIUM]

Il faut regarder dans le code source de la page et lire le commentaire pour comprendre comment trouver le mot de passe (aller sur [Dcode](https://www.dcode.fr/md5-hash) et encypter "EPITA" en md5 puis coller le resultat)).

the_boss / ea755ea897a1ff1269db3d16d2b8a57c
#### changer pour accepter Epita et epita


### [ch-14] [EASY]

Il faut faire un scan du QRCode avec une application mobile par exemple et regarder le texte qui est représenté par le QRCode:
(ne marche pas sur Iphone/ telecharger le qr code et essayer sur [QR Reader Online](https://qrscanner.net/) ou autre site)
student / EpitaRox

### [ch-15][EASY MAIS LONG]

Il faut reconstituer le QRCode. Pour cela, il existe des applications en ligne pour le faire progressivement et obtenir un QRCode valide que l'on peut lire avec le téléphone.

Exemple de site pour refaire le QRCode: https://merri.cx/qrazybox/   (une fois sur le site : New Project -> New Blank QR Code )

{MyFlag42}

## Authentification 2

### [ch-21] [EASY]

Il faut regarder sous le clavier, il y a un post-it avec le mot de passe.
Attention, il faut bien avoir mis le post-it lors de l'installation de l'atelier (uniquement en JI et pas JPO).

Gertrude / I-love-my-cat

### [ch-22] [EASY]

Il faut regarder sur les tableaux de la salle de l'atelier.
Il faut avoir écrit préalablement le nom d'utilisateur et le mot de passe sur les tableaux de la salle .

Tom / le_beau_gosse_91

### [ch-23] [EASY]

Il faut regarder sur les posters dans la salle de l'atelier.
Il faut avoir au préalable bien entourer ou écrit les mots "EPITA" et "informatique" sur des posters présents dans la salle.
La case (minuscule / majuscule) n'a pas d'importance.

EPITA / informatique

### [ch-24 / disable pour le moment]

mot de passe sur t-shirt encadrant: user devant, mdp derrière

### [ch-25] [MEDIUM]

Il faut décoder le texte par rot13.
On peut, par exemple, utiliser le site http://rot13.com :

caesar / empereur

### [ch-26][MEDIUM]

Il faut décoder le texte via le vigenaire.
Le site [Dcode](http://www.dcode.fr/) va fournir tous les outils pour l'opération.

- 1) La clef n'est pas connu, il faut faire une attaque stastistique pour déduire la taille de la clef (9 charactères) avec "Cryptanalyse de Vigenere (Test de Kasiski)"
- 2) Avec des tentatives succéssives sur la taille de la clef ("Avec la longueur/taille de la clé, nombre de lettres"), on arrive à décoder tout le texte (avec une clef de taille 9)
- 3) La dernière partie du texte nous fait trouver le nom d'utilisateur "turing"
- 4) Avec la suite du texte, on peut déduire que le mot de passe est "von Neumann"

turing / von Neumann

#### retirer le cote case sensitive

## Stéganographie

### [ch-31] [EASY]

Il faut bien zoomer sur l'image pour trouver::
- sur l'écran, dans le navigateur, dans la zone de saisie du user: louanne
- sur le post-it en dessous de l'écran le mot de passe: CanvaCestTop

louanne / CanvaCestTop

### [ch-32] [EASY]

Sur l'image, il y a un code barre de visible sur la carte "Admin" sur la caisse.

Pour avoir une bonne visibilité, il faut zoomer sur l'image (on peut l'ouvrir dans un onglet).
Avec une application Android comme "Barcode Scanner", on peut lire le code barre et trouver le code écrit.

Attention, le code est petit sur l'image et il va peut-être falloir s'y prendre à plusieurs reprises pour avoir le bon code.

Le code correspond au code barre d'un sachet de café en grain, c'est donc possible que l'applicaiton mobile vous affiche le café correspondant; ce n'est pas grave du tout, ce que l'on souhaite c'est la suite de chiffre représenté par le code barre.

8000070063334

### [ch-33][MEDIUM]

Il faut regarder les métadonnées de l'image et chercher dans la partie "comment".
Vous pouvez utilsier un site web pour extraire les informations. Par exemple: [aperisolve](https://www.aperisolve.com/) ou exiftool dans le terminal sur linux


MarcLaPhoto35 / photo42$bzh

### [ch-34 / disable][HARD]

Il faut regarder les 1er pixel de l'image, le code est dans la suite de 0-1.
La 1ère ligne par exemple, toujours en morse, blanc noir ?

### [ch-35]   /// CONNAIS PAS

Il faut décoder le morse que l'on attends dans le fichier audio en cliquant sur le gros bouton sous le logo EPITA.

Il faut des écouteurs pour ce challenge ou bien on peut entendre le son avec des écrans récents (les écrans en format panoramique
avec des enceintes intégrées) dans les salles machines mais ça va vite être très bruyant dans la salle.

Pour activiter le son sur le NUC et entendre le fichier audio, il faut utiliser la commande "pavucontrol" dans un terminal.

Encore plus malin, sur certains sites, on peut charger le fichier wav pour lire l'audio et avoir un déchiffrement
automatique et voir apparaître le message en clair.
Par exemple: https://morsecode.world/

marie / sport42

### [ch-36 / disable]  /// CONNAIS PAS

Il faut faire une analyse frequencielle de l'audio (exemple sous Spectrum Analyzer sous Android) pour trouver le code morse présent.

## Injection SQL

### [ch-41] [HARD]

#### Solution

Il faut faire une injection SQL au niveau du user en réduisant la recherche.

En user, vous pouvez mettre :  admin' or 1 = 1; --
Peut importe le mot de passe

#### Explication

Si l'on regarde le code source html et le log, une requête classque va donner:

"SELECT * FROM users WHERE login = 'XXX' AND mdp = 'XXX'"

Avec le user / mdp indiqué au dessus, ça donne:

"SELECT * FROM users WHERE login = 'admin' or 1 = 1; --' AND mdp = 'XXX'"

En retirant la fin ('--' indique que le reste est du commentaire), ça donne:

"SELECT * FROM users WHERE login = 'admin' or 1 = 1;"

Ce qui donne donc toujours un résultat puisque "1 = 1" est vrai.


## Binaire

### [ch-51] [HARD]  // FAISABLE LINUX UNIQUEMENT

Il faut faire la commande strings sur le binaire pour trouver le mot de passe.

Attention, sur le NUC, il faut penser à faire un chmod +x sur le binaire.

### [ch-52][ VERY HARD]   // FAISABLE LINUX UNIQUEMENT

Il faut analyser le code asm du binaire pour trouver le je à changer en jne (ou l'inverse) dans le binaire afin de passer outre la vérification du mot de passe.

Attention, sur le NUC, il faut penser à faire un chmod +x sur le binaire.

## OSINT

### [ch-61]

Il faut retrouver la porte KB1 du site EPITA Kremlin-bicêtre sur le site https://what3words.com/

Emplacement : https://what3words.com/ricanant.palabrer.virant

Note : ne pas oublier de passer l'interface du site en francais