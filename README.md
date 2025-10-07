Notea — Carnet de notes multimédia

📝 Description du projet

Notea centralise les notes d’étude dans une interface simple : chaque note possède un titre, un contenu texte et, au besoin, une pièce jointe (image, PDF, audio…). Les tags permettent d’organiser par thèmes, tandis que la recherche et les filtres aident à retrouver l’information en quelques secondes. Le projet privilégie la sobriété, l’accessibilité et la fiabilité pour un usage étudiant quotidien.

🎯 Objectifs

Centraliser les contenus (notes + pièces jointes).

Organiser via des tags cohérents et réutilisables.

Retrouver rapidement l’information (recherche + filtres).

Rester simple côté technique pour une maintenance facile et un apprentissage clair.

👥 Public cible

Étudiants (prise de notes, révisions, projets).

Enseignants/tuteurs (consultation) — optionnel.

⚙️ Fonctionnalités (MVP)

Notes : créer, lire, modifier, supprimer.

Tags : associer plusieurs tags à une note.

Recherche : mot-clé sur le titre et/ou le contenu.

Filtres : filtrage par tag (combinable avec la recherche).

Pièce jointe : fichier optionnel lié à une note (image, PDF, audio, etc.).

🧭 Utilisation (parcours simple)

Se connecter à son espace privé.

Créer une note : titre, contenu, tags, pièce jointe (optionnel).

Consulter la liste : lancer une recherche par mot-clé et/ou filtrer par tag.

Modifier ou supprimer une note si nécessaire.

🧰 Technologies & utilité
Backend

PHP 8.2+
Langage serveur mature et répandu, idéal pour un CRUD fiable et des validations solides.

Laravel 11
Cadre applicatif qui structure le projet et accélère le développement :

Routing & Controllers : logique claire pour les actions (création, édition, suppression).

Eloquent ORM : mapping propre entre tables PostgreSQL et modèles (User, Note, Tag, Attachment + pivot note_tag).

FormRequest (Validation) : règles serveur (champs requis, formats, tailles fichiers) → données propres.

Policies (RBAC) : sécurité applicative (un utilisateur gère ses propres notes).

Storage : gestion des pièces jointes (chemins, visibilité, types).

Resources (option) : formatage JSON propre si besoin d’API.

Laravel Sanctum (si requis)
Authentification simple pour protéger les pages privées.

Base de données

PostgreSQL 16
SGBD robuste : intégrité référentielle, index pour accélérer recherche/tri, support JSON si on veut des métadonnées flexibles.

Front (sans framework)

HTML
Templates Blade sémantiques et accessibles (titres, listes, formulaires).

CSS
Styles propres, responsive, contrastes lisibles, focus visible pour le clavier.

JavaScript (vanilla)
Interactions légères (recherche instantanée côté UI, filtres, feedbacks) sans complexité de framework.

Outils

Vite — Build et optimisation des assets (CSS/JS) pour un front rapide.

Git & GitHub — Versioning, issues, pull requests, documentation.

📁 Structure du projet (vue d’ensemble)

app/Models : User, Note, Tag, Attachment (+ pivot note_tag).

app/Http/Controllers : logique CRUD (Notes, Tags, Attachments).

app/Http/Requests : validations (FormRequest) pour des données fiables.

database/migrations : tables users, notes, tags, note_tag, attachments.

resources/views : pages Blade (liste, détail, formulaires).

resources/css & resources/js : styles et JS “vanilla”.

routes/web.php : pages et formulaires (accès après login).

routes/api.php : (option) endpoints JSON si nécessaire.

public/storage : lien vers les fichiers uploadés.

♿ Accessibilité & qualité

Navigation au clavier, focus visible, textes et labels explicites.

Contrastes lisibles, tailles de police adaptées.

Messages d’erreur clairs (validation serveur).

Code organisé (contrôleurs, requêtes, modèles, policies) et maintenable.

🗺️ Roadmap (suggestion)

Itération 1 : Auth, CRUD Notes/Tags, pivot Note-Tag.

Itération 2 : Recherche + filtres, pièces jointes.

Itération 3 : Dashboard simple, A11y renforcée, petites améliorations UX.

Itération 4 : Optimisations (index DB, pagination), tests et doc utilisateur.

🎤 Prompt / Pitch

Notea est un carnet de notes web minimaliste et robuste (Laravel + PostgreSQL) qui transforme le chaos de tes cours en savoir exploitable : crée des notes claires (texte + pièce jointe), organise-les avec des tags cohérents, puis retrouve l’essentiel en quelques secondes grâce à la recherche et aux filtres. Simple à utiliser, accessible et fiable — pour réviser mieux, produire plus vite et rester concentré sur l’essentiel.

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
