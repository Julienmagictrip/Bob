# 🛠️ BOB.AI - L'Assistant de Maintenance Intelligent

> **Automatiser le diagnostic, simplifier l'intervention, valoriser l'expérience locative.**

BOB.AI est une plateforme SaaS/PWA conçue pour révolutionner la gestion technique immobilière (Airbnb, Hôtels, Gestion locative). En plaçant l'IA générative au cœur de la détection de pannes, BOB.AI réduit les interventions inutiles et optimise la chaîne de valeur du dépannage.

---

## 🎯 Enjeux et Vision (The "Why")

La maintenance immobilière souffre de trois frictions majeures que BOB.AI résout :
1.  **Le bruit opérationnel** : 40% des demandes de maintenance sont résolvables par l'utilisateur (ex: disjoncteur sauté, bouton mal enclenché). BOB.AI agit comme un filtre intelligent.
2.  **L'asymétrie d'information** : Les techniciens arrivent souvent sans avoir les bons outils car le problème a été mal décrit. L'expertise multimodale de BOB fournit un pré-diagnostic précis (Photo + Modèle).
3.  **La preuve de dommage (AirCover)** : En cas de dégradation par le voyageur, BOB.AI collecte immédiatement les preuves (photos, horodatage) facilitant les demandes de remboursement auprès des assurances ou plateformes (Airbnb).

---

## 🧠 Logique du Projet (The "How")

### 1. Le Moteur de Diagnostic (Wizard v2)
Contrairement aux chatbots classiques basés sur des arbres de décision rigides, BOB.AI utilise un **flux itératif dynamique** piloté par Gemini 2.5 Flash.
*   **Contexte-Aware** : L'IA reçoit l'historique complet, les spécifications de l'appareil et l'analyse visuelle de la photo.
*   **JSON-Direct-Rendering** : L'IA ne "discute" pas seulement ; elle dicte l'interface. Si elle a besoin d'une info, elle renvoie un type `question` avec des boutons générés à la volée. Si elle a la solution, elle renvoie un type `diagnosis` avec des étapes illustrées.

### 2. Écosystème Multi-Rôles
Le projet n'est pas qu'un outil de chat, c'est un **ERP de maintenance léger** :
*   **Locataire/Voyageur** : Accès instantané via QR Code (PWA), diagnostic guidé, sentiment d'accompagnement 24/7.
*   **Conciergerie/Gestionnaire** : Dashboard centralisé, tri automatique par priorité, gestion financière (Devis/Factures).
*   **Artisans/Techniciens** : Une "place de marché" interne où les professionnels reçoivent des missions qualifiées avec un dossier technique complet avant même de se déplacer.

---

## 🏗️ Stratégie de Conception et Développement

### Choix de l'Architecture
*   **React 19 & TypeScript** : Pour une robustesse maximale des types de données, cruciale lors de l'échange de JSON complexes avec l'IA.
*   **Modèle "AI-first"** : Nous avons déplacé l'intelligence métier du code (hardcoded logic) vers le Prompt Engineering (`geminiService.ts`). Cela permet de supporter de nouvelles catégories d'appareils sans modifier une ligne de code UI.
*   **Approche Multimodale** : Le support natif de la vision permet à l'IA d'identifier des pièces défectueuses ou de lire des codes d'erreur sur des affichages numériques, ce qu'un utilisateur ne sait pas toujours faire.

### Sécurité et Performance
*   **Optimisation des Tokens** : Utilisation de modèles "Flash" pour garantir une réponse en moins de 2 secondes, indispensable pour une expérience utilisateur fluide sur mobile.
*   ** découplage IA/UI** : L'interface est conçue pour être "résiliente" (Graceful Degradation). Si l'IA échoue, le système bascule automatiquement sur un formulaire d'escalade standard.

---

## 🚀 Stack Technique

*   **Frontend** : Vite + React 19 + TypeScript.
*   **Design** : Tailwind CSS (Glassmorphism & Mobile-first).
*   **Intelligence** : Google Generative AI SDK (Gemini 2.5 Flash).
*   **Data/Backend** : Firebase (Scalabilité & Temps réel).

---

## 🛠️ Guide d'Installation Rapide

1.  **Clonage & Install** : `npm install`
2.  **Configuration** : Créer un `.env.local` avec `GEMINI_API_KEY`.
3.  **Lancement** : `npm run dev`

---

*BOB.AI transforme chaque problème technique en une expérience fluide et documentée.*
