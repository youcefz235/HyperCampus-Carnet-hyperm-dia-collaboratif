# HyperCampus-Carnet-hyperm-dia-collaboratif

📝 Description courte

HyperCampus centralise les notes d’étude dans une interface claire. Chaque note a un titre, un contenu texte et, au besoin, un fichier joint (image, PDF, audio, etc.). Les tags servent à classer par thèmes. La recherche plein-texte et les filtres par tag permettent de retrouver l’information en quelques secondes. Le projet met l’accent sur la simplicité, l’accessibilité et la qualité du code.

🎯 Objectifs

Centraliser les contenus (titre, texte, pièces jointes).

Organiser avec des tags cohérents et réutilisables.

Retrouver vite via recherche + filtres.

Rester sobre techniquement pour une maintenance facile.

🧰 Technologies principales & utilité
Backend

PHP 8.2+
Langage serveur stable et largement supporté, idéal pour un CRUD propre, des validations robustes et une mise en production simple.

Laravel 11
Cadre applicatif qui structure le projet :

Routing & Controllers : organisent les pages et actions.

Eloquent ORM : mappe les tables en modèles (Note, Tag, Attachment…).

FormRequest : valide les formulaires (taille, formats, champs requis).

Policies (RBAC) : sécurise l’accès (un utilisateur ne gère que ses notes).

Storage : gère les fichiers joints (chemins, visibilité, types).

Resources (facultatif) : formatage propre des réponses JSON si besoin d’API.

Laravel Sanctum (optionnel selon besoin d’auth SPA)
Authentification simple pour session ou SPA, protège les routes privées.

Base de données

PostgreSQL 16
SGBD robuste pour stocker les notes, tags, relations et métadonnées.
Points forts : intégrité référentielle, index, JSON si besoin, performances fiables.

Front (serveur rendu)

Blade (templates)
Génère les pages côté serveur, facilite les formulaires, les listes et les détails de notes sans complexité front-end inutile.

CSS / JavaScript “vanilla”
Styles et interactions légères (affichage, formulaires, filtres) en restant simple.
(Tu peux ajouter TailwindCSS plus tard pour accélérer le design si tu veux.)

Outils de build & versioning

Vite
Gère et optimise les assets (JS/CSS), rafraîchit vite en développement, compile proprement en production.

Git & GitHub
Historique clair des changements (commits), gestion d’issues, pull requests, et documentation (README, discussions).

🧭 Utilisation (parcours simple)

Connexion : l’utilisateur accède à son espace sécurisé.

Créer une note : titre, texte, tags, fichier joint (optionnel).

Organiser : tags cohérents (ex. “Réseaux”, “Examen”, “Projet”).

Retrouver : recherche par mot-clé + filtre par tag.

Gérer : consulter, modifier, supprimer au besoin.

⚙️ Fonctionnalités (MVP)

CRUD Notes (titre, contenu, timestamps)

Tags multiples par note (classification)

Recherche plein-texte simple (titre/texte)

Filtres par tag

Pièce jointe (optionnelle) par note

🧱 Modèle de données (conceptuel, simplifié)

User : compte et authentification.

Note : appartient à un utilisateur, contient titre/texte (+ fichier optionnel).

Tag : mot-clé thématique.

NoteTag (pivot) : relie notes ↔ tags (plusieurs à plusieurs).

Attachment (optionnel) : fichier lié à une note (chemin, type MIME).

♿ Accessibilité & qualité

Navigation clavier, focus visible, labels explicites, contrastes lisibles.

Validation serveur stricte, messages d’erreur clairs.

Structure de code lisible (contrôleurs, requêtes, modèles, policies).

🔭 Roadmap (suggestion)

Itération 1 : Auth, CRUD Notes/Tags, liaisons Note-Tag.

Itération 2 : Recherche + filtres, pièces jointes.

Itération 3 : Dashboard basique, accessibilité renforcée.

Itération 4 : Optimisations (index, pagination), tests et doc utilisateur.

🎤 Prompt / Pitch

HyperCampus est un carnet de notes web minimaliste et robuste (Laravel + PostgreSQL) qui transforme le chaos de tes cours en savoir exploitable : crée des notes claires (texte + pièce jointe), organise-les avec des tags cohérents, puis retrouve l’essentiel en quelques secondes grâce à la recherche et aux filtres. Simple à utiliser, accessible et fiable — pour réviser mieux, produire plus vite et rester concentré sur l’essentiel.

---
```mermaid
erDiagram
  User ||--o{ Note : "écrit"
  Note ||--o{ NoteTag : "est_tagguée"
  Tag  ||--o{ NoteTag : "contient"
  Note ||--o{ Attachment : "a"

  User {
    bigint id PK
    string name
    string email
    string password
  }

  Note {
    bigint id PK
    bigint user_id FK
    string title
    text   content
    datetime created_at
    datetime updated_at
  }

  Tag {
    bigint id PK
    string name
  }

  NoteTag {
    bigint note_id FK
    bigint tag_id  FK
  }

  Attachment {
    bigint id PK
    bigint note_id FK
    string path
    string mime_type
  }
