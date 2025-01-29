# Front End : Structure, Vulnérabilités & Bonnes Pratiques

Ce document couvre les aspects essentiels du **Front End** dans une application Web :
- Structure et rôles
- Vulnérabilités majeures avec exemples
- Bonnes pratiques de sécurité

---

## 1. Qu’est-ce que le Front End ?
Le **Front End** est la partie visible et interactive d’une application Web, exécutée dans le navigateur.  
**Technologies principales :**
- **HTML** : Structure de la page.
- **CSS** : Styles et mise en forme.
- **JavaScript** : Interactivité et dynamisme.

**Objectif :** Offrir une expérience utilisateur fluide et gérer l’affichage des données du Back End.

---

## 2. Architecture Front End
1. **HTML** : Définit la structure avec des balises (`<div>`, `<form>`, etc.).
2. **CSS** : Sépare la présentation de la structure, évite les styles inline.
3. **JavaScript** : Gère les événements, modifie le DOM, communique avec le serveur via AJAX/Fetch.

**Frameworks courants :** React, Vue, Angular, jQuery.

---

## 3. Vulnérabilités Courantes côté Front End

### 3.1 Exposition de Données Sensibles
- **Description :** Informations critiques en clair dans le code.
- **Exemple :**
    ```html
    <script>
      const apiKey = "1234-SECRET-5678";
      console.log(apiKey);
    </script>
    ```
- **Prévention :** Ne jamais stocker de secrets côté client. Utiliser des appels sécurisés côté serveur.

---

### 3.2 Cross-Site Scripting (XSS)
- **Description :** Insertion de scripts malveillants via des entrées non filtrées.
- **Exemple :**
    ```html
    <p>Recherche : <?php echo $_GET['q']; ?></p>
    ```
    Saisie : `<script>alert('XSS');</script>`
- **Prévention :** Valider et encoder les données, utiliser Content Security Policy (CSP).

---

### 3.3 HTML Injection
- **Description :** Injection de contenu HTML non souhaité.
- **Exemple :**
    ```html
    <div id="result"></div>
    <script>
      document.getElementById('result').innerHTML = userInput;
    </script>
    ```
- **Prévention :** Filtrer et échapper le contenu, éviter `innerHTML` non sécurisé.

---

### 3.4 Cross-Site Request Forgery (CSRF)
- **Description :** Exploitation de la session active pour des actions non autorisées.
- **Exemple :**
    ```html
    <img src="https://victime.com/delete-account?user=admin" style="display:none"/>
    ```
- **Prévention :** Utiliser des tokens CSRF uniques, demander des confirmations supplémentaires.

---

## 4. Bonnes Pratiques (Front End)
1. **Validation & Encodage des Entrées** : Côté client et serveur.
2. **Séparation du Code** : HTML, CSS, JS bien distincts.
3. **Headers de Sécurité** : CSP, X-XSS-Protection, Strict-Transport-Security.
4. **Gestion des Sessions** : Cookies sécurisés (`Secure`, `HttpOnly`, `SameSite`).
5. **Mise à Jour des Bibliothèques** : Maintenir à jour React, Vue, Angular, etc.

---

## 5. Ressources Recommandées
- **[MDN Web Docs](https://developer.mozilla.org/)**
- **[OWASP Top 10](https://owasp.org/www-project-top-ten/)**
- **[OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)**

---

**Pour contribuer :**  
- Ouvrez une _Issue_ pour toute question ou suggestion.  
- Créez une _Pull Request_ pour apporter des améliorations ou corriger des erreurs.

Fin du document Front End.
