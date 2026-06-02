# 🎵 MusikFlow — Application de Streaming Musical

Une application web de streaming musical moderne, inspirée de Deezer et Spotify, construite en HTML, CSS et JavaScript Vanilla.

![MusikFlow Preview](https://img.shields.io/badge/Status-Live-brightgreen) ![HTML](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white) ![CSS](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

---

## 🚀 Fonctionnalités

### 🎧 Lecture musicale
- Lecture de previews 30 secondes via l'API iTunes
- Lecture / Pause, Piste suivante / précédente
- Mode aléatoire (shuffle) et répétition
- Barre de progression cliquable
- Contrôle du volume
- Passage automatique à la piste suivante

### 🔍 Recherche
- Recherche en temps réel (debounce 420ms)
- Historique des recherches (sauvegardé en LocalStorage)
- Suggestions lors du focus sur la barre de recherche

### 📂 Navigation
| Section | Description |
|---|---|
| 🏠 Accueil | Recommandations du moment |
| 🔥 Top Charts | Top 50 France (RSS iTunes) |
| ✨ Nouveautés | Dernières sorties 2025 |
| 🎤 Artistes | Artistes populaires |
| 💿 Albums | Albums tendances |
| ❤️ Favoris | Titres sauvegardés |
| 🕓 Historique | Titres récemment écoutés |
| 🎵 Genres | Pop, Hip-Hop, Rock, Électronique, Jazz, R&B, Classique |

### ❤️ Favoris
- Ajout / suppression depuis les cartes ou le lecteur
- Badge compteur en temps réel dans la sidebar
- Persistance via LocalStorage

### 🎨 Interface
- Design **Glassmorphism** moderne
- Mode **sombre / clair** avec persistance
- Animations fluides (fade-in, hover, equalizer)
- **Skeleton loading** pendant le chargement
- Notifications toast pour chaque action
- Disc animé dans le Hero qui tourne pendant la lecture

### 📱 Responsive
- Desktop, tablette et mobile
- Menu burger sur mobile
- Grille adaptative (CSS Grid auto-fill)

### ⌨️ Raccourcis clavier
| Touche | Action |
|---|---|
| `Espace` | Lecture / Pause |
| `→` | Piste suivante |
| `←` | Piste précédente |

---

## 📁 Structure des fichiers

```
musikflow/
├── index.html     # Structure HTML sémantique
├── style.css      # Design glassmorphism + responsive
├── script.js      # Logique JavaScript modulaire
└── README.md      # Documentation
```

---

## 🌐 API utilisée

### iTunes Search API
L'application utilise l'**iTunes Search API** d'Apple (gratuite, sans clé requise, CORS compatible).

| Endpoint | Usage |
|---|---|
| `https://itunes.apple.com/search` | Recherche de titres |
| `https://itunes.apple.com/fr/rss/topsongs/limit=50/json` | Top 50 France |
| `https://itunes.apple.com/lookup?id=` | Récupération du preview d'un titre |

**Format d'une piste :**
```json
{
  "id": "123456",
  "title": "Nom du titre",
  "artist": "Nom de l'artiste",
  "album": "Nom de l'album",
  "cover": "https://is1-ssl.mzstatic.com/...300x300.jpg",
  "preview": "https://audio-ssl.itunes.apple.com/...preview.m4a",
  "genre": "Pop"
}
```

---

## 💾 LocalStorage

| Clé | Contenu |
|---|---|
| `mf_favorites` | Tableau des titres favoris |
| `mf_history` | Historique des 50 derniers titres écoutés |
| `mf_search_history` | 8 dernières recherches |
| `mf_theme` | Thème actif (`dark` ou `light`) |

---

## 🛠️ Lancer le projet

### Option 1 — Replit
Le projet est directement exécutable sur Replit. Cliquer sur **Run**.

### Option 2 — Serveur local (Python)
```bash
python3 -m http.server 5000
```
Puis ouvrir `http://localhost:5000`

### Option 3 — Serveur local (Node.js)
```bash
npx serve .
```

> **Note :** L'application doit être servie via HTTP (pas en ouvrant directement `index.html`) pour que les appels API CORS fonctionnent correctement.

---

## 🏗️ Architecture JavaScript

```
state{}           — État global de l'application
  tracks[]        — Liste des pistes en cours
  currentIndex    — Index de la piste active
  favorites[]     — Favoris (sync LocalStorage)
  history[]       — Historique d'écoute
  searchHistory[] — Historique de recherche

API
  searchTracks()    — Recherche iTunes
  fetchTopCharts()  — Top 50 RSS iTunes
  enrichPreview()   — Récupère le preview d'un titre RSS

Vues
  loadView(view)    — Charge une vue nommée
  loadGenre(genre)  — Charge un genre musical
  loadSearch(query) — Lance une recherche

Lecteur
  playTrack(index)  — Joue la piste à l'index
  togglePlay()      — Lecture / Pause
  playNext()        — Piste suivante (shuffle aware)
  playPrev()        — Piste précédente

UI
  renderGrid()      — Affiche la grille de musiques
  renderArtists()   — Affiche la rangée d'artistes
  showSkeletons()   — Squelettes de chargement
  notify()          — Toast de notification
```

---

## 📸 Aperçu

| Fonctionnalité | Détail |
|---|---|
| Hero animé | Disque rotatif synchronisé avec la lecture |
| Cartes | Overlay play + bouton favori au hover |
| Equalizer | Barres animées sur la carte en lecture |
| Player | Barre de progression, volume, shuffle, repeat |
| Sidebar | Navigation complète + 7 genres |

---

## 📄 Licence

Projet libre — utilisation personnelle et éducative.
Les previews audio appartiennent à Apple / iTunes.