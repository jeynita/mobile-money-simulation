# Simulation Mobile Money

> Application console Java qui simule les opérations essentielles d'un service de Mobile Money : clients, dépôts, retraits et historique.

![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![JDBC](https://img.shields.io/badge/JDBC-007396?style=flat-square&logo=openjdk&logoColor=white)
![UML](https://img.shields.io/badge/UML-2.0-informational?style=flat-square)

Projet d'équipe réalisé dans le cadre du DUT2 Informatique à l'École Supérieure Polytechnique de Dakar. Les données sont persistées dans **MySQL** via **JDBC**.

## Fonctionnalités

- Création d'un client avec génération automatique d'un numéro de compte
- Dépôt sur un compte
- Retrait depuis un compte
- Consultation du solde
- Historique des opérations d'un compte

## Architecture

Le projet suit une architecture **DAO (Data Access Object)** pour séparer la logique métier de l'accès aux données.

| Couche | Rôle |
|---|---|
| **Model** | Entités métier : `Client`, `Compte`, `Operation` |
| **DAO** | Accès aux données via JDBC |
| **Database** | Connexion centralisée à MySQL (pattern **Singleton**) |
| **Interface utilisateur** | Menus de l'application console |

### Diagramme de classes

![Diagramme de classes UML](Diagramme_Classe.png)

## Structure du projet

```
Simulation_Mobile_Money/
├── source/                  # Model, DAO, Database
├── interfaceUtilisateur/    # Menus console
├── lib/                     # Driver JDBC MySQL
├── main.java                # Point d'entrée
├── database.sql             # Script de création de la base
├── Diagramme_Classe.png     # Diagramme de classes
└── Diagramme_Classe.drawio  # Source du diagramme (Draw.io)
```

## Technologies

- Java 17
- MySQL (via XAMPP)
- JDBC (`mysql-connector-j-9.5.0.jar`)
- UML 2.0 (Draw.io)

## Installation

### Prérequis

- Java JDK 17+
- XAMPP (MySQL + phpMyAdmin)
- Driver `mysql-connector-j-9.5.0.jar` dans le dossier `lib/`

### Base de données

1. Démarrer **MySQL** depuis XAMPP.
2. Créer la base `simulation_mobile_money`.
3. Importer `database.sql` (phpMyAdmin, onglet *Importer*, ou en ligne de commande) :

```sql
SOURCE database.sql;
```

4. Vérifier l'URL, l'utilisateur et le mot de passe MySQL dans la classe de connexion.

### Lancement

```bash
git clone https://github.com/jeynita/Simulation_Mobile_Money.git
cd Simulation_Mobile_Money
```

Linux / macOS :
```bash
javac -cp "lib/*" -d out $(find . -name "*.java")
java -cp "out:lib/*" main
```

Windows (PowerShell) :
```powershell
javac -cp "lib/*" -d out (Get-ChildItem -Recurse -Filter *.java).FullName
java -cp "out;lib/*" main
```

Tu peux aussi ouvrir le projet dans VS Code et lancer `main.java`.

## Exemples d'utilisation

| Scénario | Entrées | Résultat |
|---|---|---|
| **Créer un client** | Nom, prénom, téléphone | Client enregistré en base, numéro de compte généré |
| **Faire un dépôt** | Numéro de compte, montant (ex : 25 000 FCFA) | Solde incrémenté, ligne `DEPOT` horodatée dans la table `operation` |
| **Faire un retrait** | Numéro de compte, montant | Solde débité, ligne `RETRAIT` ajoutée dans `operation` |
| **Consulter l'historique** | Numéro de compte | Liste de toutes les transactions du compte |


- Transfert entre comptes
- Tests unitaires
- Passage à Maven pour gérer les dépendances
