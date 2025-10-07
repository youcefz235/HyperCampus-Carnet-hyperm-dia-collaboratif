# HyperCampus-Carnet-hyperm-dia-collaboratif

## 📝 Description du projet
HyperCampus est une application web qui aide les étudiants à **centraliser** leurs notes (texte + pièces jointes), à **les organiser** avec des **tags** et à **retrouver** rapidement l’information grâce à une **recherche** et des **filtres** simples.  
Le but est de rester **minimaliste** et **facile à utiliser** : une interface claire pour créer/éditer ses notes, les classer par thèmes et les consulter rapidement.

## 🎯 Objectifs
- **Centraliser** les contenus d’étude (titre, texte, fichiers).
- **Organiser** les notes via des **tags** (plusieurs par note).
- **Retrouver vite** l’information : **recherche** par mot-clé et **filtre par tag**.
- **Rester simple et fiable** : architecture légère, code propre, bonnes pratiques Laravel.

## 🧰 Outils & technologies utilisés
**Backend**
- **PHP 8.2+**
- **Laravel 11** (Routing, Controllers, Eloquent, FormRequest, Policies)
- Authentification **Sanctum** (si nécessaire)
- Gestion des fichiers via **Storage** (uploads)

**Base de données**
- **PostgreSQL 16**
- Migrations Laravel (schéma versionné)

**Front**
- **Blade** (templates serveur)
- **CSS/JS** classiques (possibilité d’ajouter Tailwind plus tard)

**Outils**
- **Git** & **GitHub** (versionning, issues, PR)

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
