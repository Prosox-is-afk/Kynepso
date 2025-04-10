# Kinepso – Projet vitrine avec base de données

Ce projet est une application web construite avec **Next.js 15**, **TypeScript**, **Tailwind CSS** et **Prisma**. Il s'agit d'un site vitrine dynamique permettant de présenter des projets, avec filtrage par catégorie, pages dédiées, formulaire de contact, et plus encore.

## Fonctionnalités

-   Filtrage des projets par catégorie (Sites, Apps, Logiciels)
-   Pages dynamiques pour chaque projet via `slug`
-   SEO dynamique (title + description)
-   Design responsive moderne
-   API interne pour récupérer les projets
-   Formulaire de contact (structure prête, envoi d'email non configuré))

## Technologies utilisées

-   [Next.js 15](https://nextjs.org/) (App Router, Server Components)
-   [TypeScript](https://www.typescriptlang.org/)
-   [Tailwind CSS](https://tailwindcss.com/)
-   [Prisma ORM](https://www.prisma.io/)
-   [Lucide React](https://lucide.dev/)

## Structure du projet

```
├── app/
│   ├── api/               # Routes API (ex: /api/projects)
│   ├── components/        # Composants React (client et server)
│   ├── contact/           # Page de contact
│   ├── projets/           # Page projets + slug dynamique
│   ├── layout.tsx         # Layout principal
│   └── page.tsx           # Page d'accueil
├── prisma/                # Fichier schema.prisma et client
├── public/                # Fichiers statiques (images, svg...)
├── styles/ (fusionné dans app/globals.css)
├── .env                   # Variables d'environnement (Prisma + config mail)
├── tsconfig.json
├── tailwind.config.ts
├── next.config.ts
├── postcss.config.mjs
├── package.json
└── README.md
```

## Modèle de données (Prisma)

Voici le modèle utilisé dans `prisma/schema.prisma` :

```
model Projet {
  id          Int      @id @default(autoincrement())
  title       String
  description String
  category    String
  slug        String   @unique
  image       String
  createdAt   DateTime @default(now())
}
```

Pour initialiser la base :

`npx prisma migrate dev --name init`

> Note : la catégorie attendue est une chaîne parmi "Sites internet", "Applications mobiles", "Logiciels sur mesure". Le champ slug sert de clé pour générer les routes dynamiques /projets/[slug].

## Installation

1. Clonez le repo :

```bash
git clone https://github.com/Prosox-is-afk/Kinepso.git

cd Kinepso
```

2. Installez les dépendances :

```bash
npm install
```

3. Configurez l'environnement :

Créez un fichier `.env` à la racine du projet :

```env
DATABASE_URL="mysql://utilisateur:motdepasse@localhost:3306/nom_de_la_base"
```

4. Mettez en place la base de données :

```bash
npx prisma generate
npx prisma migrate dev --name init
```

5. Lancez le projet en développement :

```bash
npm run dev
```

6. (Facultatif) Construisez le projet pour la production :

```bash
npm run build
npm start
```

## Notes pour l’équipe technique

-   Le formulaire de contact n’envoie pas encore d’e-mails. Il faudra connecter un service ou autre pour que celà soit bien fonctionnel.
-   Les pages dynamiques comme `[slug]` utilisent `generateMetadata()` pour fournir les meta dynamiquement côté serveur.
-   Les SVG du logo sont en `fill` dur.

## Scripts disponibles

-   `npm run dev` – Lancement en mode développement
-   `npm run build` – Build de production (nécessite que tout compile correctement)
-   `npm start` – Lancement du serveur Node.js en production

## Déploiement

L'application peut être déployée sur :

-   Vercel (config automatique)
-   Serveur Node avec base de données MySQL (via Railway, PlanetScale, etc.)

## Auteur

Ce projet a été développé par un étudiant en BTS SIO passionné de développement web, dans le cadre d’un projet professionnel concret pour une agence.

Pour en savoir plus sur l’auteur, rendez-vous sur [https://pierreburnier.dev](https://pierreburnier.dev)
