# 🎵 Spotify Lyrics Overlay

Un overlay léger, toujours au premier plan, qui affiche les **paroles synchronisées** du morceau Spotify en cours, avec la barre de progression, la pochette et les commandes de lecture.

**100 % local : aucun compte développeur, aucune clé, aucune connexion à Spotify.** L'overlay lit ce que l'application Spotify affiche déjà dans Windows (le même lecteur multimédia que les touches média de ton clavier). Tu le lances, et ça marche.

> Pour **Windows**, avec l'**application Spotify de bureau**. Fonctionne avec un compte gratuit comme avec un compte Premium.

---

## ✨ Fonctionnalités

- **Paroles synchronisées** via [LRCLIB](https://lrclib.net) (gratuit, sans clé), en mode compact (ligne en cours + suivante) ou étendu (3 ou 5 lignes) avec défilement fluide
- **Barre de progression cliquable** (clic ou glisser pour avancer / reculer)
- **Pochette** en option, et **couleur d'accent** qui s'adapte à la pochette
- **Boutons** : thème, précédent / pause-lecture / suivant, réglages
- **Slider de volume** vertical (clic, glisser ou molette), qui règle le volume de Spotify dans le mélangeur Windows
- **4 thèmes** : sombre, clair, néon, verre dépoli, changeables d'un clic
- **Réactivité au son** (optionnelle) : vrai spectre audio et pulsation de la bordure
- **Icône dans la zone de notification** (la flèche à côté du volume) : afficher / masquer, réglages, quitter
- **Mode verrouillé (clic traversant)** : la souris passe à travers l'overlay (utile par-dessus un jeu ou un navigateur), sauf sur les boutons, le volume et la barre
- Menu clic droit et panneau de réglages dans le style de l'overlay (thème, transparence, taille, décalage des paroles…)
- Position et réglages mémorisés, disparition automatique quand rien ne joue
- Lancement automatique avec Windows (optionnel)

---

## 🚀 Installation

1. Va dans l'onglet **[Releases](../../releases)** de ce dépôt.
2. Télécharge **`SpotifyLyricsOverlay.exe`**.
3. Lance-le, puis lance (ou garde ouverte) l'**application Spotify de bureau**. Rien d'autre à installer ni à configurer.

> **Windows SmartScreen / antivirus** : l'exécutable n'est pas signé numériquement, Windows peut donc afficher « Windows a protégé votre PC ». Clique sur **Informations complémentaires** puis **Exécuter quand même**. Un antivirus peut aussi le signaler à tort (faux positif courant pour ce type de fichier).

### Prérequis

- Windows 10 ou 11
- L'application **Spotify de bureau** (version classique ou Microsoft Store). Le lecteur web dans un navigateur n'est **pas** détecté.

---

## 🎛️ Contrôles

| Action | Effet |
|---|---|
| Pastille ◐ | Changer de thème |
| Boutons ⏮ ⏯ ⏭ | Précédent, pause / lecture, suivant (grisés si Spotify refuse les sauts) |
| Barre de progression | Clic ou glisser : avancer / reculer |
| Slider vertical | Volume de Spotify (clic, glisser ou molette dessus) |
| Icône à droite | Panneau de réglages |
| Clic gauche + glisser (ailleurs) | Déplacer la fenêtre |
| Molette (ailleurs) | Transparence |
| Clic droit | Menu (Réglages, Masquer, Thème, Paroles, Pochette, Verrouiller, Quitter) |
| Icône de notification | Clic gauche : afficher / masquer. Clic droit : menu (dont Verrouiller et Quitter) |
| `Échap` | Quitter |

### Mode verrouillé

Active-le depuis le menu, les réglages ou l'icône de notification. L'overlay laisse alors passer la souris, sauf sur les boutons, le volume et la barre de progression. Pour le déplacer ou le déverrouiller : **clic droit sur l'icône de notification** → décocher *Verrouiller (clic traversant)*.

---

## 💎 Compte gratuit ou Premium

Comme l'overlay passe par Windows et non par l'API Spotify, il n'y a **aucune vérification de compte** : tout est disponible dans l'overlay. Ce sont les règles de Spotify qui s'appliquent ensuite :

- **Sauts limités en gratuit** : Spotify limite les « suivant » / « précédent » des comptes gratuits. Si Spotify ignore un saut, l'overlay grise les boutons ⏮ ⏭ pendant 1 minute et affiche **« Limite de sauts dépassée »**, puis les réactive tout seul.
- **Publicités** : pendant une pub, l'overlay affiche « Publicité en cours » et masque les paroles. Spotify peut bloquer les commandes pendant ce temps.
- **Volume** : il agit sur Spotify dans le mélangeur de volume de Windows (pas sur le curseur interne de Spotify). Spotify doit avoir joué du son au moins une fois pour y apparaître.

---

## 🔊 Réactivité au son (optionnel)

Active le spectre et/ou la pulsation dans les réglages. L'overlay capte la **sortie audio du PC** et ne garde que des niveaux par bande de fréquences en mémoire : aucun enregistrement n'est réalisé ni conservé. L'état de la capture s'affiche dans les réglages.

---

## 💾 Données et vie privée

- Réglages : `%APPDATA%\SpotifyLyricsOverlay\settings.json`
- Journal : `%APPDATA%\SpotifyLyricsOverlay\overlay.log`
- **Aucune connexion à Spotify, aucun jeton, aucun compte.**
- Seule requête réseau : la recherche des paroles chez LRCLIB, avec l'artiste, le titre, l'album et la durée du morceau (et le téléchargement de rien d'autre : la pochette vient de Windows)
- Pour tout réinitialiser, supprime le dossier `SpotifyLyricsOverlay` dans `%APPDATA%`

---

## ❓ Dépannage

- **« Rien en cours de lecture » alors que Spotify joue** : vérifie que c'est bien l'**application de bureau** et non le lecteur web. Lance une musique, puis regarde `overlay.log` : tu dois voir `Lecture locale OK`.
- **« Lecture locale impossible »** : ouvre `overlay.log` et regarde la ligne `SMTC :`, elle indique la cause. Relance Spotify puis l'overlay.
- **Le volume ne bouge pas** : lance un morceau pour que Spotify apparaisse dans le mélangeur de volume Windows.
- **Pas d'icône dans la zone de notification** : elle peut se cacher sous la flèche `^` à côté du volume.
- **Pas de spectre audio** : regarde le message affiché dans les réglages, sous *Réactivité au son*.
- **Paroles introuvables ou décalées** : toutes les chansons n'ont pas de paroles synchronisées sur LRCLIB. Ajuste le *décalage des paroles* dans les réglages.
- **Anciennes versions** : le fichier `.spotify_cache` de l'ancien dossier de réglages n'est plus utilisé, tu peux le supprimer.

---

## 🙏 Crédits

- Paroles : [LRCLIB](https://lrclib.net)
- Lecture et contrôle : lecteur multimédia de Windows (SMTC)

Fait par **JulesFR**.

> Ce projet n'est ni affilié ni approuvé par Spotify.
