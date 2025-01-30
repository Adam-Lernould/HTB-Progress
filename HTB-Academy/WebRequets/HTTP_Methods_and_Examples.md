# 5. HTTP Methods & Codes

## 5.1 Méthodes HTTP courantes
- **GET** : Récupérer une ressource (paramètres dans l’URL).  
- **POST** : Envoyer des données (formulaires, fichiers) dans le *body*.  
- **HEAD** : Récupérer seulement les en-têtes (sans le corps).  
- **PUT** : Mettre à jour/créer une ressource sur le serveur.  
- **DELETE** : Supprimer une ressource.  
- **OPTIONS** : Obtenir les méthodes autorisées par le serveur.

## 5.2 Codes de statut
- **2xx (Succès)** : ex. `200 OK`, `201 Created`  
- **3xx (Redirection)** : ex. `301 Moved Permanently`, `302 Found`  
- **4xx (Erreur client)** : ex. `400 Bad Request`, `403 Forbidden`, `404 Not Found`  
- **5xx (Erreur serveur)** : ex. `500 Internal Server Error`

---

# 6. GET

## 6.1 Principes
- Paramètres directement dans l’URL (ex. `?search=flag`).  
- **HTTP Basic Auth** :  
  - `http://user:pass@host/`  
  - ou `curl -u user:pass http://host/`

## 6.2 Exemples
```bash
# GET avec authentification Basic
curl -u admin:admin http://<SERVER_IP>:<PORT>/
```

# 7. POST
## 7.1 Principes
1. Envoi des données dans le body (formulaire, JSON, etc.).
2. Plus discret que GET (pas stocké dans l’URL).
3. Supporte l’upload de fichiers volumineux.
## 7.2 Exemples
Formulaire de login :
```bash
curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
```
Cookie d’authentification :
```bash
curl -i -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/
# => Set-Cookie: PHPSESSID=xyz
```
Réutiliser le cookie :
```bash
curl -b 'PHPSESSID=xyz' http://<SERVER_IP>:<PORT>/
```
Envoi JSON :
```bash
curl -X POST -d '{"search":"london"}' \
     -H 'Content-Type: application/json' \
     -b 'PHPSESSID=xyz' \
     http://<SERVER_IP>:<PORT>/search.php
```
# 8. CRUD API

## 8.1 Définition

**CRUD** : *Create, Read, Update, Delete*.

**Exemple d’URL** :  

- **GET** : Lire  
- **POST** : Créer  
- **PUT** : Mettre à jour  
- **DELETE** : Supprimer  

---

## 8.2 Exemples de commandes

### Lire (Read)

```bash
curl http://<SERVER_IP>:<PORT>/api.php/city/london
```

Avec un format JSON plus lisible :
```bash
curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq
```
Créer (Create) : 
```bash
curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ \
     -d '{"city_name":"HTB_City","country_name":"HTB"}' \
     -H 'Content-Type: application/json'
```
Mettre à jour (Update) : 
```bash
curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london \
     -d '{"city_name":"New_HTB_City","country_name":"HTB"}' \
     -H 'Content-Type: application/json'
```
Supprimer (Delete) : 
```bash
curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```
# Flags & Exercices Marquants
HTTP : HTB{64$!c_cURL_u$3r}
HTTP Headers : HTB{p493_r3qu3$t$_m0n!t0r}
GET : HTB{curl_g3773r}
POST : HTB{p0$t_r3p34t3r}
CRUD API : HTB{crud_4p!_m4n!pul4t0r}























