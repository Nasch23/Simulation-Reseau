# 💻 Simulateur de Réseau Local (LAN) avec STP

<h3 align="center">Un Simulateur en C pour la Commutation Ethernet et le Spanning Tree Protocol (STP)</h3>

<p align="center">
Ce projet est un simulateur en langage C, conçu pour modéliser le comportement des réseaux locaux (LAN) en intégrant les mécanismes fondamentaux de la <strong>commutation Ethernet</strong> et du protocole <strong>STP (Spanning Tree Protocol)</strong>.
</p>

---

<details>
  <summary>Table des matières</summary>
  <ol>
    <li><a href="#-fonctionnalités-clés">Fonctionnalités Clés</a></li>
    <li><a href="#-démarrer">Démarrer</a>
      <ul>
        <li><a href="#prérequis">Prérequis</a></li>
        <li><a href="#installation-et-compilation">Installation et Compilation</a></li>
      </ul>
    </li>
    <li><a href="#-utilisation">Utilisation</a></li>
    <li><a href="#-format-de-configuration-réseau">Format de Configuration Réseau</a></li>
    <li><a href="#-structure-du-projet">Structure du Projet</a></li>
    <li><a href="#-licence-et-contact">Licence et Contact</a></li>
  </ol>
</details>

---

## 💡 Fonctionnalités Clés

Ce simulateur reproduit les éléments essentiels d'un réseau local :

### 🌉 Commutation Ethernet
* **Apprentissage MAC :** Les commutateurs apprennent dynamiquement les adresses MAC des stations source et les stockent dans leurs **tables MAC**.
* **Propagation de Trames :** Gestion de la transmission des trames :
    * **Commutation Directe :** Envoi vers le port spécifique si l'adresse MAC de destination est connue.
    * **Inondation (Flooding) :** Envoi sur tous les ports actifs si la destination est inconnue.
* **Simulation de Trames :** Possibilité de simuler l'envoi d'une trame complète (MAC source/destination, données) entre deux stations, avec affichage détaillé du chemin.

### 🌳 Spanning Tree Protocol (STP)
* **Prévention de Boucles :** Calcul de l'arbre couvrant minimal pour **éliminer les boucles** dans la topologie du réseau. 

[Image of Spanning Tree Protocol network topology]

* **Rôles des Ports :** Blocage ou activation des ports selon l'algorithme STP (Root Port, Designated Port, Blocking Port).
* **Priorités :** Prise en compte de la **priorité des commutateurs** pour l'élection de la racine (Root Bridge).

### 🛠️ Outils de Visualisation
* **Affichage des Tables MAC :** Inspection des tables d'apprentissage des commutateurs.
* **État STP :** Visualisation de l'état des ports (Actif/Bloqué) après le calcul du Spanning Tree.
* **Matrice d'Adjacence :** Affichage de la topologie du réseau sous forme matricielle.
* **Interface Colorée :** Utilisation des codes ANSI pour une meilleure lisibilité dans le terminal.

---

## ▶️ Démarrer

### Prérequis

Pour compiler et exécuter le simulateur, vous aurez besoin de :
* **GCC** (GNU Compiler Collection) - Compilateur C.
* **Make** - Outil de construction.
* Un **terminal** supportant les codes ANSI (pour l'affichage en couleur).

### Installation et Compilation

1.  **Cloner le dépôt :**
    ```sh
    git clone <url-du-depot>
    cd Simulation-Reseau
    ```

2.  **Compiler le projet :** Le `Makefile` utilise des flags stricts (`-Wall -Wextra -Werror`).
    ```sh
    make
    ```
    L'exécutable `simulateur_reseau` sera généré dans le répertoire `bin/`.

3.  **Lancer le simulateur :**
    ```sh
    make run
    # ou directement :
    ./bin/simulateur_reseau reseau_config.txt
    ```

4.  **Nettoyage :** Supprimer les fichiers compilés.
    ```sh
    make clean
    ```

---

## ⚙️ Utilisation

Après le lancement avec un fichier de configuration, le simulateur affiche un **menu interactif** :

1.  **Lancer une simulation de trame :**
    * Choisissez la station **source** et la station **destination**.
    * Saisissez les données à transmettre.
    * Le simulateur détaille chaque étape du trajet de la trame (apprentissage, commutation, inondation).
2.  **Afficher l'état des ports STP :**
    * Affiche si chaque port est en état *Actif* ou *Bloqué* par le protocole STP.
3.  **Afficher les tables MAC :**
    * Liste les adresses MAC apprises par chaque commutateur et le port associé.
4.  **Afficher la matrice d'adjacence :**
    * Présente la topologie actuelle du réseau.

---

## 📝 Format de Configuration Réseau

Le réseau est défini dans un fichier texte (par défaut : `reseau_config.txt`) selon une structure simple :
