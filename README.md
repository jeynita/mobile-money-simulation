# Simulation Mobile Money

Application console en **Java** qui simule les fonctionnalités essentielles d'un service de Mobile Money : création de clients, dépôts, retraits et consultation de l'historique. Les données sont persistées dans **MySQL** via **JDBC**.

Projet réalisé dans le cadre du DUT2 à l'École Supérieure Polytechnique de Dakar.

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

### Diagramme de classes

![Diagramme de classes UML](Diagramme_Classe.png)

## Technologies

- Java 17
- MySQL (via XAMPP)
- JDBC (`mysql-connector-j-9.5.0.jar`)
- UML 2.0 (Draw.io)

## Installation

### Prérequis

- Java JDK 17+
- XAMPP (MySQL + phpMyAdmin)
- Driver JDBC `mysql-connector-j-9.5.0.jar` placé dans le dossier `/lib`

### Base de données

1. Démarrer **Apache** et **MySQL** depuis XAMPP.
2. Créer la base `simulation_mobile_money`.
3. Importer le script `database.sql` (via phpMyAdmin, onglet *Importer*, ou en ligne de commande) :

```sql
SOURCE database.sql;
```

### Lancement

```bash
git clone https://github.com/jeynita/Simulation_Mobile_Money.git
cd Simulation_Mobile_Money
# Compiler et lancer (adapte le chemin de la classe principale)
javac -cp "lib/*" -d out $(find src -name "*.java")
java -cp "out:lib/*" <PackageDeLaClassePrincipale>.Main
```

> Sous Windows, remplace `:` par `;` dans le classpath.
> Vérifie l'URL, l'utilisateur et le mot de passe MySQL dans la classe de connexion.

## Exemples d'utilisation

**Créer un client**
- Menu : *Créer un Client*
- Entrées : nom (ex : DIA), prénom (ex : Abdou), téléphone (ex : 77XXXXXXX)
- Résultat : le client est enregistré en base et un numéro de compte est généré.

**Faire un dépôt**
- Menu : *Faire un dépôt*
- Entrées : numéro de compte, montant (ex : 25 000 FCFA)
- Résultat : le solde est incrémenté et une ligne `DEPOT` horodatée est ajoutée dans la table `operation`.

**Consulter l'historique**
- Menu : *Historique des opérations*
- Entrée : numéro de compte
- Résultat : la liste de toutes les transactions du compte.

## Équipe

- Diarra DIA
- Dieynaba BALDE
- Rokhaya GUEYE

## Ma contribution

- J'étais en charge de la partie backend.

