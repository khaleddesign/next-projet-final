# 🏗️ ChantierPro - Plateforme de Gestion BTP

ChantierPro est une plateforme complète de gestion pour les professionnels du BTP, développée avec Next.js 15 et TypeScript.

## 🎯 Vue d'ensemble

ChantierPro offre une solution tout-en-un pour la gestion des chantiers, la facturation, le CRM client, et la planification des travaux BTP.

### ✨ Fonctionnalités principales

- 🏗️ **Gestion des chantiers** - Suivi complet des projets de construction
- 💰 **Devis et Facturation** - Système de facturation BTP avec TVA multi-taux
- 👥 **CRM Client** - Gestion complète de la relation client
- 📅 **Planning** - Planification des tâches avec diagramme de Gantt
- 💬 **Messagerie** - Communication intégrée par chantier
- 📄 **Documents** - Gestion des documents et photos de chantier
- 📊 **Tableaux de bord** - Analytics et reporting avancés
- 👤 **Gestion des utilisateurs** - Rôles et permissions (Admin, Commercial, Ouvrier, Client)

## 🛠️ Technologies utilisées

### Frontend
- **Next.js 15** - Framework React avec App Router
- **TypeScript** - Typage statique
- **Tailwind CSS** - Framework CSS utilitaire
- **Radix UI** - Composants accessibles
- **Lucide React** - Icônes

### Backend
- **Next.js API Routes** - API REST intégrée
- **Prisma** - ORM pour base de données
- **SQLite** - Base de données (peut être changée facilement)
- **NextAuth.js** - Authentification

### Outils de développement
- **ESLint** - Linting du code
- **Jest** - Tests unitaires
- **TypeScript** - Vérification de types

## 🚀 Installation et démarrage

### Prérequis
- Node.js 18+ 
- npm ou yarn

### Installation

```bash
# Cloner le projet
git clone [url-du-repo]
cd chantierpro

# Installer les dépendances
npm install

# Configurer la base de données
npx prisma db push

# Démarrer en mode développement
npm run dev
```

L'application sera accessible sur `http://localhost:3000`

### Scripts disponibles

```bash
npm run dev          # Démarrage en mode développement
npm run build        # Build de production
npm run start        # Démarrage du serveur de production
npm run lint         # Linting du code
npm run test         # Lancement des tests
npm run db:push      # Synchronisation du schéma Prisma
npm run db:generate  # Génération du client Prisma
```

## 📁 Structure du projet

```
chantierpro/
├── app/                    # Pages Next.js (App Router)
│   ├── api/               # Routes API
│   ├── auth/              # Pages d'authentification
│   ├── dashboard/         # Interface principale
│   └── globals.css        # Styles globaux
├── components/            # Composants React réutilisables
│   ├── ui/               # Composants UI de base
│   ├── layout/           # Composants de mise en page
│   ├── auth/             # Composants d'authentification
│   ├── chantiers/        # Composants spécifiques aux chantiers
│   ├── devis/            # Composants de facturation
│   ├── messages/         # Composants de messagerie
│   └── planning/         # Composants de planification
├── hooks/                 # Hooks React personnalisés
├── lib/                   # Utilitaires et configurations
├── prisma/               # Schema et migrations Prisma
├── types/                # Définitions TypeScript
└── public/               # Assets statiques
```

## 🎭 Rôles utilisateurs

### 👨‍💼 Admin
- Accès complet à toutes les fonctionnalités
- Gestion des utilisateurs et permissions
- Configuration de la bibliothèque prix
- Analytics et rapports avancés

### 💼 Commercial
- Gestion des clients et prospects
- Création et suivi des devis
- CRM et pipeline commercial
- Planning des rendez-vous

### 🔨 Ouvrier
- Vue sur ses chantiers assignés
- Upload de photos et rapports
- Suivi de l'avancement des tâches
- Messagerie chantier

### 👤 Client
- Vue sur ses chantiers
- Validation des devis
- Communication avec l'équipe
- Consultation des documents

## 🏗️ Modules principaux

### 📊 Dashboard
- Vue d'ensemble des KPIs
- Graphiques de performance
- Activité récente
- Actions rapides

### 🏗️ Gestion des chantiers
- Création et suivi des chantiers
- Attribution d'équipes
- Timeline des événements
- Gestion des étapes et jalons
- Upload de photos et documents

### 💰 Devis et Facturation
- Création de devis personnalisés
- Conversion devis → facture
- Gestion TVA multi-taux (5.5%, 10%, 20%)
- Autoliquidation pour sous-traitance
- Situations de travaux
- Retenues de garantie
- Suivi des paiements

### 👥 CRM Client
- Fiche client complète
- Historique des interactions
- Pipeline des opportunités
- Segmentation par type (Particulier, Professionnel, etc.)
- Géolocalisation

### 📅 Planning
- Calendrier des événements
- Diagramme de Gantt
- Gestion des conflits
- Notifications automatiques
- Récurrence des tâches

### 💬 Messagerie
- Chat temps réel
- Messages par chantier
- Partage de fichiers
- Notifications push
- Recherche avancée

### 📄 Gestion documentaire
- Upload et stockage sécurisé
- Aperçu des fichiers
- Organisation par dossiers
- Partage avec liens sécurisés
- Versions et historique

## 🔐 Authentification et sécurité

- **NextAuth.js** pour l'authentification
- Sessions sécurisées
- Hachage des mots de passe avec bcrypt
- Protection CSRF
- Validation des données côté serveur

## 🗄️ Base de données

### Modèle de données principal

```prisma
model User {
  id       String @id @default(cuid())
  email    String @unique
  name     String
  role     Role   @default(CLIENT)
  // ... autres champs
}

model Chantier {
  id          String @id @default(cuid())
  nom         String
  description String
  statut      ChantierStatus
  client      User   @relation(fields: [clientId], references: [id])
  // ... autres champs
}

model Devis {
  id       String @id @default(cuid())
  numero   String @unique
  statut   DevisStatus
  montant  Float
  // ... autres champs
}
```

### Types principaux
- **Statuts chantier** : PLANIFIE, EN_COURS, EN_ATTENTE, TERMINE, ANNULE
- **Statuts devis** : BROUILLON, ENVOYE, ACCEPTE, REFUSE, PAYE, ANNULE
- **Rôles utilisateur** : ADMIN, COMMERCIAL, OUVRIER, CLIENT

## 🎨 Interface utilisateur

### Design System
- **Tailwind CSS** pour le styling
- **Radix UI** pour les composants accessibles
- **Lucide React** pour les icônes
- Design responsive mobile-first
- Thème cohérent avec variables CSS

### Composants principaux
- `Button` - Boutons avec variants
- `Card` - Cartes de contenu
- `Badge` - Labels et statuts
- `Toast` - Notifications
- `Modal` - Fenêtres modales
- `DataTable` - Tableaux de données

## 📡 API Routes

### Endpoints principaux

```typescript
// Chantiers
GET    /api/chantiers              # Liste des chantiers
POST   /api/chantiers              # Créer un chantier
GET    /api/chantiers/[id]         # Détail d'un chantier
PUT    /api/chantiers/[id]         # Modifier un chantier

// Devis
GET    /api/devis                  # Liste des devis
POST   /api/devis                  # Créer un devis
GET    /api/devis/[id]             # Détail d'un devis
PUT    /api/devis/[id]             # Modifier un devis
POST   /api/devis/[id]/convert     # Convertir en facture

// Users
GET    /api/users                  # Liste des utilisateurs
POST   /api/users                  # Créer un utilisateur
GET    /api/users/[id]             # Détail d'un utilisateur

// Documents
GET    /api/documents              # Liste des documents
POST   /api/documents              # Upload de document
GET    /api/documents/[id]         # Télécharger un document
```

## 🧪 Tests

### Configuration des tests
- **Jest** pour les tests unitaires
- **React Testing Library** pour les tests de composants
- **MSW** pour le mocking des API

```bash
# Lancer les tests
npm run test

# Tests en mode watch
npm run test:watch

# Tests avec couverture
npm run test:coverage
```

## 🚀 Déploiement

### Variables d'environnement

```env
# Base de données
DATABASE_URL="file:./prisma/dev.db"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="votre-clé-secrète-très-sécurisée"

# Optionnel : pour PostgreSQL en production
# DATABASE_URL="postgresql://user:password@host:port/database"
```

### Build de production

```bash
# Build
npm run build

# Démarrage production
npm run start
```

### Déploiement recommandé
- **Vercel** (recommandé pour Next.js)
- **Railway** ou **Render** avec PostgreSQL
- **Docker** avec docker-compose

## 🔧 Configuration avancée

### Personnalisation du thème
```css
/* app/globals.css */
:root {
  --primary: 220 90% 50%;
  --primary-foreground: 0 0% 100%;
  /* ... autres variables */
}
```

### Extension de la base de données
Le schéma Prisma peut être facilement étendu pour ajouter de nouveaux modèles ou champs.

### Ajout de nouveaux rôles
Modifier l'enum `Role` dans `prisma/schema.prisma` et adapter les permissions.

## 📚 Documentation complète

La documentation technique complète est disponible dans le dossier [`documentation/`](./documentation/) :

- **[Architecture](./documentation/ARCHITECTURE.md)** - Architecture technique détaillée
- **[API Documentation](./documentation/API_DOCUMENTATION.md)** - Documentation complète de l'API
- **[Guide de déploiement](./documentation/DEPLOYMENT.md)** - Instructions de déploiement
- **[Guide de contribution](./documentation/CONTRIBUTING.md)** - Comment contribuer au projet
- **[Changelog](./documentation/CHANGELOG.md)** - Historique des versions

### Ressources utiles

- [Next.js Documentation](https://nextjs.org/docs)
- [Prisma Documentation](https://www.prisma.io/docs)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Radix UI](https://www.radix-ui.com)

## 🤝 Contribution

Pour contribuer au projet :

1. Fork le repository
2. Créer une branche feature (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Commit les changes (`git commit -am 'Ajout nouvelle fonctionnalité'`)
4. Push la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Créer une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier `LICENSE` pour plus de détails.

## 🆘 Support

Pour toute question ou problème :
- Créer une issue sur GitHub
- Consulter la documentation
- Contacter l'équipe de développement

---

**ChantierPro** - La solution complète pour les professionnels du BTP 🏗️# next-projet-final
