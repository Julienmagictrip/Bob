# 🛠️ BOB.AI - Assistant de Maintenance Intelligent

BOB.AI est une application web progressive (PWA) conçue pour simplifier le diagnostic et la résolution des problèmes de maintenance dans les appartements (notamment pour la location courte durée). Elle combine une interface utilisateur intuitive avec la puissance de l'IA (Gemini) pour guider les utilisateurs vers une solution ou faciliter l'escalade vers un professionnel.

---

## 🚀 Stack Technique

*   **Framework** : React 19 (TypeScript)
*   **Module Bundler** : Vite 6
*   **Langage** : TypeScript 5.8
*   **IA** : Google Generative AI (SDK `@google/genai`) - Modèle `gemini-2.5-flash`
*   **Styles** : Tailwind CSS (Vanilla CSS pour les composants spécifiques)
*   **Back-end** : Firebase (Configuré pour la persistance des données)

---

## 🏗️ Architecture du Projet

Le projet est structuré de manière modulaire pour séparer la logique de rendu, les services de données et les définitions de types.

### 📁 Structure des dossiers
*   `/src` (ou racine)
    *   `App.tsx` : Composant principal gérant l'état de navigation (Wizard) et l'orchestration des écrans.
    *   `/components` : Composants UI réutilisables, notamment `icons.tsx` pour le système d'icônes SVG.
    *   `/services` : Logique métier externe, principalement `geminiService.ts` pour les appels à l'IA.
    *   `types.ts` : Centralisation de tous les types TypeScript (Interfaces, Enums, Aliases).
    *   `firebase.ts` : Initialisation et configuration de la couche de données.

### 🔄 Flux de Diagnostic (The Wizard)
L'application fonctionne comme une machine à états gérée par la variable `step` dans `App.tsx`.
1.  **LANDING** : Accueil et présentation.
2.  **CATEGORY_SELECTION** : Choix de la famille de problème (Plomberie, Électricité, etc.).
3.  **APPLIANCE_SELECTION** : Choix de l'équipement spécifique.
4.  **APPLIANCE_DETAILS** : Saisie optionnelle de la marque/modèle et capture photo.
5.  **DIAGNOSIS** : Dialogue itératif avec l'IA.
6.  **RESULT** : Affichage de la solution ou proposition d'intervention.

---

## 🧠 Intégration de l'IA (Gemini)

La logique de diagnostic réside dans `services/geminiService.ts`.

*   **Format de réponse** : L'IA répond exclusivement en JSON pour permettre un rendu UI dynamique.
    *   Type `question` : Pour demander des précisions.
    *   Type `diagnosis` : Fournit une solution structurée (`solutionType`, `title`, `steps`, `summary`).
*   **Multimodalité** : Le service supporte l'envoi de photos (base64) à l'IA pour améliorer la précision du diagnostic visuel.
*   **Contrôle** : Utilisation de `systemInstruction` pour forcer l'IA à rester dans son rôle d'expert en maintenance.

---

## 🏢 Espace Pro (Backoffice)

BOB.AI inclut un tableau de bord complet pour les gestionnaires (Concierges) et les techniciens (Artisans).

### Fonctions Concierge :
*   Gestion des propriétés et des tickets d'incidents.
*   Suivi des dossiers **AirCover** (dommages causés par les voyageurs).
*   Validation des devis et gestion des factures.

### Fonctions Artisan :
*   Réception de "Leads" (opportunités de chantier) avec diagnostic IA pré-rempli.
*   Envoi de devis chiffrés.
*   Gestion du planning d'intervention et profil public (notes/avis).

---

## 🛠️ Installation et Installation

### Pré-requis
*   Node.js (v18+)
*   Clé API Google Gemini

### Installation
1.  `npm install`
2.  Créez un fichier `.env.local` à la racine :
    ```bash
    GEMINI_API_KEY=votre_cle_api_ici
    ```
3.  Lancement en mode dev :
    ```bash
    npm run dev
    ```

---

## 📝 Types Clés (à consulter dans `types.ts`)

*   `Ticket` : Objet central pour le suivi d'un incident.
*   `AiResponse` : Union type (`question` | `diagnosis`) dictant le comportement du Wizard.
*   `BackofficeRole` : Gère les permissions d'affichage (`CONCIERGE` vs `ARTISAN`).

---

*Développé avec passion pour automatiser la maintenance immobilière.*
