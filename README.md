# 🎵 Spotify Lyrics Overlay

Un overlay léger, toujours au premier plan, qui affiche les **paroles synchronisées** du morceau Spotify en cours, avec la barre de progression, la pochette et les commandes de lecture.

Aucune clé n'est fournie : chacun crée sa propre application Spotify (2 minutes, un assistant intégré t'explique comment).

> Pour **Windows**.

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

---

## 🚀 Installation

1. Va dans l'onglet **[Releases](../../releases)** de ce dépôt.
2. Télécharge **`SpotifyLyricsOverlay.exe`**.
3. Lance-le. Rien d'autre à installer : tout est inclus.

> **Windows SmartScreen / antivirus** : l'exécutable n'est pas signé numériquement, Windows peut donc afficher « Windows a protégé votre PC ». Clique sur **Informations complémentaires** puis **Exécuter quand même**. Un antivirus peut aussi le signaler à tort (faux positif courant pour ce type de fichier).

---

## 🔑 Premier lancement : créer ton application Spotify

Spotify demande une « application » personnelle pour lire le morceau en cours. C'est une clé d'accès, rien n'est publié. Une fenêtre te guide, en résumé :

1. Ouvre le [dashboard développeur Spotify](https://developer.spotify.com/dashboard) et connecte-toi.
2. Clique sur **Create app** et remplis :
   - **App name** : `Lyrics Overlay`
   - **Redirect URI** : `http://127.0.0.1:8888/callback` (puis **Add**)
   - **API/SDKs** : coche uniquement **Web API**
3. Ouvre **Settings** de ton app, copie le **Client ID** (pas le Client secret) et colle-le dans la fenêtre.

Le Client ID est mémorisé ensuite.

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

Active-le depuis le menu, les réglages ou l'icône de notification. L'overlay laisse alors passer la souris, sauf sur les boutons, le volume et la barre de progression. Pour le déplacer ou le déverrouiller : **clic droit sur l'icône de notification** → décocher *Verrouiller (clic traversant)*.

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

Active le spectre et/ou la pulsation dans les réglages. L'overlay capte la **sortie audio du PC** et ne garde que des niveaux par bande de fréquences en mémoire : aucun enregistrement n'est réalisé ni conservé. L'état de la capture s'affiche dans les réglages.

---

## 💾 Données et vie privée

- Réglages : `%APPDATA%\SpotifyLyricsOverlay\settings.json`
- Connexion Spotify : jeton mis en cache dans le même dossier (aucun Client secret n'est utilisé)
- Paroles : requêtes envoyées à LRCLIB avec l'artiste, le titre, l'album et la durée du morceau
- Pour tout réinitialiser, supprime ce dossier, ou utilise *Changer d'application Spotify…* dans les réglages

---

## ❓ Dépannage

- **« Erreur Spotify : vérifie le Client ID »** : le Client ID est faux ou la Redirect URI ne correspond pas exactement à `http://127.0.0.1:8888/callback`. Corrige-les via *Changer d'application Spotify…* dans les réglages.
- **Le navigateur s'ouvre pour autoriser Spotify** : normal au premier lancement, et une fois après une mise à jour qui change les permissions.
- **Pas d'icône dans la zone de notification** : elle peut se cacher sous la flèche `^` à côté du volume.
- **Pas de spectre audio** : regarde le message affiché dans les réglages, sous *Réactivité au son*.
- **Paroles introuvables ou décalées** : toutes les chansons n'ont pas de paroles synchronisées sur LRCLIB. Ajuste le *décalage des paroles* dans les réglages.

---

## 🙏 Crédits

- Paroles : [LRCLIB](https://lrclib.net)
- Lecture et contrôle : [Spotify Web API](https://developer.spotify.com/documentation/web-api)

Fait par **JulesFR**.

> Ce projet n'est ni affilié ni approuvé par Spotify.