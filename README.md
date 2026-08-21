# 🐇 Mon Lièvre

**Compagnon d'entraînement course à pied & trail — 100 % local, hors-ligne, sans compte.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

Mon Lièvre est une Progressive Web App (PWA) qui construit et adapte ton plan d'entraînement selon une méthodologie polarisée 80/20, sans jamais faire sortir tes données de ton appareil — sauf si tu actives, volontairement, un Coach IA basé sur l'API Claude (BYOK : *Bring Your Own Key*, tu utilises ta propre clé).

- **Aucun compte, aucun serveur, aucun cloud.** Tout tourne et est stocké sur ton appareil (`localStorage`).
- **Fonctionne hors-ligne** une fois chargée (Service Worker + manifeste PWA), installable comme une app.
- **Moteur d'entraînement local** : calcul de charge, ACWR, monotonie, adaptation du plan — sans IA.
- **Coach IA optionnel** : réponses personnalisées via l'API Claude (Anthropic), activé uniquement si tu ajoutes ta propre clé API.
- **Import multi-montres** : fichiers `.fit` (Garmin / Polar / Wahoo / Suunto), `.gpx`, `.tcx`, ou archive Strava (`.zip`) — tout est lu et traité en local, sans connexion à un compte tiers.
- **Code source unique et lisible** : une seule page (`index.html`), JavaScript vanilla, sans dépendance ni build.

## Sommaire

- [Démarrer](#démarrer)
- [Activer le Coach IA (optionnel)](#activer-le-coach-ia-optionnel)
- [Importer tes activités](#importer-tes-activités)
- [Tes données et vie privée](#tes-données-et-vie-privée)
- [Documentation du projet](#documentation-du-projet)
- [Pour les développeurs](#pour-les-développeurs)
- [Licence](#licence)

## Démarrer

Trois façons d'utiliser Mon Lièvre, de la plus simple à la plus complète :

### 1. En ligne (recommandé)

Ouvre directement l'app à cette adresse : **[à compléter — lien GitHub Pages]**
→ Fonctionne hors-ligne après un premier chargement, installable sur mobile (« Ajouter à l'écran d'accueil ») et sur ordinateur.

### 2. En local, sans rien installer

Télécharge ou clone ce dépôt, puis ouvre `index.html` dans ton navigateur : l'app est pleinement fonctionnelle ainsi (tes données restent dans le `localStorage` de ton navigateur). Seuls le mode hors-ligne complet et l'installation en PWA nécessitent de servir les fichiers via un petit serveur local plutôt que de les ouvrir en `file://` :

```bash
git clone https://github.com/<ton-compte>/<ton-repo>.git
cd <ton-repo>
python3 -m http.server 8080
# puis ouvre http://localhost:8080
```

### 3. Héberger ta propre instance

Le projet ne nécessite aucun backend : n'importe quel hébergeur de fichiers statiques convient (GitHub Pages, Netlify, Cloudflare Pages…). Il suffit de déployer le contenu du dépôt tel quel.

## Activer le Coach IA (optionnel)

Par défaut, Mon Lièvre fonctionne en **mode local gratuit** : le moteur intégré adapte ton plan sans aucune IA. Si tu veux pouvoir discuter avec un Coach qui connaît ton contexte (charge, objectif, ressenti…), tu peux activer le **mode Coach IA** avec ta propre clé API Claude :

1. Crée un compte sur la [Claude Console](https://console.anthropic.com)
2. Génère une clé API
3. Colle-la dans **Réglages → Clé API** de l'app
4. Choisis ton modèle (Sonnet 4.6 ou Haiku 4.5, selon ton budget)

Le guide illustré pas-à-pas (création du compte, génération et suppression de la clé, suppression des données…) est disponible dans **[`Tuto_éveil_du_Lièvre.pdf`](./Tuto_éveil_du_Lièvre.pdf)**.

⚠️ Ta clé API est facturée directement par Anthropic à l'usage (voir leurs [tarifs](https://www.anthropic.com/pricing)) ; Mon Lièvre ne prend aucune commission et ne voit jamais ta clé transiter ailleurs que dans ton propre navigateur.

Tu peux désactiver le Coach IA et revenir au mode local à tout moment en supprimant la clé dans les réglages — tes données d'entraînement sont conservées.

## Importer tes activités

Mon Lièvre lit directement les formats exportés par les montres et plateformes courantes — sans jamais se connecter à un compte tiers :

| Format | Sources typiques |
|---|---|
| `.fit` | Garmin, Polar, Wahoo, Suunto |
| `.gpx` / `.tcx` | Export individuel, depuis n'importe quelle plateforme |
| `.zip` (archive Strava) | Export « Toutes mes données » de Strava |

Import possible fichier par fichier, ou en une fois via une archive `.zip`. Tout le traitement (lecture, dé-duplication) se fait localement dans le navigateur.

## Tes données et vie privée

**En une phrase : par défaut, rien ne quitte ton appareil.** La seule information qui sort de ton navigateur est celle envoyée à l'API Claude si tu choisis d'activer le Coach IA — et uniquement ce qui est nécessaire pour répondre à ta question, au moment où tu la poses.

Le détail complet (ce qui est transmis, ce qui ne l'est jamais, et pourquoi) est expliqué sans jargon dans **[`Mon_Lièvre_données_et_API.pdf`](./Mon_Lièvre_données_et_API.pdf)**.

## Documentation du projet

| Document | Pour qui ? | Contenu |
|---|---|---|
| **[Mon_Lièvre_données_et_API.pdf](./Mon_Lièvre_données_et_API.pdf)** | Tout le monde | Ce qui est stocké, ce qui est transmis à l'IA, ce qui ne l'est jamais — écrit sans jargon. |
| **[Tuto_éveil_du_Lièvre.pdf](./Tuto_éveil_du_Lièvre.pdf)** | Qui veut activer le Coach IA | Guide pas-à-pas : créer un compte Claude Console, générer / ajouter / supprimer une clé API, supprimer les données de l'app. |
| **[Mon_Lièvre__Méthodologie.pdf](./Mon_Lièvre__Méthodologie.pdf)** | Coureurs curieux & développeurs | Système de charge (ACWR, monotonie), logique du moteur de programme, lecture des indicateurs — texte pédagogique + blocs techniques détaillés. |
| **[Questions_réponses.md](./Questions_réponses.md)** | Développeurs / contributeurs | Base de connaissances qui alimente les réponses du Coach IA (méthodologie, matériel, nutrition, récupération, psychologie, santé). |
| **[Mon_Lievre_Coach_BYOK_Cahier_des_charges_docx.pdf](./Mon_Lievre_Coach_BYOK_Cahier_des_charges_docx.pdf)** | Développeurs / contributeurs | Cahier des charges du Coach & du mode BYOK — document de conception pour de futures évolutions, pas encore implémenté. |

## Pour les développeurs

- **Techno** : JavaScript vanilla, une seule page (`index.html`, ~3700+ lignes), aucune dépendance externe, aucun build.
- **Stockage** : tout l'état de l'app dans une seule clé `localStorage` (`monlievre.state.v1`).
- **Hors-ligne** : `sw.js` (Service Worker, cache-first) + `manifest.webmanifest` pour l'installation en PWA.
- **IA** : appels directs au endpoint `/v1/messages` de l'API Anthropic depuis le navigateur (`anthropic-dangerous-direct-browser-access`), aucun serveur intermédiaire.
- **Constantes à personnaliser** en tête de `index.html` si tu forkes le projet : `DOCS_URL` (lien vers le guide d'installation du coach), `PRIVACY_URL` (lien vers la doc données & IA), `DONATE_URL` (optionnel).
- `planche-pictogrammes.html` est un outil interne de validation visuelle (palette de couleurs par famille de séance) — pas une page destinée aux utilisateurs finaux.

Contributions, suggestions et retours bienvenus via les *issues* du dépôt.

## Licence

Distribué sous licence **MIT** — voir [`LICENSE`](./LICENSE).
