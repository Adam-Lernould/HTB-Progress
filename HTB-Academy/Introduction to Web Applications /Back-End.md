# Back End : Serveurs, Bases de Données & Sécurité

Ce document aborde les aspects essentiels du **Back End** dans une application Web :
- Composants principaux
- Types de bases de données
- Vulnérabilités publiques
- Bonnes pratiques de sécurité

---

## 1. Back End Servers

### Définition
Le **serveur Back End** héberge les applications nécessaires au fonctionnement de l'application Web, intégrant la logique métier et l'accès aux données.

### Composants Software
- **Web Server** : Gère le trafic HTTP (Apache, NGINX, IIS).
- **Database** : Stocke les données (MySQL, PostgreSQL, MongoDB).
- **Development Framework** : Facilite le développement (Laravel, Express, Django, Rails).

### Stacks Communes
- **LAMP** : Linux, Apache, MySQL, PHP.
- **WAMP** : Windows, Apache, MySQL, PHP.
- **WINS** : Windows, IIS, .NET, SQL Server.
- **MAMP** : macOS, Apache, MySQL, PHP.
- **XAMPP** : Cross-Platform, Apache, MySQL, PHP/PERL.

---

## 2. Web Servers

### Définition
Un **web server** traite les requêtes HTTP des navigateurs clients et sert les ressources demandées.

### Codes de Réponse HTTP Courants
| Code | Description |
|------|-------------|
| **200 OK** | Requête réussie. |
| **301 Moved Permanently** | Ressource déplacée définitivement. |
| **404 Not Found** | Ressource non trouvée. |
| **500 Internal Server Error** | Erreur serveur. |

### Exemples de Web Servers
1. **Apache**
   - Populaire et extensible via des modules.
   - Utilisé par Apple, Adobe, Baidu.
2. **NGINX**
   - Optimisé pour les requêtes concurrentes.
   - Utilisé par Google, Facebook, Netflix.
3. **IIS**
   - Intégré à Windows Server.
   - Utilisé par Microsoft, Office365, Dell.

**Exemple de commande cURL :**
```bash
# Vérifier les en-têtes HTTP
curl -I https://academy.hackthebox.com

# Obtenir le contenu de la page
curl https://academy.hackthebox.com
```

## 3. Databases

### Types de Bases de Données
1. Relational (SQL)
Structure : Tables, lignes, colonnes.
Exemples : MySQL, MSSQL, Oracle, PostgreSQL.
Avantages : Relations claires, requêtes complexes.

2. Non-relational (NoSQL)
Structure : Key-Value, Document-Based, Wide-Column, Graph.
Exemples : MongoDB, ElasticSearch, Cassandra.
Avantages : Scalabilité, flexibilité.

### Utilisation dans les Applications Web

#### Exemple
```php
// Connexion à la base de données
$conn = new mysqli("localhost", "user", "pass");

// Création d'une nouvelle base de données
$sql = "CREATE DATABASE database1";
$conn->query($sql);

// Connexion et requête
$conn = new mysqli("localhost", "user", "pass", "database1");
$query = "SELECT * FROM table_1";
$result = $conn->query($query);

// Affichage des résultats
while($row = $result->fetch_assoc()) {
    echo $row["name"] . "<br>";
}
```
## 4. Vulnérabilités Communes du Back End
### 4.1 Broken Authentication/Access Control
Broken Authentication : Bypass des fonctions d'authentification.
Exemple : Auth Bypass avec " ' or 0=0 # ".
Broken Access Control : Accès non autorisé à des ressources.
Exemple : Utilisateur normal accède au panneau admin.

### 4.2 Malicious File Upload
Description : Upload de scripts malveillants via des fonctionnalités non sécurisées.
Exemple : Plugin WordPress "Responsive Thumbnail Slider 1.0" permet shell.php.jpg.

### 4.3 Command Injection
Description : Injection de commandes OS via entrées non filtrées.
Exemple : Plugin WordPress "Plainview Activity Monitor" permet | COMMAND....

### 4.4 SQL Injection (SQLi)
Description : Injection de requêtes SQL malveillantes.
Exemple : Authentification SQLi permettant un accès sans identifiants.


