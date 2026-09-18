# Cahier des charges éditorial XERA1

## Guide officiel du Proof of Building

## 1. Objet du document

Ce cahier des charges définit le contenu à produire pour transformer la documentation XERA1 en un guide pédagogique, progressif et compréhensible par une personne qui découvre la plateforme.

Le document repose sur une comparaison entre :

- les pages documentaires actuelles ;
- `XERA1_COMPLETE_REFERENCE.md` ;
- les fichiers `.md` et `.mdx` du dépôt ;
- le code réellement présent dans ce workspace.

### Règle éditoriale de confiance

La documentation ne doit jamais présenter une fonctionnalité comme disponible uniquement parce qu’elle est décrite dans un document de conception.

Chaque affirmation doit recevoir l’un des statuts suivants :

- **Vérifié dans ce dépôt** : le comportement est visible dans le code local.
- **Documenté, mais non vérifiable ici** : le comportement est décrit dans la documentation ou la référence, mais le code de l’application n’est pas présent.
- **À confirmer avant publication** : le comportement est annoncé ou demandé, mais aucun élément suffisamment précis ne permet de garantir son fonctionnement.

Le dépôt contient principalement le site documentaire, son moteur de recherche et son assistant Gemini. Il ne contient pas l’application XERA1 complète. Les guides ci-dessous doivent donc être utilisés comme contenu cible et soumis à une validation produit avant d’être publiés comme procédures garanties.

## 2. Résumé exécutif

### Ce qui est réellement vérifiable

- Navigation entre les pages documentaires HTML.
- Menu documentaire responsive.
- Recherche de documentation par bouton et par raccourci `Ctrl+K` ou `Cmd+K`.
- Assistant documentaire appelé via `/api/ask`.
- Lecture des sources Markdown et MDX par l’assistant.
- Lecture des sept pages HTML principales par l’assistant.
- Endpoint local de santé du service.
- Serveur statique local.

### Ce qui est documenté mais non implémenté dans ce workspace

- Création de compte XERA1.
- Authentification par email, magic link ou google OAuth.
- Sessions utilisateur et révocation des jetons.
- Feed de découverte ou d’abonnements.
- Traces, ARCs, jalons et preuves publiées dans l’application.
- Likes, commentaires, suivis et partages produit.
- Recherche produit, catégories, tendances et historique de sept jours.
- Messagerie entre builders, fondateurs et entreprises.
- Pièces jointes et partage de preuves dans un chat.
- Création et gestion de pages PRO.
- CTA, capture de leads, pitch deck et recrutement.
- Badge de vérification XERA1.
- Vérification C2PA et détection de médias générés par IA.
- RLS, contrôle d’accès métier, rate limiting et journal d’audit.

## 3. Comparaison code et documentation

### 3.1 Authentification et onboarding

#### Présent dans la documentation

La page `getting-started.html` décrit la création d’un compte par email, magic link, la confirmation, le profil initial, la création d’un ARC et la première preuve.

`account-setup.mdx` complète ce parcours avec la gestion du profil, des notifications, du mot de passe et de la déconnexion.

`api/authentication.mdx` décrit des jetons Bearer, des scopes, une session active et la révocation.

`XERA1_COMPLETE_REFERENCE.md` ajoute l’email, OAuth et des règles de sécurité autour des sessions.

#### Vérifié dans le code

Aucune route d’inscription, de connexion, d’OAuth, de session ou de révocation n’est présente dans le workspace.

Les seules informations d’authentification exécutées localement concernent la clé serveur `GEMINI_API_KEY` utilisée par l’assistant documentaire. Cette clé ne constitue pas une authentification utilisateur XERA1.

#### Écart à traiter

Le guide doit séparer clairement le parcours prévu de la disponibilité effective. Avant publication, l’équipe doit confirmer :

- les méthodes d’inscription réellement proposées ;
- le nom exact des écrans ;
- la place de l’OAuth ;
- la durée de vie d’une session ;
- la procédure de récupération de compte ;
- les règles de déconnexion globale ;
- les messages d’erreur réellement affichés.

### 3.2 Feed et interactions

#### Présent dans la documentation

`features/feed.mdx` décrit un feed Abonnements et un feed Découverte, des filtres par domaine et par étape d’ARC, ainsi que les likes, commentaires, partages et suivis.

`search-and-discovery.html` décrit la navigation verticale, le mode immersif et les gestes.

La référence décrit également les vues, les interactions et les signaux de progression.

#### Vérifié dans le code

Aucun composant de feed, endpoint de feed, pagination, classement, interaction ou suivi n’est présent.

La recherche actuellement visible concerne uniquement la documentation. Elle filtre une liste locale de pages et ne recherche pas les utilisateurs, les ARCs ou les Traces de l’application.

#### Écart à traiter

Le guide doit être conservé comme procédure cible, mais chaque bouton et chaque geste doit être vérifié dans l’application réelle avant publication. Il faut notamment confirmer le nom du bouton de lecture immersive, la zone de glissement, les états de chargement et le comportement après un signalement.

### 3.3 Command palette et recherche

#### Présent dans la documentation

La documentation mentionne `/search`, `Cmd/Ctrl+K`, les catégories Builds, Founders, VCs, Tech, Milestones et Open Source, les tendances et l’historique de sept jours.

#### Vérifié dans le code

Le site documentaire ouvre un overlay de recherche avec le bouton **Search docs** ou `Cmd/Ctrl+K`.

La recherche locale porte sur les pages documentaires connues. Elle ne traite pas la commande `/search`, ne conserve pas un historique utilisateur et ne calcule pas de tendances produit.

#### Écart à traiter

La documentation doit distinguer **Recherche dans la documentation** et **Recherche dans l’application**. Il faut confirmer avant publication :

- si `/search` est une commande textuelle ou une URL ;
- si les catégories sont cliquables ;
- si l’historique est lié au compte ou au navigateur ;
- si la durée de sept jours est exacte ;
- comment supprimer un terme ;
- comment les tendances sont calculées ;
- quelles données sont exclues de la recherche.

### 3.4 Messagerie

#### Présent dans la documentation

`messaging-and-network.html` et `features/messaging.mdx` décrivent les conversations directes, les demandes de messages, les entreprises, les pièces jointes, les images, les liens et le signalement.

#### Vérifié dans le code

Aucun écran, endpoint, stockage, système de notification ou contrôle d’accès de messagerie n’est présent.

#### Écart à traiter

Il faut valider le parcours exact d’ouverture d’une conversation, les conditions pour contacter un membre, la taille et les formats des fichiers, la modération, le blocage, le signalement et les notifications.

### 3.5 Pages PRO

#### Présent dans la documentation

`pro-pages.html` explique la différence entre profil et page PRO, les types de présence, le contenu de marque, les CTA, la capture de leads, le pitch deck, GitHub et le recrutement.

#### Vérifié dans le code

Aucun éditeur de page PRO, modèle de données, route de leads, système de permission d’équipe ou suivi de CTA n’est présent.

#### Écart à traiter

Le guide doit être validé par un propriétaire produit. Il faut confirmer les champs obligatoires, les rôles administrateurs, les changements de visibilité, la destination des contacts, la confidentialité du pitch deck et les règles de suppression.

### 3.6 Trust, certification et C2PA

#### Présent dans la documentation

`trust-and-verification.html` décrit le badge, la provenance des médias et les principes d’authenticité.

La référence mentionne C2PA, `isAI`, l’émetteur, l’outil, l’historique d’action, la sécurité, les règles d’accès et la validation serveur.

#### Vérifié dans le code

Aucun utilitaire C2PA, import de bibliothèque C2PA, signature vérifiée, détection `isAI`, calcul de badge, RLS ou journal d’audit n’est présent.

Le code local démontre seulement quelques protections du site documentaire, notamment l’échappement des réponses de l’assistant et la conservation de la clé Gemini côté serveur.

#### Écart à traiter

Aucune phrase ne doit garantir qu’un média est authentifié ou qu’un badge prouve à lui seul la réalité d’un travail. Le guide doit expliquer la différence entre provenance technique, déclaration de l’auteur et validation éditoriale.

## 4. Architecture éditoriale cible

La navigation finale doit suivre l’ordre naturel d’un nouvel utilisateur :

1. Comprendre XERA1.
2. Créer son compte.
3. Préparer son profil.
4. Créer un ARC.
5. Publier une première preuve.
6. Explorer le feed.
7. Rechercher une personne ou un projet.
8. Échanger avec quelqu’un.
9. Créer une présence PRO.
10. Renforcer la confiance et la sécurité.

Chaque page doit commencer par :

- une phrase qui explique à quoi sert la page ;
- le résultat attendu ;
- les conditions nécessaires ;
- le temps approximatif ;
- une procédure numérotée ;
- les erreurs fréquentes ;
- une vérification finale ;
- un lien vers l’étape suivante.

Le ton doit être direct, calme et concret. Une étape doit contenir une seule action principale. Les mots d’interface doivent être écrits exactement comme ils apparaissent dans le produit et en gras.

## 5. Texte rédigé pour les guides utilisateurs

## Section 1 — Prise en main et inscription

### Ce que vous allez faire

Vous allez créer votre compte, confirmer votre adresse, préparer votre profil et publier votre première preuve de travail.

Une preuve de travail montre une action réelle : une étape terminée, une décision prise, une version livrée, un test réalisé ou un résultat observable.

### Avant de commencer

Préparez une adresse email que vous pouvez consulter immédiatement.

Préparez aussi :

- un nom ou un nom de marque ;
- une courte présentation ;
- une image d’avatar ;
- votre rôle ou domaine d’activité ;
- les liens sociaux ou professionnels que vous souhaitez rendre publics ;
- un premier résultat à montrer.

### Étape 1 — Ouvrir l’inscription

1. Ouvrez la page d’inscription XERA1.
2. Saisissez votre adresse email.
3. Relisez l’adresse avant de continuer.
4. Validez l’inscription.
5. Gardez l’onglet ouvert pendant la confirmation.

Si XERA1 propose plusieurs méthodes, choisissez la méthode affichée sur l’écran : email, magic link ou fournisseur OAuth. Ne choisissez pas une méthode décrite dans un ancien document si elle n’est pas visible dans l’interface.

### Étape 2 — Confirmer votre accès

1. Ouvrez votre boîte email.
2. Cherchez le message envoyé par XERA1.
3. Si un lien magique est proposé, cliquez une seule fois dessus.
4. Si un code OTP est demandé, recopiez le code sans ajouter d’espace.
5. Revenez à XERA1 et attendez la confirmation de la session.
6. Vérifiez que votre nom ou votre avatar apparaît dans l’interface.

Ne transmettez jamais votre code OTP ou votre lien magique à une autre personne. Un code de connexion est personnel et temporaire.

Si le message n’arrive pas :

- vérifiez les courriers indésirables ;
- confirmez que l’adresse saisie est correcte ;
- attendez quelques instants avant de demander un nouvel envoi ;
- utilisez uniquement le dernier code reçu.

### Étape 3 — Préparer le profil initial

1. Ouvrez les paramètres du profil.
2. Ajoutez votre nom affiché.
3. Choisissez un avatar reconnaissable.
4. Écrivez une bio en une ou deux phrases.
5. Indiquez votre rôle ou votre domaine.
6. Ajoutez uniquement les liens sociaux que vous acceptez de rendre publics.
7. Enregistrez les changements.
8. Ouvrez votre profil public pour vérifier le résultat.

Votre bio doit répondre à trois petites questions : qui êtes-vous, que construisez-vous, et quel type de progrès voulez-vous montrer ?

### Étape 4 — Créer votre premier ARC

Un ARC est le conteneur d’un projet ou d’une ambition. Il permet de relier plusieurs preuves à une même trajectoire.

1. Ouvrez la création d’un ARC.
2. Donnez-lui un nom précis.
3. Expliquez en quelques mots le résultat recherché.
4. Ajoutez trois à cinq jalons observables.
5. Classez les jalons dans l’ordre.
6. Enregistrez l’ARC.
7. Vérifiez que le premier jalon est compréhensible sans explication orale.

Évitez les objectifs vagues comme « réussir ». Préférez « publier la première version », « obtenir dix retours » ou « ouvrir la bêta ».

### Étape 5 — Publier la première preuve

1. Ouvrez la création d’une publication ou d’une Trace.
2. Choisissez un média utile : image, vidéo, démonstration ou capture d’écran.
3. Vérifiez que le média montre réellement l’étape décrite.
4. Écrivez un titre court.
5. Décrivez ce qui a été fait.
6. Expliquez le résultat obtenu.
7. Mentionnez le blocage rencontré, s’il y en a un.
8. Indiquez la prochaine étape.
9. Reliez la preuve à l’ARC et au jalon concernés.
10. Vérifiez la visibilité de la publication.
11. Publiez.

Une bonne description répond à cette question : « Qu’est-ce qui a changé grâce à ce travail ? »

Exemple de structure éditoriale :

- Situation de départ : ce qui devait être résolu.
- Action : ce que vous avez réellement fait.
- Résultat : ce qui fonctionne maintenant.
- Suite : ce que vous allez tester ensuite.

### Vérification finale

Votre profil est prêt si :

- votre identité est compréhensible ;
- votre domaine est indiqué ;
- votre premier ARC possède des jalons ;
- votre preuve contient un média ou une explication vérifiable ;
- la preuve est reliée au bon jalon ;
- vous savez qui peut voir la publication.

## Section 2 — Feed immersif et interactions

### Ce que vous allez faire

Vous allez parcourir les preuves, ouvrir leurs détails, comprendre leur contexte et interagir avec celles qui vous sont utiles.

### Étape 1 — Choisir un feed

1. Ouvrez le feed XERA1.
2. Choisissez le feed des comptes suivis si vous voulez voir les personnes que vous connaissez.
3. Choisissez le feed Découverte si vous voulez trouver de nouveaux builders et projets.
4. Utilisez les filtres disponibles lorsque vous cherchez un domaine ou une étape d’ARC précise.

Le feed doit vous aider à comprendre une progression. Ne vous contentez pas de regarder l’image : cherchez l’action, le résultat et l’étape du projet.

### Étape 2 — Lire une preuve

1. Faites défiler le feed verticalement.
2. Arrêtez-vous lorsqu’une preuve vous intéresse.
3. Ouvrez la description avec **Lire la suite**, si ce bouton existe dans l’interface.
4. Lisez le contexte complet.
5. Vérifiez l’auteur, l’ARC, le jalon et la date affichée.
6. Revenez au feed lorsque vous avez terminé.

Le mode immersif doit mettre la preuve au premier plan, avec un fond sombre et les informations associées visibles sans ambiguïté. Les noms exacts des boutons et métadonnées doivent être confirmés dans l’application réelle.

### Étape 3 — Fermer le mode immersif

Sur téléphone ou tablette :

1. Posez le doigt dans la zone centrale de la vue immersive.
2. Faites glisser l’écran vers le bas.
3. Continuez jusqu’à voir la vue se réduire ou le feed réapparaître.
4. Relâchez le doigt.

Ce geste est appelé **glissement vers le bas** ou **Swipe-to-close**. Si le geste ne fonctionne pas, utilisez le bouton de fermeture visible à l’écran. Ne faites pas glisser depuis une zone qui contient un bouton ou un lien.

### Étape 4 — Aimer et commenter

1. Ouvrez la preuve.
2. Appuyez sur le bouton **J’aime** pour enregistrer votre réaction.
3. Appuyez à nouveau si vous voulez retirer votre réaction.
4. Ouvrez les commentaires.
5. Écrivez un commentaire lié au travail présenté.
6. Relisez votre message.
7. Publiez-le.

Un commentaire utile pose une question précise, partage un retour d’expérience ou reconnaît une étape concrète. Évitez de publier des informations privées.

### Étape 5 — Partager et suivre

1. Ouvrez les actions de la preuve.
2. Choisissez **Partager** si cette action est disponible.
3. Sélectionnez le canal proposé par votre appareil.
4. Pour suivre l’auteur, ouvrez son profil.
5. Appuyez sur **Suivre**.
6. Vérifiez que l’état du bouton a changé.

### Étape 6 — Signaler une preuve

1. Ouvrez le menu d’actions de la preuve.
2. Choisissez **Signaler**.
3. Sélectionnez la raison la plus proche du problème.
4. Ajoutez un contexte factuel si un champ est proposé.
5. Envoyez le signalement.
6. Ne republiez pas le contenu signalé pour attirer l’attention dessus.

Les noms des motifs, le traitement du signalement et la possibilité de suivre son état doivent être confirmés par l’équipe produit.

### Vérification finale

Vous savez utiliser le feed si vous pouvez :

- passer du feed suivi au feed Découverte ;
- filtrer un sujet ou une étape ;
- ouvrir et fermer une description immersive ;
- identifier l’auteur et le jalon ;
- aimer, commenter, partager ou signaler une preuve.

## Section 3 — Command palette et recherche éphémère

### Ce que vous allez faire

Vous allez trouver rapidement un contenu ou une personne, utiliser une catégorie et gérer votre historique de recherche.

### Étape 1 — Ouvrir la recherche

Vous pouvez ouvrir la recherche de deux manières :

1. Appuyez sur `Cmd+K` sur macOS.
2. Appuyez sur `Ctrl+K` sur Windows ou Linux.
3. Vous pouvez aussi cliquer sur la barre ou le bouton de recherche.

Dans la documentation actuelle, ce raccourci ouvre la recherche documentaire. Dans l’application XERA1, le comportement de `/search` doit être confirmé séparément.

### Étape 2 — Écrire une recherche utile

1. Commencez par un mot simple.
2. Utilisez le nom d’un builder, d’un projet ou d’un sujet.
3. Ajoutez un second mot si les résultats sont trop nombreux.
4. Ouvrez le résultat qui correspond à votre besoin.
5. Revenez à la recherche pour essayer une autre formulation.

Cherchez « milestone » ou « jalon » si vous voulez trouver une étape de projet. Cherchez « open source » si vous voulez explorer des projets publiés avec cette orientation.

### Étape 3 — Utiliser les catégories

Lorsque les catégories sont visibles, choisissez celle qui correspond à votre intention :

- **Builds** pour les projets et réalisations ;
- **Founders** pour les fondateurs et porteurs de projet ;
- **VCs** pour les investisseurs ou contenus liés au financement ;
- **Tech** pour les sujets techniques ;
- **Milestones** pour les jalons ;
- **Open Source** pour les projets ouverts et contributions publiques.

Une catégorie réduit le bruit. Commencez par une catégorie, puis ajoutez un mot-clé si nécessaire.

### Étape 4 — Comprendre l’historique de sept jours

La règle documentaire annoncée est une conservation éphémère de sept jours. Cela signifie qu’un terme récent peut réapparaître pendant cette durée, puis disparaître automatiquement.

Cette durée doit être confirmée dans le produit réel avant publication, notamment pour savoir :

- si elle s’applique à tous les comptes ;
- si elle s’applique au navigateur ou au compte ;
- si une recherche vide est conservée ;
- si la suppression manuelle est immédiate partout.

### Étape 5 — Supprimer un terme manuellement

1. Ouvrez l’historique de recherche.
2. Repérez le terme à supprimer.
3. Appuyez sur la croix **×** placée à côté du terme.
4. Vérifiez que le terme disparaît de la liste.
5. Recommencez pour chaque terme que vous voulez retirer.

Ne confondez pas la suppression d’un terme de l’historique avec la suppression d’une publication ou d’un compte.

### Étape 6 — Utiliser les tendances

1. Ouvrez la zone des tendances.
2. Lisez le mot-clé et son contexte.
3. Ouvrez la tendance qui correspond à votre sujet.
4. Vérifiez la date ou la période affichée.
5. Comparez plusieurs preuves au lieu de vous fier à un seul résultat.

La popularité d’un mot-clé ne prouve pas la qualité d’un projet. Utilisez les tendances pour explorer, puis vérifiez les preuves et les jalons.

### Vérification finale

Vous savez utiliser la recherche si vous pouvez :

- ouvrir la palette au clavier ;
- choisir une catégorie ;
- lancer une recherche par mot-clé ;
- supprimer un terme avec **×** ;
- expliquer la conservation annoncée de sept jours ;
- distinguer une tendance d’une preuve de qualité.

## Section 4 — Messagerie dédiée et réseau d’échange

### Ce que vous allez faire

Vous allez ouvrir une conversation, contacter un builder ou une entreprise et partager des informations utiles sans exposer de données sensibles.

### Étape 1 — Ouvrir la messagerie

1. Ouvrez la messagerie depuis la navigation principale.
2. Repérez la liste des conversations.
3. Ouvrez une conversation existante pour lire les derniers messages.
4. Vérifiez le nom et le profil de votre interlocuteur.
5. Ne répondez pas avant d’avoir vérifié que vous êtes dans la bonne conversation.

Le nom exact de l’écran, son affichage plein écran et les états de lecture doivent être confirmés dans l’application réelle.

### Étape 2 — Démarrer une discussion

1. Ouvrez le profil du builder ou du fondateur.
2. Choisissez **Message** si l’action est proposée.
3. Lisez les éventuelles règles de demande de message.
4. Écrivez pourquoi vous contactez cette personne.
5. Faites référence à une preuve, un ARC ou un sujet précis.
6. Relisez votre message.
7. Envoyez-le.

Un bon premier message est court et contextualisé. Il indique ce que vous avez regardé et ce que vous voulez comprendre ou proposer.

### Étape 3 — Contacter une Page PRO

1. Ouvrez la Page PRO de l’entreprise.
2. Vérifiez le nom de la marque et les informations visibles.
3. Choisissez **Message** ou l’action de contact proposée.
4. Expliquez votre demande en une phrase.
5. Ajoutez le lien vers votre profil ou votre preuve si cela est pertinent.
6. Envoyez la demande.

Lorsque la messagerie au nom d’une marque est disponible, un administrateur autorisé peut répondre depuis la Page PRO. L’interface doit clairement indiquer que la réponse est envoyée au nom de la marque et non depuis un profil personnel.

### Étape 4 — Répondre au nom d’une marque

Pour un administrateur de Page PRO :

1. Ouvrez la boîte de réception de la Page PRO.
2. Vérifiez que vous disposez de la permission de répondre.
3. Ouvrez la demande concernée.
4. Sélectionnez l’identité de réponse de la marque si plusieurs identités sont proposées.
5. Rédigez une réponse professionnelle.
6. Vérifiez le nom affiché avant l’envoi.
7. Envoyez la réponse.

Les rôles autorisés et l’historique des actions doivent être confirmés avant d’être documentés comme une règle définitive.

### Étape 5 — Partager un fichier ou une preuve

1. Ouvrez la conversation.
2. Utilisez le bouton de pièce jointe si l’action est disponible.
3. Choisissez un fichier non sensible.
4. Vérifiez le format et la taille autorisés.
5. Ajoutez une phrase expliquant ce que contient le fichier.
6. Ajoutez une preuve visuelle ou un lien si cela aide la conversation.
7. Vérifiez le destinataire.
8. Envoyez.

Ne partagez jamais un mot de passe, une clé secrète, un document d’identité ou un fichier contenant des informations privées sans procédure sécurisée explicite.

### Étape 6 — Signaler ou bloquer

1. Ouvrez le menu de la conversation.
2. Choisissez **Signaler** ou **Bloquer** si l’action est disponible.
3. Sélectionnez le motif approprié.
4. Conservez les informations utiles au signalement sans poursuivre l’échange.
5. Envoyez le signalement.

Les routes, règles d’accès mutuel, notifications et pièces jointes ne sont pas vérifiables dans le code local. Elles doivent faire l’objet d’un test produit avant publication.

### Vérification finale

Vous savez utiliser la messagerie si vous pouvez :

- retrouver une conversation ;
- envoyer un premier message contextualisé ;
- contacter une Page PRO ;
- identifier l’identité utilisée pour répondre ;
- partager un fichier autorisé ;
- signaler un échange problématique.

## Section 5 — Pages professionnelles et entreprises

### Ce que vous allez faire

Vous allez comprendre la différence entre un profil personnel et une Page PRO, créer une présence pour une startup, choisir une action principale et organiser les membres de l’équipe.

### Étape 1 — Choisir entre profil et Page PRO

Le profil personnel raconte votre progression individuelle, vos projets et votre travail.

La Page PRO présente une entreprise, une équipe, un studio, une communauté ou une marque. Elle sert à expliquer une offre, afficher des preuves, orienter une demande et organiser une relation professionnelle.

Choisissez un profil si vous construisez principalement votre réputation personnelle. Choisissez une Page PRO si plusieurs personnes doivent représenter une même activité ou si vous avez besoin d’un espace de conversion.

### Étape 2 — Préparer les informations

Avant de créer la page, préparez :

- le nom officiel ;
- le logo ;
- une bannière si elle est proposée ;
- une description claire ;
- le site web ;
- les liens GitHub, Discord ou autres ;
- les preuves de travail à mettre en avant ;
- les membres autorisés à administrer la page.

### Étape 3 — Créer la Page PRO

1. Ouvrez la création d’une Page PRO.
2. Choisissez le type de présence : entreprise, équipe, studio, communauté ou marque.
3. Saisissez le nom.
4. Ajoutez le logo et la description.
5. Ajoutez le site web et les liens utiles.
6. Sélectionnez les preuves et jalons à mettre en avant.
7. Vérifiez l’aperçu public.
8. Enregistrez ou publiez la page.

Les écrans de création et les champs obligatoires doivent être vérifiés dans l’application réelle.

### Étape 4 — Choisir le CTA

Un CTA est l’action principale proposée à la personne qui consulte la page. Il ne doit pas demander plusieurs choses à la fois.

#### Option A — Réserver une démonstration

1. Choisissez l’objectif de démonstration.
2. Sélectionnez Calendly, Cal.com ou le service effectivement proposé.
3. Collez le lien de réservation.
4. Testez le lien dans une fenêtre privée.
5. Vérifiez que la page de réservation correspond à la marque.
6. Publiez le CTA.

#### Option B — Fundraising ou pitch deck

1. Choisissez l’objectif de financement.
2. Préparez une version autorisée du pitch deck.
3. Choisissez si le deck est public ou accessible après demande.
4. Configurez les informations demandées aux contacts.
5. Testez la réception d’une demande.
6. Vérifiez où les contacts sont stockés et qui peut les consulter.
7. Publiez le CTA.

Ne rendez pas public un document confidentiel par erreur.

#### Option C — Recrutement

1. Choisissez l’objectif de recrutement.
2. Ajoutez les postes ouverts.
3. Écrivez les compétences et le niveau attendu.
4. Indiquez le canal de candidature.
5. Testez le parcours candidat.
6. Vérifiez que chaque poste obsolète peut être désactivé.
7. Publiez le CTA.

#### Option D — Lien externe

1. Choisissez la redirection externe.
2. Saisissez l’URL GitHub, Discord ou autre.
3. Vérifiez le domaine et l’orthographe.
4. Ouvrez le lien dans une nouvelle fenêtre.
5. Vérifiez qu’il mène au bon espace.
6. Publiez le CTA.

### Étape 5 — Ajouter les membres

1. Ouvrez la gestion de l’équipe.
2. Invitez chaque membre avec l’adresse appropriée.
3. Attribuez uniquement la permission nécessaire.
4. Vérifiez l’identité affichée de chaque membre.
5. Retirez les accès qui ne sont plus nécessaires.
6. Consultez l’aperçu public de l’équipe.

Les rôles d’administration, les invitations et la révocation doivent être confirmés avec l’équipe produit.

### Étape 6 — Afficher les jalons

1. Ouvrez les jalons de la Page PRO.
2. Sélectionnez les étapes qui représentent réellement l’entreprise.
3. Associez chaque jalon à une preuve.
4. Ajoutez une date ou une période lorsque cela est disponible.
5. Vérifiez que le statut est exact.
6. Publiez l’affichage.

Un jalon certifié doit être présenté comme un signal de confiance encadré par les règles XERA1. Il ne doit pas être décrit comme une garantie financière, juridique ou commerciale.

### Vérification finale

La Page PRO est prête si :

- la différence avec le profil personnel est claire ;
- la description correspond à l’activité réelle ;
- un seul CTA principal est mis en avant ;
- le lien du CTA fonctionne ;
- les membres affichés sont autorisés ;
- les preuves et jalons sont correctement associés ;
- les informations confidentielles ne sont pas publiques.

## Section 6 — Sécurité, confiance et certification

### Ce que vous allez faire

Vous allez comprendre les signaux de confiance, préparer un profil cohérent et interpréter correctement la provenance des médias.

### Étape 1 — Construire un profil crédible

1. Utilisez une identité cohérente.
2. Décrivez clairement ce que vous construisez.
3. Publiez des preuves liées à des étapes concrètes.
4. Ajoutez le contexte de chaque média.
5. Corrigez les informations qui ne sont plus exactes.
6. Respectez les règles de la communauté.

La confiance se construit par l’ensemble du parcours. Une seule image, un grand nombre d’abonnés ou un badge ne suffit pas à prouver la qualité d’un travail.

### Étape 2 — Comprendre le badge XERA1

Le badge de certification est décrit comme un signal lié à la cohérence d’une présence, à la visibilité des preuves, à l’activité et aux standards d’authenticité.

Avant d’expliquer comment l’obtenir, l’équipe doit publier les critères exacts :

- conditions d’éligibilité ;
- éléments examinés ;
- délai de décision ;
- durée de validité ;
- motif de retrait ;
- procédure de contestation ;
- personne ou système responsable de la décision.

Tant que ces critères ne sont pas vérifiés dans le produit, utilisez la formulation « critères de certification à confirmer ».

### Étape 3 — Préparer une preuve transparente

1. Conservez le média original.
2. Décrivez ce qu’il montre.
3. Indiquez le contexte de création.
4. Reliez-le à un ARC ou à un jalon.
5. Mentionnez les outils utilisés lorsque cela est demandé.
6. Signalez toute retouche importante.
7. Indiquez clairement lorsqu’un média est généré ou modifié par IA.
8. Vérifiez que vous avez le droit de publier le média.

### Étape 4 — Comprendre C2PA

C2PA est un mécanisme de provenance qui peut associer à un média des informations sur son origine, ses modifications et certains outils utilisés.

Dans la documentation cible, il faut expliquer que la provenance peut aider à comprendre l’histoire technique d’un fichier, mais qu’elle ne remplace pas une vérification humaine du résultat ou du contexte.

Ne promettez pas qu’un fichier sans métadonnées est faux. Ne promettez pas non plus qu’un fichier portant une provenance est automatiquement authentique dans tous les sens du terme.

### Étape 5 — Comprendre le statut IA

Si un champ comme `isAI` est affiché dans le produit, expliquez précisément :

- qui le renseigne ;
- s’il est déclaré par l’auteur ou détecté automatiquement ;
- s’il peut être corrigé ;
- ce que signifie une valeur inconnue ;
- quelles conséquences il entraîne.

Aucune détection automatique ne doit être présentée comme parfaite sans mesure publique de ses limites.

### Étape 6 — Protéger son compte et ses données

1. Utilisez un mot de passe unique lorsqu’un mot de passe est demandé.
2. Ne partagez jamais un code de connexion.
3. Vérifiez les liens avant de les ouvrir.
4. Limitez les informations personnelles publiées.
5. Retirez les accès d’anciens membres d’équipe.
6. Signalez les contenus suspects.
7. Conservez une copie des contenus importants.
8. Contactez le support par le canal officiel.

Les règles de RLS, de validation serveur, de limitation de débit, de CSP et d’audit doivent être documentées uniquement après vérification dans l’application déployée.

### Vérification finale

Vous comprenez la confiance XERA1 si vous pouvez :

- expliquer ce qu’une preuve montre ;
- distinguer une déclaration d’auteur d’une provenance technique ;
- expliquer les limites de C2PA ;
- décrire le badge sans le présenter comme une garantie absolue ;
- protéger vos codes et informations privées ;
- signaler un contenu problématique.

## 6. Matrice des pages à produire ou à mettre à jour

### Page d’accueil

Mettre en avant le parcours complet : compte, preuve, feed, recherche, réseau et Page PRO. Ajouter un encadré indiquant que la documentation décrit les fonctionnalités prévues et que certains écrans doivent être confirmés selon la version déployée.

### Getting started

Conserver le parcours existant, puis ajouter la confirmation OTP ou magic link, les liens sociaux, le rôle, l’ARC, les jalons et la structure d’une bonne preuve.

### Feed

Créer une page dédiée aux deux feeds, aux filtres, à la lecture immersive, au geste de fermeture, aux interactions et au signalement.

### Recherche

Séparer la recherche documentaire actuelle de la recherche produit annoncée. Ajouter les catégories, les tendances, la règle de sept jours et la suppression par **×**, avec un statut « à confirmer » tant que le produit réel n’a pas été testé.

### Messagerie

Détailler les conversations, les demandes, les Pages PRO, les identités de réponse, les pièces jointes, le signalement et le blocage.

### Pages PRO

Ajouter un tableau des quatre CTA, un parcours de création, un parcours d’administration, la gestion d’équipe, les leads et les jalons.

### Trust et vérification

Séparer badge, provenance, C2PA, statut IA, droits médias, signalement et sécurité du compte. Ajouter les limites et les critères de certification.

### API

Aligner les pages API sur les routes réellement déployées. Toute route non présente dans le code ou dans l’environnement de production doit être marquée comme exemple, projetée ou non disponible.

## 7. Checklist de validation avant publication

### Validation produit

- Chaque bouton cité existe avec le même libellé.
- Chaque route citée répond dans l’environnement cible.
- Chaque parcours a été testé sur téléphone, tablette et ordinateur.
- Les états vide, chargement, erreur et succès sont documentés.
- Les permissions sont testées avec un compte normal et un compte administrateur.
- Les fichiers et pièces jointes sont testés avec les limites réelles.
- Les règles de confidentialité sont confirmées.

### Validation éditoriale

- Chaque page commence par son objectif.
- Les étapes sont numérotées.
- Une étape ne contient qu’une action principale.
- Les termes d’interface sont en gras.
- Les limites sont visibles avant l’action sensible.
- Les affirmations non vérifiées sont marquées.
- Les exemples n’exposent aucune donnée réelle.
- Les liens entre les pages suivent le parcours de l’utilisateur.

### Validation technique

- Les routes documentées correspondent aux routes déployées.
- Les noms de champs correspondent au produit.
- Les sources de l’assistant sont complètes et actualisées.
- Les métadonnées de provenance sont décrites sans promesse excessive.
- Les tests de sécurité et de permission sont disponibles avant toute garantie écrite.

## 8. Priorités de mise en œuvre éditoriale

### Priorité 1 — Fiabiliser le parcours débutant

Mettre à jour l’inscription, le profil, l’ARC et la première preuve. Ajouter les avertissements de vérifiabilité lorsque les écrans réels ne sont pas disponibles.

### Priorité 2 — Documenter la valeur centrale

Créer le guide du feed, de la preuve, de la lecture immersive et des interactions.

### Priorité 3 — Clarifier recherche et réseau

Séparer recherche documentaire et recherche produit. Puis documenter la messagerie avec ses règles d’accès et de confidentialité.

### Priorité 4 — Documenter la conversion professionnelle

Finaliser les Pages PRO, les CTA, les leads, l’équipe et les jalons après validation des permissions.

### Priorité 5 — Publier la confiance avec prudence

Finaliser le badge, C2PA, le statut IA, la provenance et les règles de sécurité uniquement après preuve d’implémentation et tests.

## 9. Décision recommandée

La documentation actuelle peut devenir un excellent guide pédagogique, mais elle ne doit pas être présentée comme la preuve que toutes les fonctionnalités sont déjà disponibles dans le code de ce dépôt.

La prochaine étape recommandée est une session de validation avec l’application XERA1 déployée. Pour chaque section, un rédacteur doit effectuer le parcours avec un compte de test, relever les libellés exacts, capturer les états importants et remplacer les mentions « à confirmer » par des procédures vérifiées.
