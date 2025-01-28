# Front End : Introduction et Sécurité

Ce document couvre les points clés liés au **Front End** dans une application Web :  
- Structure et rôles du Front End  
- Vulnérabilités majeures  
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
   
**Notion de Frameworks** : On peut utiliser des outils comme React, Vue, Angular ou des bibliothèques comme jQuery pour accélérer le développement.

---

## 3. Vulnérabilités Courantes côté Front End

### 3.1 Exposition de Données Sensibles
- Informations critiques (ex. mot de passe, clé API) présentes en clair dans le code JavaScript ou dans les commentaires HTML.
- **Risque** : un simple « View Source » ou un outil de débogage peut révéler ces informations.

#### Prévention
- Ne jamais stocker d’informations sensibles côté client.  
- Utiliser des variables d’environnement et des appels sécurisés côté serveur.

---

### 3.2 Cross-Site Scripting (XSS)
- Insertion de code malveillant (souvent JavaScript) dans la page, exécuté par le navigateur.
- **Causes** : absence de filtrage/sanitisation des entrées utilisateur (formulaires, URL…).

#### Prévention
1. **Valider et encoder** toutes les données côté serveur et côté client.  
2. Utiliser des **fonctions d’échappement** pour éviter qu’un texte devienne du code.  
3. Mettre en place une **Content Security Policy** (CSP) afin de limiter l’exécution de scripts non autorisés.

---

### 3.3 HTML Injection
- Forme plus basique d’injection, où l’attaquant insère du contenu HTML non souhaité.
- Peut se traduire par du défacement (changement de l’interface) ou un faux formulaire (phishing).

#### Prévention
- Filtrer et échapper tout contenu avant de l’insérer dans le DOM.
- Éviter `innerHTML` non maîtrisé (privilégier la manipulation d’éléments DOM sécurisés).

---

### 3.4 Cross-Site Request Forgery (CSRF)
- Exploite la session active de l’utilisateur (via cookies ou tokens) pour effectuer une action à son insu.
- Ex. : Cliquer sur un lien malveillant qui déclenche une requête POST, modifiant un mot de passe ou effectuant un achat.

#### Prévention
- Implémenter un **token CSRF** unique par session, vérifié à chaque requête côté serveur.  
- Parfois, nécessiter une **confirmation supplémentaire** (re-saisir le mot de passe) pour les actions sensibles.

---

## 4. Bonnes Pratiques (Front End)

1. **Validation & Encodage des Données**  
   - Valider d’abord côté client pour améliorer l’UX (ex. formulaires).  
   - Encoder toutes les données dynamiques avant de les afficher (prévenir XSS/HTML Injection).
2. **Séparation du Code**  
   - Rester cohérent : HTML pour la structure, CSS pour le style, JS pour l’interactivité.  
   - Éviter d’encombrer le HTML avec du code inline.
3. **Utilisation de Headers de Sécurité (config serveur)**  
   - `Content-Security-Policy` (CSP) pour restreindre les sources autorisées (scripts, images…).  
   - `X-XSS-Protection`, `X-Content-Type-Options`, `Strict-Transport-Security` (pour forcer HTTPS).
4. **Gestion des Sessions**  
   - Cookies sécurisés : `Secure`, `HttpOnly`, `SameSite`.  
   - Expiration de session et renouvellement de token.
5. **Mise à Jour des Bibliothèques**  
   - Frameworks front end (React, Vue, Angular), libraries (jQuery…), packages NPM.  
   - Les versions obsolètes peuvent contenir des failles.

---

## 5. Ressources Conseillées
- **[MDN Web Docs](https://developer.mozilla.org/)** : documentation complète sur HTML, CSS, JS.  
- **[OWASP Top 10](https://owasp.org/www-project-top-ten/)** : classification des vulnérabilités Web les plus fréquentes.  
- **[OWASP Cheat Sheets](https://cheatsheetseries.owasp.org/)** : fiches pratiques pour prévenir XSS, CSRF, etc.

---

