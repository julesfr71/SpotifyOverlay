# 🎵 Spotify Lyrics Overlay

Un overlay léger, toujours au premier plan, qui affiche les **paroles synchronisées** du morceau Spotify en cours, avec la barre de progression, la pochette et les commandes de lecture.

Pas de clé à partager : chacun crée sa propre application Spotify (2 minutes, un assistant intégré t'explique comment).

> Conçu pour **Windows**. Le cœur de l'overlay fonctionne aussi sous Linux, mais le lancement automatique, le clic traversant et la compilation `.exe` sont propres à Windows.

---

## ✨ Fonctionnalités

- **Paroles synchronisées** via [LRCLIB](https://lrclib.net) (gratuit, sans clé), en mode compact (ligne en cours + suivante) ou étendu (3 ou 5 lignes) avec défilement fluide
- **Barre de progression cliquable** (clic ou glisser pour avancer / reculer)
- **Pochette** en option, et **couleur d'accent** qui s'adapte à la pochette
- **Boutons** : like (animation « + » → coche verte), thème, précédent / pause-lecture / suivant, réglages
- **Slider de volume** vertical (clic, glisser ou molette)
- **4 thèmes** : sombre, clair, néon, verre dépoli, changeables d'un clic
- **Réactivité au son** (optionnelle) : vrai spectre audio et pulsation de la bordure
- **Icône dans la zone de notification** (la flèche à côté du volume) : afficher / masquer, réglages, quitter
- **Mode verrouillé (clic traversant)** : la souris passe à travers l'overlay (utile par-dessus un jeu ou un navigateur), sauf sur les boutons, le volume et la barre
- **Compte gratuit géré** : les commandes réservées au Premium sont grisées au lieu d'afficher une erreur
- Menu clic droit et panneau de réglages dans le style de l'overlay (thème, transparence, taille, décalage des paroles…)
- Position et réglages mémorisés, disparition automatique quand rien ne joue
- Lancement automatique avec Windows (optionnel)
- **Installation automatique** des modules Python manquants au premier lancement

---

## 🚀 Installation

### Option 1 : le `.exe` (le plus simple)

Télécharge `SpotifyLyricsOverlay.exe` depuis l'onglet **Releases** et lance-le. Rien d'autre à installer.

> Un antivirus peut parfois signaler un `.exe` PyInstaller non signé : c'est un faux positif courant. Tu peux aussi le compiler toi-même (voir plus bas).

### Option 2 : le script Python

1. Installe [Python](https://www.python.org/downloads/) (coche « Add Python to PATH »).
2. Télécharge ce dépôt et garde ces fichiers dans le **même dossier** : `spotify_lyrics_overlay.py` et `tray_icon.py`.
3. Lance :

```bash
python spotify_lyrics_overlay.py
```

Au premier lancement, les modules manquants (`spotipy`, `requests`, `pillow`, `numpy`, `pyaudiowpatch`, `pystray`) s'installent tout seuls avec pip. Sur Windows, le script se relance sans fenêtre de console ; ajoute `--console` pour la garder (débogage).

Équivalent manuel :

```bash
pip install spotipy requests pillow numpy pyaudiowpatch pystray
```

---

## 🔑 Premier lancement : créer ton application Spotify

Spotify demande une « application » personnelle pour lire le morceau en cours. C'est une clé d'accès, rien n'est publié. Une fenêtre te guide, en résumé :

1. Ouvre le [dashboard développeur Spotify](https://developer.spotify.com/dashboard) et connecte-toi.
2. Clique sur **Create app** et remplis :
   - **App name** : `Lyrics Overlay`
   - **Redirect URI** : `http://127.0.0.1:8888/callback` (puis **Add**)
   - **API/SDKs** : coche uniquement **Web API**
3. Ouvre **Settings** de ton app, copie le **Client ID** (pas le Client secret) et colle-le dans la fenêtre.

Le Client ID est mémorisé ensuite. Aucune clé n'est écrite dans le code, tu peux partager le fichier tel quel.

> D'après l'assistant intégré, depuis 2026 le compte Spotify qui crée l'application doit être **Premium**. Vérifie les conditions actuelles sur le dashboard.

---

## 🎛️ Contrôles

| Action | Effet |
|---|---|
| `+` / coche | Ajouter / retirer le titre des titres likés |
| Pastille ◐ | Changer de thème |
| Barre de progression | Clic ou glisser : avancer / reculer |
| Slider vertical | Volume (clic, glisser ou molette dessus) |
| Icône à droite | Panneau de réglages |
| Clic gauche + glisser (ailleurs) | Déplacer la fenêtre |
| Molette (ailleurs) | Transparence |
| Clic droit | Menu (Réglages, Masquer, Thème, Paroles, Pochette, Verrouiller, Quitter) |
| Icône de notification | Clic gauche : afficher / masquer. Clic droit : menu (dont Verrouiller et Quitter) |
| `Échap` | Quitter |

### Mode verrouillé

Active-le depuis le menu, les réglages ou l'icône de notification. L'overlay laisse alors passer la souris, sauf sur les boutons, le volume et la barre de progression. Pour le déplacer ou le déverrouiller : **clic droit sur l'icône de notification** → décocher *Verrouiller (clic traversant)*. Sans icône de notification, le verrouillage est refusé pour ne jamais te bloquer.

---

## 💎 Compte gratuit ou Premium

Les paroles, le titre, la pochette, la barre en lecture seule, le like et le spectre audio marchent avec n'importe quel compte. Les **commandes de lecture** de l'API Spotify sont, elles, réservées au Premium :

| Fonction | Gratuit | Premium |
|---|:---:|:---:|
| Titre, artiste, pochette, couleur d'accent | ✅ | ✅ |
| Paroles synchronisées | ✅ | ✅ |
| Like / unlike | ✅ | ✅ |
| Spectre audio, pulsation | ✅ | ✅ |
| Pause / lecture, suivant, précédent | ❌ | ✅ |
| Volume | ❌ | ✅ |
| Clic sur la barre pour avancer / reculer | ❌ | ✅ |

Avec un compte gratuit, ces boutons sont grisés et affichent « Réservé aux comptes Premium ».

---

## 🔊 Réactivité au son (optionnel)

Active le spectre et/ou la pulsation dans les réglages. L'overlay capte la **sortie audio du PC** (loopback) et ne garde que des niveaux par bande de fréquences en mémoire : aucun enregistrement.

| Système | Module |
|---|---|
| Windows | `numpy` + `pyaudiowpatch` |
| Linux | `numpy` + `soundcard` |
| macOS | `numpy` + `soundcard` + un périphérique virtuel (ex. BlackHole) |

---

## 🛠️ Compiler le `.exe` toi-même

Sur Windows, avec Python installé, mets dans le même dossier `spotify_lyrics_overlay.py`, `tray_icon.py`, `make_icon.py` et `build_exe.bat`, puis double-clique sur **`build_exe.bat`**.

Il installe les modules, génère l'icône et compile avec PyInstaller. Le résultat est dans `dist\SpotifyLyricsOverlay.exe`.

---

## 💾 Données et vie privée

- Réglages : `%APPDATA%\SpotifyLyricsOverlay\settings.json` (Linux : `~/.config/spotify-lyrics-overlay/`)
- Connexion Spotify : jeton PKCE mis en cache dans le même dossier (aucun Client secret n'est utilisé)
- Paroles : requêtes envoyées à LRCLIB avec l'artiste, le titre, l'album et la durée du morceau
- Pour tout réinitialiser, supprime ce dossier, ou utilise *Changer d'application Spotify…* dans les réglages

---

## ❓ Dépannage

- **« Erreur Spotify : vérifie le Client ID »** : le Client ID est faux ou la Redirect URI ne correspond pas exactement à `http://127.0.0.1:8888/callback`. Corrige-les via *Changer d'application Spotify…* dans les réglages.
- **Le navigateur s'ouvre à chaque mise à jour** : normal après un changement de permissions (une nouvelle autorisation est demandée une fois).
- **Pas d'icône dans la zone de notification** : vérifie que `pystray` est installé (`pip install pystray`). Elle peut aussi se cacher sous la flèche `^`.
- **Pas de spectre audio** : installe les modules de la section « Réactivité au son » ; l'état de la capture s'affiche dans les réglages.
- **Paroles introuvables ou décalées** : tout le monde n'a pas de paroles synchronisées sur LRCLIB. Ajuste le *décalage des paroles* dans les réglages.

---

## 🙏 Crédits

- Paroles : [LRCLIB](https://lrclib.net)
- Lecture et contrôle : [Spotify Web API](https://developer.spotify.com/documentation/web-api) via [spotipy](https://github.com/spotipy-dev/spotipy)
- Icône de notification : [pystray](https://github.com/moses-palmer/pystray)

Fait par **JulesFR**.

> Ce projet n'est ni affilié ni approuvé par Spotify.
