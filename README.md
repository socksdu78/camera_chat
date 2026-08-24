# Meowmeow cat cam — détecteur de mèmes

Pointe ta webcam vers toi, fais un geste ou une expression, et reçois un mème de chat en temps réel. Fonctionne soit en application bureau (fenêtres OpenCV) soit entièrement dans le navigateur (MediaPipe WASM, aucune installation).

Deux volets côte à côte :
- **Caméra** — ton flux webcam avec les repères de main superposés, plus un affichage de débogage en direct dans le coin
- **Mème** — le mème correspondant au geste que tu es en train de faire

## Gestes

Vérifiés dans cet ordre — quand une pose peut correspondre à plusieurs, le premier l'emporte.

| # | Geste | Comment le déclencher |
|---|---|---|
| 1 | Muehehe | Les deux mains levées, index seulement, bouts des doigts qui se touchent |
| 2 | Chat qui a peur | Les deux mains levées, au-dessus de la tête |
| 3 | Chat qui mâche un câble | Les deux mains levées de chaque côté du visage comme pour tenir un câble |
| 4 | Je vais te frapper | Une main, les quatre doigts repliés en poing |
| 5 | EHHEHEEEHEEEE | Pouce + auriculaire écartés, rockstar cat |
| 6 | Chat silencieux (chut) | Index seulement, bout du doigt posé sur la bouche |
| 7 | Chat nerd | Index seulement, éloigné du visage |
| 8 | Chat choqué/kidnappé | Main qui couvre la bouche |
| 9 | DONNE-MOI DES SOUS !! | Une paume ouverte, tous les doigts étendus, loin du visage |
| 10 | Chat regard de côté | Tourne la tête de 15°+ dans un sens ou l'autre |
| 11 | Pokercat | Par défaut |
| 12 | Chat tournoyant OIIAI | Tu tournes !!!! |

Les images de mèmes se trouvent dans `memes/`. Certains gestes choisissent aléatoirement parmi plusieurs images.

## Lancer — navigateur (GitHub Pages)

Aucune installation nécessaire. Ouvre simplement l'URL du site et autorise l'accès à la webcam. Les modèles se chargent depuis le CDN MediaPipe de Google au démarrage.

## Lancer — bureau (Python)

Nécessite Python 3 et une webcam.

    python3 -m venv .venv
    source .venv/bin/activate  # Windows : .venv\Scripts\activate
    pip install -r requirements.txt
    python3 gesture_meme.py

Appuie sur `q` ou `Esc` dans la fenêtre Caméra pour quitter.

## HUD de débogage

La fenêtre Caméra affiche toujours un petit indicateur en haut à gauche :

    geste : regard de côté
    rotation : +18.4°  (side-eye +/-15.0)

Utile pour ajuster les seuils de détection en haut de `gesture_meme.py` / `app.js` si un geste se déclenche trop facilement ou pas assez selon ton setup/éclairage.

## Structure du projet

    gesture_meme.py   version bureau (OpenCV + MediaPipe Python tasks API)
    app.js            version navigateur (MediaPipe tasks-vision WASM)
    index.html        interface navigateur
    memes/            images de mèmes (+ une vidéo, inutilisée pour l'instant)
    models/           fichiers modèles MediaPipe .task pour la version bureau
    requirements.txt  dépendances Python
