# 🏭 Absolut Warehouse

**Absolut Warehouse** est une application **client–serveur distribuée** conçue pour la gestion d’entrepôt.  
Elle repose sur une architecture multi‑composants : un **client Python**, un **serveur applicatif Java**, une **base PostgreSQL**, ainsi qu’un **serveur web PHP** pour la consultation.

---

## 🧩 Architecture globale

### 🖥 1. Client applicatif
- **Langage :** Python  
- **Rôle :** Interface utilisée par les opérateurs sur le terrain  
- **Communication :** Envoie des commandes textuelles via **TCP** vers le serveur Java  
- **Protocole :** Protocole personnalisé basé sur des commandes (`ADD`, `READ`, `MODIFY`, `DELETE`.)

---

### ⚙️ 2. Serveur applicatif (Java)
- **Langage :** Java 17+  
- **Rôle :**
  - Authentification du terminal
  - Validation des permissions via `server_config.json`
  - Traitement des commandes et logique métier
  - Communication directe avec PostgreSQL
- **Composants internes :**
  - `SocketServer` : gestion TCP multi‑thread
  - `ClientListener` : gestion du flux entrant
  - `DatabaseManager` : Query Builder interne (SELECT / INSERT / UPDATE / DELETE)
  - `ActionConfig` : permissions dynamiques
  - `DbUtils` : traitements DB (réservations, parseurs, utilitaires)

---

### 🗃 3. Base de données (PostgreSQL)
- Stocke :
  - Items
  - Espaces de stockage
  - Terminaux et permissions
- Communication : **SQL via TCP**
- Le serveur Java gère toutes les transactions.

---

### 🌐 4. Serveur web (PHP)
- Utilisé pour la **consultation** et **création de comptes**
- Communique directement avec PostgreSQL
- Protocole : **HTTP + SQL**

---

## ⚡ Vue d’ensemble des technologies

| Composant             | Technologie | Protocole(s) |
|-----------------------|-------------|--------------|
| Client applicatif     | Python      | TCP          |
| Serveur applicatif    | Java        | SQL          |
| Base de données       | PostgreSQL  | SQL          |
| Serveur web           | PHP         | HTTP / SQL   |

---

## 📊 Schéma d’architecture

![Architecture réseau](./réseaux.drawio.png)

---

## 📦 Fonctionnalités principales

### ✔ Communication client–serveur
- Protocole textuel simple et robuste
- Thread dédié par client
- Gestion des erreurs et réponses normalisées

### ✔ Système de Permissions
- Basées sur un système simple (`R-`, `-W`, `RW`)
- Définies dans `server_config.json`

### ✔ Gestion de stock :
- Ajout, consultation, modification et suppression d’items
- Visualisation des données par le client disponible en ligne

### ✔ Base de données centralisée
- PostgreSQL fiable, robuste, transactionnelle

### ✔ Interface web complémentaire
- Permet au client de se créer un compte afin d'avoir des livraisons associé
- Le client authentifier peut voir toutes les commandes qui sont lié à lui

---

## 🚀 Installation

### Serveur Java
Simple Main à éxécuter (et Config à préciser).

### Client Python
Simple Main à éxécuter (et Config à préciser).

### Serveur web
À déployer sur un serveur PHP + PostgreSQL.

---

## 🧑‍💻 Auteurs
Projet réalisé par **Thomas Hornung**, **Haohan Yu** et **Gauthier Defrance**  
Dans le cadre d’un projet universitaire à **CY Université**

---

