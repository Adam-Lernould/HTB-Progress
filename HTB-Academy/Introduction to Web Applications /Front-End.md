# Front End : Introduction et Sécurité

Ce document couvre les points clés liés au **Front End** dans une application Web :  
- Structure et rôles du Front End  
- Vulnérabilités majeures (avec **exemples** concrets)  
- Meilleures pratiques pour s’en prémunir  

---

## 1. Qu’est-ce que le Front End ?
Le **Front End** est la partie visible et interactive d’une application Web, exécutée dans le navigateur de l’utilisateur. Il repose sur :
- **HTML** : structure de la page (titres, paragraphes, formulaires…).  
- **CSS** : style et mise en forme (layouts, couleurs, animations…).  
- **JavaScript** : interactivité, mise à jour dynamique du contenu, requêtes AJAX/Fetch.

**Objectif principal** : offrir une expérience utilisateur fluide (UI/UX) et gérer l’affichage des données renvoyées par le Back End.

---

## 2. Architecture Front End
1. **HTML**  
   - Définit la sémantique et la structure.  
   - Utilise des balises (`<div>`, `<form>`, `<a>`, etc.) pour décrire les éléments de la page.
2. **CSS**  
   - Sépare la présentation de la structure.  
   - Évite d’avoir du style inline directement dans le HTML (bonnes pratiques).
3. **JavaScript**  
   - Permet d’écouter les événements (clic, soumission de formulaire…), de modifier le DOM, et de communiquer avec le serveur via AJAX/Fetch/WebSockets.
   
**Notion de Frameworks** : On peut utiliser des outils comme **React**, **Vue**, **Angular** ou des bibliothèques comme **jQuery** pour accélérer le développement.

---

## 3. Vulnérabilités Courantes côté Front End

### 3.1 Exposition de Données Sensibles
- Informations critiques (ex. mot de passe, clé API) présentes en clair dans le code JavaScript ou dans les commentaires HTML.
- **Risque** : un simple « View Source » ou un outil de débogage peut révéler ces informations.

#### Exemple
```html
<!-- Mauvais exemple -->
<!-- ATTENTION : Clé d’API exposée dans un commentaire -->
<!-- API_KEY = "1234-SECRET-5678" -->

<script>
  // Mauvais exemple : mot de passe admin stocké en clair
  const adminPassword = "SuperSecret123!";
  console.log(`Le mot de passe est : ${adminPassword}`);
</script>
```

### 3.2 Cross-Site Scripting (XSS)
- Insertion de code malveillant (souvent JavaScript) dans la page, exécuté par le navigateur.
- Causes : absence de filtrage/sanitisation des entrées utilisateur (formulaires, URL…).

#### Exemple
```html
<!-- Page vulnérable : recherche.php -->
<!DOCTYPE html>
<html>
<head>
  <title>Recherche</title>
</head>
<body>
  <form action="search.php" method="get">
    <input type="text" name="q">
    <button type="submit">Rechercher</button>
  </form>

  <!-- Suppose qu'on affiche la recherche sans encodage -->
  Vous avez cherché : <?php echo $_GET['q']; ?>
</body>
</html>
```
- Si l’utilisateur saisit <script>alert('XSS');</script>, le script s’exécute.

### 3.3 HTML Injection
-Forme plus basique d’injection, où l’attaquant insère du contenu HTML non souhaité.
- Peut se traduire par du défacement (changement de l’interface) ou un faux formulaire (phishing).

#### Exemple
```html
<!-- Mauvais usage de innerHTML -->
<div id="result"></div>
<script>
  // Suppose qu'on récupère une saisie utilisateur
  // et qu'on l'injecte directement sans aucun contrôle
  document.getElementById('result').innerHTML = userInput;
</script>
```
- Avec userInput contenant par exemple "<h1>Hacked!</h1>", la page est modifiée.

### 3.4 Cross-Site Request Forgery (CSRF)
- Exploite la session active de l’utilisateur (via cookies ou tokens) pour effectuer une action à son insu.
- Ex. : Cliquer sur un lien malveillant qui déclenche une requête (GET ou POST) modifiant un mot de passe ou supprimant un compte.

#### Exemple :
```html
<!-- Image invisible déclenchant une requête dangereuse -->
<img src="https://victime.com/delete-account?user=admin" style="display:none"/>
```

### 4 Ressources Conseillées

- MDN Web Docs : documentation complète sur HTML, CSS, JS.
- OWASP Top 10 : classification des vulnérabilités Web les plus fréquentes.
- OWASP Cheat Sheets : fiches pratiques pour prévenir XSS, CSRF, etc.

