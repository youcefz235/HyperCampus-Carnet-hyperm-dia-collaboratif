HyperCampus — Carnet de notes multimédia

(Laravel + PostgreSQL · Front : HTML + CSS + JavaScript)

📝 Description du projet

HyperCampus centralise les notes d’étude dans une interface simple : chaque note possède un titre, un contenu texte et, au besoin, une pièce jointe (image, PDF, audio…). Les tags servent à organiser par thèmes, et une recherche + des filtres permettent de retrouver l’info en quelques secondes. Le projet met l’accent sur la sobriété, l’accessibilité et la fiabilité.

🎯 Objectifs

Centraliser les contenus d’étude (note + pièces jointes).

Organiser via des tags cohérents et réutilisables.

Retrouver rapidement l’information grâce à la recherche et aux filtres.

Rester simple côté technique pour une maintenance facile.

👥 Public cible

Étudiants (prise de notes, révisions, projets).

Enseignants/tuteurs (consultation) — optionnel.

⚙️ Fonctionnalités (MVP)

Notes : créer, lire, modifier, supprimer.

Tags : plusieurs tags par note (classement thématique).

Recherche : mot-clé sur titre/contenu.

Filtres : par tag (combinable avec recherche).

Pièce jointe : fichier optionnel attaché à une note.

🧭 Utilisation (parcours simple)

Se connecter à son espace.

Créer une note : titre, contenu, tags, fichier joint (optionnel).

Consulter la liste : rechercher par mot-clé et/ou filtrer par tag.

Modifier ou supprimer une note si nécessaire.

🧰 Technologies & utilité
Backend

PHP 8.2+ — Langage serveur stable pour un CRUD propre et des validations fiables.

Laravel 11 — Structure l’app (routes, contrôleurs, modèles) et apporte :

Eloquent ORM (modèles : User, Note, Tag, Attachment + pivot note_tag),

FormRequest (validation serveur),

Policies (RBAC) (droits d’accès aux notes),

Storage (gestion des fichiers),

Resources (facultatif) pour réponses JSON propres si besoin d’API.

Laravel Sanctum (si nécessaire) — Auth simple pour sécuriser les pages privées.

Base de données

PostgreSQL 16 — SGBD robuste (intégrité, index, JSON possible).

Front (sans framework)

HTML — Templates Blade sémantiques, accessibles.

CSS — Styles propres, responsive, focus visible, contrastes.

JavaScript (vanilla) — Interactions légères (recherche, filtres, feedbacks).

Outils

Vite — Build et optimisation des assets (CSS/JS).

Git & GitHub — Versioning, issues, pull requests, documentation.

♿ Accessibilité & qualité

Navigation clavier, focus visible, labels explicites, contrastes lisibles.

Messages d’erreur clairs (validation).

Code organisé (contrôleurs, requêtes, modèles, policies).

🗺️ Roadmap (suggestion)

Itération 1 : Auth, CRUD Notes/Tags, liaison Note-Tag.

Itération 2 : Recherche + filtres, pièce jointe.

Itération 3 : Dashboard simple, A11y renforcée.

Itération 4 : Optimisations (index DB, pagination), tests & doc.

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
