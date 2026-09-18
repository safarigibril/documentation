# Documentation XERA1

Ce dossier contient désormais la documentation autonome du produit XERA1, conçue pour un site dédié type docs.xera1.xyz.

## Objectif

La documentation a été nettoyée pour se concentrer sur le vrai fonctionnement de XERA1 :

- preuve d'exécution plutôt qu'un simple CV,
- parcours utilisateur guidé de A à Z,
- onboarding, pages PRO, messagerie, feed immersif, recherche et vérification,
- contenu pratique, moderne et orienté action.

## Nouvelle architecture

- `docs.html` : page d'accueil de documentation et point d'entrée du site.
- `getting-started.html` : onboarding, compte, première preuve et certification.
- `pro-pages.html` : configuration des pages professionnelles et CTA.
- `messaging-and-network.html` : messagerie et interactions B2B/B2C.
- `search-and-discovery.html` : feed immersif et commande de recherche.
- `trust-and-verification.html` : badge, provenance media, sécurité.
- `styles.css` : design dark mode minimaliste du site.
- `docs-app.js` : nav, recherche rapide et interactions UI.

## Lancer la doc localement

Depuis la racine du projet, après avoir configuré la clé Gemini dans l'environnement du serveur :

```bash
cp .env.example .env
# Renseignez GEMINI_API_KEY dans .env, puis lancez :
node local-server.js
```

Puis ouvrez :

```text
http://localhost:3000/docs.html
```

La clé reste côté serveur et n'est jamais envoyée au navigateur. En production, configurez `GEMINI_API_KEY` dans le gestionnaire de secrets de la plateforme plutôt que dans un fichier commité.

## Déployer sur Vercel

1. Importez ce dépôt dans Vercel.
2. Dans **Settings > Environment Variables**, ajoutez `GEMINI_API_KEY` avec une nouvelle clé Gemini, pour les environnements nécessaires (`Production`, `Preview` et éventuellement `Development`).
3. Ajoutez éventuellement `GEMINI_MODEL` avec la valeur `gemini-2.5-flash`.
4. Relancez un déploiement après avoir enregistré les variables.

Vercel détecte automatiquement `api/ask.js` et `api/health.js`. Les pages statiques restent servies directement par Vercel, et le navigateur appelle `/api/ask` sur le même domaine.

## Règle éditoriale de confiance

La documentation doit distinguer clairement ce qui est :

- **Vérifié dans ce dépôt** : visible dans le code local et fonctionnelment présent dans ce workspace.
- **Documenté, mais non vérifiable ici** : décrit dans la référence ou dans les docs, mais absent de l’application réellement livrée dans ce dépôt.
- **À confirmer avant publication** : annoncé ou souhaité, mais sans éléments suffisants pour garantir son comportement dans le produit final.

Le dépôt contient surtout le site documentaire, son moteur de recherche et son assistant Gemini. Il ne contient pas l’application XERA1 complète. Les pages doivent donc être lues comme un guide cible, pas comme une preuve de disponibilité absolue de toutes les fonctionnalités.

## Assistant XERA1 AI

L’assistant documentaire doit :

- répondre en français et de manière concise ;
- s’appuyer sur les sources locales du dépôt ;
- distinguer clairement les affirmations vérifiées, documentées ou simplement projetées ;
- indiquer clairement si une fonctionnalité n’est pas présente dans ce workspace ;
- éviter de promettre des comportements non vérifiés dans l’application déployée.

## Conventions

- Le contenu est écrit en français.
- Le style privilégie la clarté, les étapes, les blocs de code et les callouts.
- La documentation reste alignée sur les fonctionnalités réellement implémentées dans l'application XERA1.
- Les écrans et routes non présents dans ce dossier sont explicitement marqués comme « à confirmer » ou « non vérifiable ici ».
