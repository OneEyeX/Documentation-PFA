
# 📘 User Info API Endpoint

Récupère les informations du profil utilisateur actuellement authentifié à l’aide d’un token JWT.

---

## 🔗 Endpoint

* **URL**: `http://localhost:8081/api/users/info`
* **Method**: `GET`
* **Auth Required**: ✅ Oui (JWT Bearer Token)

---

## 🔐 Headers

| Clé           | Valeur                  |
| ------------- | ----------------------- |
| Authorization | Bearer `<access_token>` |

Exemple :

```
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJ...
```

---

## 📥 Request Body

Aucun corps requis pour cette requête.

---

## ✅ Réponse : 200 OK

```json
{
  "sub": "57e82cc1-eee7-4f06-a348-63e848dd4c83",
  "email_verified": true,
  "gender": "Male",
  "name": "colocataire colocap updated 3",
  "preferred_username": "coloc",
  "given_name": "colocataire",
  "family_name": "colocap updated 3",
  "email": "coclo@col.com"
}
```

| Champ               | Type    | Description                        |
| ------------------- | ------- | ---------------------------------- |
| sub                 | string  | ID unique de l’utilisateur         |
| email\_verified     | boolean | L'email a-t-il été vérifié ?       |
| gender              | string  | Genre de l’utilisateur             |
| name                | string  | Nom complet (prénom + nom)         |
| preferred\_username | string  | Nom d’utilisateur préféré (pseudo) |
| given\_name         | string  | Prénom                             |
| family\_name        | string  | Nom de famille                     |
| email               | string  | Adresse e-mail                     |

---

## ❌ Erreurs possibles

| Code HTTP | Message      | Cause                              |
| --------- | ------------ | ---------------------------------- |
| 401       | Unauthorized | Token manquant, invalide ou expiré |
| 403       | Forbidden    | Accès refusé                       |

---

# 📘 Update User Profile API Endpoint

Met à jour les informations du profil d'un utilisateur dans le système (Keycloak).

---

## 🔗 Endpoint

* **URL**: `http://localhost:8081/api/users/{userId}`
* **Method**: `PUT`
* **Auth Required**: ✅ Oui (JWT Bearer Token)

### Paramètres

* **userId** : L'ID de l'utilisateur à mettre à jour (par exemple `57e82cc1-eee7-4f06-a348-63e848dd4c83`).

---

## 🔐 Headers

| Clé           | Valeur                  |
| ------------- | ----------------------- |
| Authorization | Bearer `<access_token>` |

Exemple :

```
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJ...
```

---

## 📥 Request Body

Les données à mettre à jour pour l’utilisateur spécifié. Voici un exemple de payload valide :

```json
{
  "username": "chedlyCH",
  "firstName": "chedli",
  "lastName": "ch",
  "enabled": true,
  "birth_date": "1999-01-27",
  "gender": "Male",
  "phone_number": "55987632"
}
```

| Champ         | Type    | Description                                      |
| ------------- | ------- | ------------------------------------------------ |
| username      | string  | Nouveau nom d'utilisateur                        |
| firstName     | string  | Prénom de l'utilisateur                          |
| lastName      | string  | Nom de famille de l'utilisateur                  |
| enabled       | boolean | Indique si l'utilisateur est activé (true/false) |
| birth\_date   | string  | Date de naissance (format : YYYY-MM-DD)          |
| gender        | string  | Genre de l'utilisateur (ex: Male, Female)        |
| phone\_number | string  | Numéro de téléphone de l'utilisateur             |

---

## ✅ Réponse : 200 OK

Si la mise à jour réussit, vous recevrez la réponse suivante :

```json
{
  "message": "User profile updated successfully.",
  "status": "success"
}
```

---

## ❌ Erreurs possibles

1. **400 Bad Request** - Lorsque des données nécessaires sont manquantes ou mal formatées dans la requête.

   Exemple :

   ```json
   {
     "message": "Failed to update user in Keycloak: {\"errorMessage\":\"User name is missing\"}",
     "status": "error"
   }
   ```

2. **409 Conflict** - Lorsque le nom d'utilisateur que vous essayez de définir existe déjà dans le système.

   Exemple :

   ```json
   {
     "message": "Failed to update user in Keycloak: {\"errorMessage\":\"User exists with same username\"}",
     "status": "error"
   }
   ```

---

## Exemple de réponse avec code de succès 200

```json
{
  "message": "User profile updated successfully.",
  "status": "success"
}
```

---

# 📘 Get User by ID API Endpoint

Récupère les informations d'un utilisateur dans le système (Keycloak) en fonction de son identifiant.

---

## 🔗 Endpoint

* **URL**: `http://localhost:8081/api/users/{userId}`
* **Method**: `GET`
* **Auth Required**: ✅ Oui (JWT Bearer Token)

### Paramètres

* **userId** : L'ID de l'utilisateur à récupérer (par exemple `57e82cc1-eee7-4f06-a348-63e848dd4c83`).

---

## 🔐 Headers

| Clé           | Valeur                  |
| ------------- | ----------------------- |
| Authorization | Bearer `<access_token>` |

Exemple :

```
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJ...
```

---

## 📥 Request Body

Aucun corps n'est requis pour cette requête.

---

## ✅ Réponse : 200 OK

Si la requête réussit, vous recevrez la réponse suivante avec les détails de l'utilisateur :

```json
{
  "id": "57e82cc1-eee7-4f06-a348-63e848dd4c83",
  "username": "chedlych",
  "firstName": "chedli",
  "lastName": "ch",
  "emailVerified": true,
  "attributes": {
    "gender": ["Male"],
    "birth_date": ["1999-01-27"],
    "phone_number": ["55987632"]
  },
  "createdTimestamp": 1741285282057,
  "enabled": true,
  "totp": false,
  "disableableCredentialTypes": [],
  "requiredActions": [],
  "federatedIdentities": [],
  "notBefore": 0,
  "access": {
    "manageGroupMembership": true,
    "view": true,
    "mapRoles": true,
    "impersonate": true,
    "manage": true
  }
}
```

---

## ❌ Erreurs possibles

1. **404 Not Found** - Lorsque l'utilisateur avec l'ID spécifié n'est pas trouvé.

   Exemple :

   ```json
   {
     "error": "Keycloak Error",
     "message": "{\"error\":\"User not found\"}",
     "status": 404
   }
   ```

2. **401 Unauthorized** - Lorsque l'authentification est invalide ou absente. Assurez-vous que le token JWT est valide.

---

## Exemple de réponse en cas de succès (code 200)

```json
{
  "id": "57e82cc1-eee7-4f06-a348-63e848dd4c83",
  "username": "chedlych",
  "firstName": "chedli",
  "lastName": "ch",
  "emailVerified": true,
  "attributes": {
    "gender": ["Male"],
    "birth_date": ["1999-01-27"],
    "phone_number": ["55987632"]
  },
  "createdTimestamp": 1741285282057,
  "enabled": true,
  "totp": false,
  "disableableCredentialTypes": [],
  "requiredActions": [],
  "federatedIdentities": [],
  "notBefore": 0,
  "access": {
    "manageGroupMembership": true,
    "view": true,
    "mapRoles": true,
    "impersonate": true,
    "manage": true
  }
}
```

---

# 📄 Get Users Endpoint

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/users`
- **Méthode** : `GET`
- **Authentification requise** : Oui (Bearer Token)
- **Code succès** : `200 OK`
- **Code erreur** : `401 Unauthorized` si le token est manquant ou invalide

---

## 📥 Paramètres de requête (Filtres optionnels)

Vous pouvez filtrer les résultats à l’aide des paramètres de requête. Tous sont facultatifs.

| Paramètre   | Description                             |
|------------|-----------------------------------------|
| `username`  | Filtrer par nom d'utilisateur exact     |
| `firstName` | Filtrer par prénom exact                |
| `lastName`  | Filtrer par nom de famille exact        |
| `email`     | Filtrer par adresse e-mail exacte       |

> Exemple :
```bash
GET /api/users?username=admin2&firstName=chedli
```

Si aucun paramètre n’est fourni, l’API renvoie tous les utilisateurs disponibles.

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l’en-tête de la requête.

### Exemple d'en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

---

## 📤 Format de la réponse

La réponse est un tableau JSON contenant zéro ou plusieurs objets utilisateur.

### Exemple d'objet utilisateur :
```json
{
    "id": "86c13de2-7fdb-4ee6-a547-e9266ad19b0a",
    "username": "admin2",
    "firstName": "chedli",
    "lastName": "CHAHED",
    "email": "admin@admin.com",
    "emailVerified": false,
    "attributes": {
        "gender": ["Male"],
        "phone_number": ["5595188614"],
        "birth_date": ["2025-03-20"]
    },
    "createdTimestamp": 1741285187386,
    "enabled": true,
    "totp": false,
    "disableableCredentialTypes": [],
    "requiredActions": [],
    "notBefore": 0,
    "access": {
        "manageGroupMembership": true,
        "view": true,
        "mapRoles": true,
        "impersonate": true,
        "manage": true
    }
}
```

---

## ✅ Exemples de requêtes

### Récupérer tous les utilisateurs :
```bash
GET http://localhost:8081/api/users
Authorization: Bearer <votre_token>
```

### Récupérer un utilisateur avec le nom d'utilisateur `admin2` :
```bash
GET http://localhost:8081/api/users?username=admin2
Authorization: Bearer <votre_token>
```

---

## ❌ Gestion des erreurs

| Code HTTP | Description                              |
|----------|-------------------------------------------|
| `401`    | Le token Bearer est manquant ou invalide |

---

## 🧪 Notes importantes

- Les champs horaires comme `createdTimestamp` sont en **timestamp Unix en millisecondes**.
- Certains utilisateurs peuvent avoir des actions obligatoires listées dans `requiredActions`, comme `"TERMS_AND_CONDITIONS"` ou `"VERIFY_PROFILE"`.
- Le statut de vérification de l'e-mail (`emailVerified`) peut être `true` ou `false`.

---
Voici la documentation de l'API `/api/colocations` en français, sous forme d'un README pour un ami :

---

# 📄 Documentation de l'API Colocation

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations`
- **Méthode** : `GET`
- **Authentification requise** : Oui (Bearer Token)
- **Code succès** : `200 OK` 
- **Format de réponse** : JSON

---

## 📥 Paramètres de requête (Filtres et Pagination)

| Paramètre | Description |
|----------|-------------|
| `page`   | Numéro de la page à récupérer (commence à 1) |
| `size`   | Nombre d'éléments par page |
| `search` | Terme de recherche optionnel (par exemple : nom de ville, adresse, etc.) |

> Exemple :
```bash
GET /api/colocations?page=1&size=1&search=sss
```

---

## 🔐 Authentification

Cette API ne nécessite pas un **token Bearer** 
---

## 📤 Format de la réponse

La réponse est un objet JSON contenant une liste paginée de colocations avec leurs détails.

### Exemple de réponse (succès - 200 OK) :

```json
{
    "content": [
        {
            "id": 4,
            "name": "admin",
            "idOfPublisher": "86c13de2-7fdb-4ee6-a547-e9266ad19b0a",
            "nameOfPublisher": "admin2",
            "address": "aa",
            "city": "za",
            "postalCode": "azza",
            "description": "xccx",
            "price": 52.0,
            "numberOfRooms": 1,
            "roommatesGenderPreference": "MALE",
            "hasWifi": true,
            "hasParking": null,
            "hasAirConditioning": true,
            "isFurnished": null,
            "hasBalcony": null,
            "hasPrivateBathroom": true,
            "maxRoommates": 3,
            "currentRoommates": 2,
            "status": "yes",
            "rules": ["no", "no"],
            "tags": ["yes", ""],
            "imageUrls": ["image"],
            "averageRating": 0.0,
            "reviews": [],
            "availableFrom": "2025-05-14T00:00:00",
            "createdAt": "2025-05-12T05:43:01",
            "updatedAt": "2025-05-12T05:43:01",
            "isArchived": false,
            "isPublished": false
        }
    ],
    "pageable": {
        "pageNumber": 0,
        "pageSize": 1,
        "sort": { "empty": false, "sorted": true, "unsorted": false },
        "offset": 0,
        "paged": true,
        "unpaged": false
    },
    "last": false,
    "totalPages": 4,
    "totalElements": 4,
    "size": 1,
    "number": 0,
    "first": true,
    "numberOfElements": 1,
    "empty": false
}
```

### Réponse vide :

Si aucune colocation n'est trouvée sur la page demandée, la réponse sera :

```json
{
    "content": [],
    "pageable": {
        "pageNumber": 1,
        "pageSize": 1,
        "sort": { "empty": false, "sorted": true, "unsorted": false },
        "offset": 1,
        "paged": true,
        "unpaged": false
    },
    "last": true,
    "totalPages": 0,
    "totalElements": 0,
    "size": 1,
    "number": 1,
    "first": false,
    "numberOfElements": 0,
    "empty": true
}
```

---

## ✅ Exemples de requêtes

### Récupérer toutes les colocations (première page, 1 élément par page, terme de recherche "sss") :
```bash
GET http://localhost:8081/api/colocations?page=1&size=1&search=sss

```

---

## ❌ Gestion des erreurs

| Code HTTP | Description                              |
|----------|-------------------------------------------|
| `404`    | NOt found |

---

## 🧪 Notes importantes

- Les champs comme `hasParking`, `isFurnished`, `hasBalcony` peuvent être `true`, `false` ou `null`.
- Les dates sont au format ISO 8601.
- La pagination commence à **la page 0** côté serveur (`pageNumber`) mais peut être demandée à partir de la page 1 côté client (`page=1`).
- Si `empty` vaut `true`, cela signifie qu’il n’y a pas de données disponibles pour cette page.

---

# 📄 Documentation de l'API : Récupérer une colocation par son ID

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations/{{roomId}}`
- **Méthode** : `GET`
- **Authentification requise** : ❌ Non (Aucun token n'est nécessaire)
- **Code succès** : `200 OK`
- **Code erreur** : `404 Not Found` si aucune colocation avec cet ID n'existe

---

## 📥 Paramètres de requête

| Paramètre | Type   | Obligatoire | Description                     |
|----------|--------|-------------|---------------------------------|
| `roomId` | Number | ✅ Oui       | L’identifiant unique de la colocation dans l’URL |

> Exemple :
```bash
GET http://localhost:8081/api/colocations/2
```

---

## 📤 Format de la réponse (succès - 200 OK)

```json
{
    "message": "Colocation found successfully",
    "data": {
        "id": 2,
        "name": "Colocation El Manar",
        "idOfPublisher": "1",
        "nameOfPublisher": "Chedly",
        "address": "Rue des étudiants, Tunis",
        "city": "Tunis",
        "postalCode": "1002",
        "description": "Proche de la faculté",
        "price": 350.0,
        "numberOfRooms": 3,
        "roommatesGenderPreference": null,
        "hasWifi": null,
        "hasParking": null,
        "hasAirConditioning": null,
        "isFurnished": null,
        "hasBalcony": null,
        "hasPrivateBathroom": null,
        "maxRoommates": null,
        "currentRoommates": null,
        "status": null,
        "rules": [],
        "tags": [],
        "imageUrls": [],
        "averageRating": 0.0,
        "reviews": [],
        "availableFrom": null,
        "createdAt": "2025-05-12T02:54:43",
        "updatedAt": "2025-05-12T08:30:39",
        "isArchived": false,
        "isPublished": true
    }
}
```

---

## ❌ Réponse en cas d'erreur (404 Not Found)

```json
{
    "error": {
        "message": "Colocation with ID 265152 not found"
    }
}
```

---

## ✅ Exemple complet de requête

### Récupérer la colocation avec l'ID `2` :
```bash
GET http://localhost:8081/api/colocations/2
```

---

## 🧪 Notes importantes

- Aucun **token Bearer** n’est requis pour cette API.
- Les champs avec la valeur `null` indiquent qu'ils ne sont pas renseignés.
- Les dates (`createdAt`, `updatedAt`) sont au format **ISO 8601**.
- Si la colocation est introuvable, le serveur retourne une erreur `404`.

---
 

# 📄 Documentation de l'API : Rendre une Colocation visible( accepter /rejeter la publication)

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations/{{roomId}}/publish`
- **Méthode** : `PATCH`
- **Authentification requise** : ✅ Oui (Bearer Token)
- **Corps de la requête** : Objet JSON avec le champ `"isPublished": true`
- **Code succès** : `200 OK`
- **Code erreur** : `500 Internal Server Error` si la colocation n'existe pas

---

## 📥 Paramètres de requête

| Paramètre | Type   | Obligatoire | Description                     |
|----------|--------|-------------|---------------------------------|
| `roomId` | Number | ✅ Oui       | L’identifiant unique de la colocation dans l’URL |

> Exemple :
```bash
PATCH http://localhost:8081/api/colocations/2/publish
```

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l'en-tête de la requête.

### Exemple d’en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

---

## 📝 Corps de la requête

```json
{
    "isPublished": true
}
```

---

## 📤 Format de la réponse (succès - 200 OK)

```json
{
    "message": "Colocation publication status updated successfully",
    "data": {
        "id": 2,
        "name": "Colocation El Manar",
        "idOfPublisher": "1",
        "nameOfPublisher": "Chedly",
        "address": "Rue des étudiants, Tunis",
        "city": "Tunis",
        "postalCode": "1002",
        "description": "Proche de la faculté",
        "price": 350.0,
        "numberOfRooms": 3,
        "roommatesGenderPreference": null,
        "hasWifi": null,
        "hasParking": null,
        "hasAirConditioning": null,
        "isFurnished": null,
        "hasBalcony": null,
        "hasPrivateBathroom": null,
        "maxRoommates": null,
        "currentRoommates": null,
        "status": null,
        "rules": [],
        "tags": [],
        "imageUrls": [],
        "averageRating": 0.0,
        "reviews": [],
        "availableFrom": null,
        "createdAt": "2025-05-12T02:54:43",
        "updatedAt": "2025-05-12T08:30:39",
        "isArchived": false,
        "isPublished": true
    }
}
```

---

## ❌ Réponse en cas d'erreur (500 Internal Server Error)

```json
{
    "error": "Internal Server Error",
    "message": "An unexpected error occurred: Colocation with ID 298 not found",
    "status": 500
}
```

---

## ✅ Exemple complet de requête

### Publier la colocation avec l'ID `2` :
```bash
PATCH http://localhost:8081/api/colocations/2/publish
Authorization: Bearer <votre_token>
Content-Type: application/json

{
    "isPublished": true
}
```

---

## 🧪 Notes importantes

- Le champ `isPublished` est mis à jour côté serveur.
- Si la colocation avec l’ID spécifié n’existe pas, une erreur `500` est retournée (ce qui peut être amélioré côté backend avec un code `404 Not Found`).
- Les dates (`createdAt`, `updatedAt`) sont au format **ISO 8601**.
- Le token Bearer est obligatoire pour effectuer cette action.

---
 

# 📄 Documentation de l'API : Archiver une Colocation

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations/{{roomId}}/archive`
- **Méthode** : `PATCH`
- **Authentification requise** : ✅ Oui (Bearer Token)
- **Corps de la requête** : Objet JSON avec le champ `"isArchived": true | false`
- **Code succès** : `200 OK`
- **Codes erreurs** :
  - `401 Unauthorized` : si le token est manquant ou invalide
  - `500 Internal Server Error` : si la colocation n'existe pas

---

## 📥 Paramètres de requête

| Paramètre | Type   | Obligatoire | Description                     |
|----------|--------|-------------|---------------------------------|
| `roomId` | Number | ✅ Oui       | L’identifiant unique de la colocation dans l’URL |

> Exemple :
```bash
PATCH http://localhost:8081/api/colocations/2/archive
```

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l'en-tête de la requête.

### Exemple d’en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

---

## 📝 Corps de la requête

```json
{
    "isArchived": true
}
```

Vous pouvez aussi utiliser `false` pour désarchiver une colocation déjà archivée.

---

## 📤 Format de la réponse (succès - 200 OK)

```json
{
    "data": {
        "id": 2,
        "name": "Colocation El Manar",
        "idOfPublisher": "1",
        "nameOfPublisher": "Chedly",
        "address": "Rue des étudiants, Tunis",
        "city": "Tunis",
        "postalCode": "1002",
        "description": "Proche de la faculté",
        "price": 350.0,
        "numberOfRooms": 3,
        "roommatesGenderPreference": null,
        "hasWifi": null,
        "hasParking": null,
        "hasAirConditioning": null,
        "isFurnished": null,
        "hasBalcony": null,
        "hasPrivateBathroom": null,
        "maxRoommates": null,
        "currentRoommates": null,
        "status": null,
        "rules": [],
        "tags": [],
        "imageUrls": [],
        "averageRating": 0.0,
        "reviews": [],
        "availableFrom": null,
        "createdAt": "2025-05-12T02:54:43",
        "updatedAt": "2025-05-12T08:30:39",
        "isArchived": false,
        "isPublished": true
    },
    "message": "Colocation archive status updated successfully.",
    "status": 200
}
```

---

## ❌ Réponse en cas d'erreur (500 Internal Server Error)

```json
{
    "error": "Internal Server Error",
    "message": "An unexpected error occurred: Colocation with ID 298 not found",
    "status": 500
}
```

---

## ✅ Exemple complet de requête

### Archiver la colocation avec l'ID `2` :
```bash
PATCH http://localhost:8081/api/colocations/2/archive
Authorization: Bearer <votre_token>
Content-Type: application/json

{
    "isArchived": true
}
```

---

## 🧪 Notes importantes

- Le champ `isArchived` permet de basculer entre archivé (`true`) et non archivé (`false`).
- Si la colocation avec l’ID spécifié n’existe pas, une erreur `500` est retournée (ce qui peut être amélioré côté backend avec un code `404 Not Found`).
- Les dates (`createdAt`, `updatedAt`) sont au format **ISO 8601**.
- Le token Bearer est obligatoire pour effectuer cette action.

---
 

# 📄 Documentation de l'API : Supprimer une Colocation

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations/{{roomId}}`
- **Méthode** : `DELETE`
- **Authentification requise** : ✅ Oui (Bearer Token)
- **Code succès** : `200 OK`
- **Codes erreurs** :
  - `401 Unauthorized` : si le token est manquant ou invalide
  - `404 Not Found` : si la colocation avec cet ID n’existe pas

---

## 📥 Paramètres de requête

| Paramètre | Type   | Obligatoire | Description                     |
|----------|--------|-------------|---------------------------------|
| `roomId` | Number | ✅ Oui       | L’identifiant unique de la colocation dans l’URL |

> Exemple :
```bash
DELETE http://localhost:8081/api/colocations/2
```

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l'en-tête de la requête.

### Exemple d’en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

---

## 📤 Format de la réponse (succès - 200 OK)

```json
{
    "message": "Colocation with ID 2 has been deleted successfully.",
    "status": 200
}
```

---

## ❌ Réponse en cas d'erreur (404 Not Found)

```json
{
    "error": "Not Found",
    "message": "Colocation with ID 2212 not found.",
    "status": 404
}
```

---

## ✅ Exemple complet de requête

### Supprimer la colocation avec l'ID `2` :
```bash
DELETE http://localhost:8081/api/colocations/2
Authorization: Bearer <votre_token>
```

---

## 🧪 Notes importantes

- Une fois la colocation supprimée, elle ne sera plus disponible dans le système (sauf si sauvegardée ailleurs).
- Le token Bearer est obligatoire pour effectuer cette action.
- Si l’ID fourni n’existe pas, le serveur retourne une erreur `404 Not Found`.

---
 
# 📄 Documentation de l'API : Créer une Colocation

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations`
- **Méthode** : `POST`
- **Authentification requise** : ✅ Oui (Bearer Token)
- **Corps de la requête** : Objet JSON avec les détails de la colocation
- **Code succès** : `201 Created`
- **Codes erreurs** :
  - `401 Unauthorized` : si le token est manquant ou invalide
  - `500 Internal Server Error` : en cas d’erreur serveur inattendue

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l'en-tête de la requête.

### Exemple d’en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

---

## 📝 Corps de la requête (exigé)

Tous les champs marqués comme **obligatoires** doivent être présents dans le corps de la requête.

```json
{
    "name": "Colocation El Manar",
    "address": "Rue des étudiants, Tunis",
    "city": "Tunis",
    "postalCode": "1002",
    "description": "Proche de la faculté",
    "price": 350.0,
    "availableFrom": "2025-06-01",
    "numberOfRooms": 3,
    "roommatesGenderPreference": "MIXED",
    "hasWifi": true,
    "hasParking": true,
    "hasAirConditioning": false,
    "isFurnished": true,
    "hasBalcony": false,
    "hasPrivateBathroom": true,
    "maxRoommates": 4,
    "currentRoommates": 2,
    "status": "AVAILABLE",
    "rules": ["No smoking", "No pets"],
    "tags": ["faculté", "wifi", "proche centre"],
    "imageUrls": [
        "https://example.com/image1.jpg",
        "https://example.com/image2.jpg"
    ]
}
```

---

## ✅ Champs obligatoires (`nullable = false`)

| Champ                 | Type      | Description |
|----------------------|-----------|-------------|
| `name`               | String    | Nom de la colocation |
| `address`            | String    | Adresse exacte |
| `city`               | String    | Ville |
| `postalCode`         | String    | Code postal |
| `price`              | Double    | Prix mensuel |
| `numberOfRooms`      | Integer   | Nombre total de chambres |
| `availableFrom`      | LocalDate | Date à partir de laquelle la colocation est disponible |

> Les autres champs sont facultatifs et peuvent être omis.

---

## 📤 Format de la réponse (succès - 201 Created)

```json
{
    "message": "Colocation created successfully",
    "data": {
        "id": 5,
        "name": "Colocation El Manar",
        "idOfPublisher": "86c13de2-7fdb-4ee6-a547-e9266ad19b0a",
        "nameOfPublisher": "admin2",
        "address": "Rue des étudiants, Tunis",
        "city": "Tunis",
        "postalCode": "1002",
        "description": "Proche de la faculté",
        "price": 350.0,
        "numberOfRooms": 3,
        "roommatesGenderPreference": "MIXED",
        "hasWifi": true,
        "hasParking": true,
        "hasAirConditioning": false,
        "isFurnished": true,
        "hasBalcony": false,
        "hasPrivateBathroom": true,
        "maxRoommates": 4,
        "currentRoommates": 2,
        "status": "AVAILABLE",
        "rules": ["No smoking", "No pets"],
        "tags": ["faculté", "wifi", "proche centre"],
        "imageUrls": ["https://example.com/image1.jpg", "https://example.com/image2.jpg"],
        "averageRating": null,
        "reviews": [],
        "availableFrom": "2025-06-01",
        "createdAt": "2025-05-14",
        "updatedAt": "2025-05-14",
        "isArchived": false,
        "isPublished": false
    }
}
```

---

## ❌ Réponse en cas d'erreur (500 Internal Server Error)

```json
{
    "error": "Internal Server Error",
    "message": "An unexpected error occurred",
    "status": 500
}
```

---

## ✅ Exemple complet de requête

### Créer une nouvelle colocation :
```bash
POST http://localhost:8081/api/colocations
Authorization: Bearer <votre_token>
Content-Type: application/json

{
    "name": "Colocation El Manar",
    "address": "Rue des étudiants, Tunis",
    "city": "Tunis",
    "postalCode": "1002",
    "description": "Proche de la faculté",
    "price": 350.0,
    "availableFrom": "2025-06-01",
    "numberOfRooms": 3,
    "roommatesGenderPreference": "MIXED",
    "hasWifi": true,
    "hasParking": true,
    "hasAirConditioning": false,
    "isFurnished": true,
    "hasBalcony": false,
    "hasPrivateBathroom": true,
    "maxRoommates": 4,
    "currentRoommates": 2,
    "status": "AVAILABLE",
    "rules": ["No smoking", "No pets"],
    "tags": ["faculté", "wifi", "proche centre"],
    "imageUrls": [
        "https://example.com/image1.jpg",
        "https://example.com/image2.jpg"
    ]
}
```

---

## 🧪 Notes importantes

- Le champ `availableFrom` doit être au format **`YYYY-MM-DD`**.
- Les dates `createdAt` et `updatedAt` sont automatiquement gérées par le système.
- Les images sont stockées sous forme de liste d’URLs.
- Le champ `averageRating` est calculé dynamiquement à partir des avis associés.
- Le token Bearer est obligatoire pour effectuer cette action.

---


# 📄 Documentation de l'API : Mettre à jour une Colocation

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations`
- **Méthode** : `PUT`
- **Authentification requise** : ✅ Oui (Bearer Token)
- **Corps de la requête** : Objet JSON avec les nouvelles données
- **Code succès** : `200 OK`
- **Codes erreurs** :
  - `401 Unauthorized` : si le token est manquant ou invalide

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l'en-tête de la requête.

### Exemple d’en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

---

## 📝 Corps de la requête

Le corps doit contenir toutes les informations nécessaires pour mettre à jour la colocation.

```json
{
    "name": "test",
    "address": "Rue des étudiants, Tunis",
    "city": "Tunis",
    "postalCode": "1002",
    "description": "Proche de la faculté",
    "price": 350.0,
    "availableFrom": "2025-06-01",
    "numberOfRooms": 3,
    "roommatesGenderPreference": "MIXED",
    "hasWifi": true,
    "hasParking": true,
    "hasAirConditioning": false,
    "isFurnished": true,
    "hasBalcony": false,
    "hasPrivateBathroom": true,
    "maxRoommates": 4,
    "currentRoommates": 2,
    "status": "AVAILABLE",
    "rules": ["No smoking", "No pets"],
    "tags": ["faculté", "wifi", "proche centre"]
}
```

> **Note** : Le champ `imageUrls` n’est pas inclus ici car il est optionnel lors de la mise à jour.

---

## ✅ Champs obligatoires

| Champ                 | Type      | Description |
|----------------------|-----------|-------------|
| `name`               | String    | Nom de la colocation |
| `address`            | String    | Adresse exacte |
| `city`               | String    | Ville |
| `postalCode`         | String    | Code postal |
| `price`              | Double    | Prix mensuel |
| `numberOfRooms`      | Integer   | Nombre total de chambres |
| `availableFrom`      | LocalDate | Date à partir de laquelle la colocation est disponible |

> Les autres champs sont facultatifs et peuvent être omis.

---

## 📤 Format de la réponse (succès - 200 OK)

```json
{
    "message": "Colocation created successfully",
    "data": {
        "id": 7,
        "name": "test",
        "idOfPublisher": "86c13de2-7fdb-4ee6-a547-e9266ad19b0a",
        "nameOfPublisher": "admin2",
        "address": "Rue des étudiants, Tunis",
        "city": "Tunis",
        "postalCode": "1002",
        "description": "Proche de la faculté",
        "price": 350.0,
        "numberOfRooms": 3,
        "roommatesGenderPreference": "MIXED",
        "hasWifi": true,
        "hasParking": true,
        "hasAirConditioning": false,
        "isFurnished": true,
        "hasBalcony": false,
        "hasPrivateBathroom": true,
        "maxRoommates": 4,
        "currentRoommates": 2,
        "status": "AVAILABLE",
        "rules": ["No smoking", "No pets"],
        "tags": ["faculté", "wifi", "proche centre"],
        "imageUrls": [],
        "averageRating": null,
        "reviews": [],
        "availableFrom": "2025-06-01",
        "createdAt": "2025-05-14",
        "updatedAt": "2025-05-14",
        "isArchived": false,
        "isPublished": false
    }
}
```

---

## ✅ Exemple complet de requête

### Mettre à jour une colocation :
```bash
PUT http://localhost:8081/api/colocations
Authorization: Bearer <votre_token>
Content-Type: application/json

{
    "name": "test",
    "address": "Rue des étudiants, Tunis",
    "city": "Tunis",
    "postalCode": "1002",
    "description": "Proche de la faculté",
    "price": 350.0,
    "availableFrom": "2025-06-01",
    "numberOfRooms": 3,
    "roommatesGenderPreference": "MIXED",
    "hasWifi": true,
    "hasParking": true,
    "hasAirConditioning": false,
    "isFurnished": true,
    "hasBalcony": false,
    "hasPrivateBathroom": true,
    "maxRoommates": 4,
    "currentRoommates": 2,
    "status": "AVAILABLE",
    "rules": ["No smoking", "No pets"],
    "tags": ["faculté", "wifi", "proche centre"]
}
```

---

## 🧪 Notes importantes

- Les dates (`availableFrom`, `createdAt`, `updatedAt`) doivent être au format **`YYYY-MM-DD`**.
- Les champs comme `hasWifi`, `isFurnished`, etc., doivent être des booléens (`true` ou `false`).

- Le token Bearer est obligatoire pour effectuer cette action.

---

# 📄 Documentation de l'API : Récupérer les colocations non publiées

## 🔍 Vue d'ensemble

- **URL de base** : `http://localhost:8081/api/colocations/non-published`
- **Méthode** : `GET`
- **Authentification requise** : ✅ Oui (Bearer Token)
- **Code succès** : `200 OK`
- **Code erreur** :
  - `401 Unauthorized` : si le token est manquant ou invalide
  - `403 Forbidden` : si l’utilisateur n’a pas les droits nécessaires

---

## 📥 Paramètres de requête (optionnels)

| Paramètre | Description |
|----------|-------------|
| `page`   | Numéro de la page à récupérer (commence à 1) |
| `size`   | Nombre d’éléments par page |
| `search` | Terme de recherche optionnel (par exemple : ville, adresse, etc.) |

> Exemple :
```bash
GET /api/colocations/non-published?page=1&size=1&search=sss
```

---

## 🔐 Authentification

Cette API nécessite un **token Bearer** valide dans l'en-tête de la requête.

### Exemple d’en-tête :
```http
Authorization: Bearer <votre_token>
```

En cas d'absence ou d'invalidité du token, l'API renverra :
```http
HTTP/1.1 401 Unauthorized
```

Si l'utilisateur connecté n'a pas les permissions nécessaires :
```http
HTTP/1.1 403 Forbidden
```

---

## 📤 Format de la réponse (succès - 200 OK)

La réponse est un objet JSON contenant une liste paginée de colocations non publiées.

### Exemple de réponse :

```json
{
    "content": [
        {
            "id": 1,
            "name": "Colocation El Manar",
            "idOfPublisher": "1",
            "nameOfPublisher": "Chedly",
            "address": "Rue des étudiants, Tunis",
            "city": "Tunis",
            "postalCode": "1002",
            "description": "Proche de la faculté",
            "price": 350.0,
            "numberOfRooms": 3,
            "roommatesGenderPreference": null,
            "hasWifi": null,
            "hasParking": null,
            "hasAirConditioning": null,
            "isFurnished": null,
            "hasBalcony": null,
            "hasPrivateBathroom": null,
            "maxRoommates": null,
            "currentRoommates": null,
            "status": null,
            "rules": [],
            "tags": [],
            "imageUrls": [],
            "averageRating": 0.0,
            "reviews": [],
            "availableFrom": null,
            "createdAt": "2025-05-12",
            "updatedAt": "2025-05-12",
            "isArchived": false,
            "isPublished": false
        }
    ],
    "pageable": {
        "pageNumber": 0,
        "pageSize": 10,
        "sort": { "empty": true, "sorted": false, "unsorted": true },
        "offset": 0,
        "paged": true,
        "unpaged": false
    },
    "last": true,
    "totalPages": 1,
    "totalElements": 5,
    "first": true,
    "numberOfElements": 5,
    "size": 10,
    "number": 0,
    "sort": { "empty": true, "sorted": false, "unsorted": true },
    "empty": false
}
```

---

## 📌 Réponse vide (aucune colocation trouvée)

```json
{
    "content": [],
    "pageable": {
        "pageNumber": 1,
        "pageSize": 1,
        "sort": { "empty": true, "sorted": false, "unsorted": true },
        "offset": 1,
        "paged": true,
        "unpaged": false
    },
    "last": true,
    "totalPages": 0,
    "totalElements": 0,
    "first": false,
    "numberOfElements": 0,
    "size": 1,
    "number": 1,
    "sort": { "empty": true, "sorted": false, "unsorted": true },
    "empty": true
}
```

---

## ✅ Exemple complet de requête

### Récupérer les colocations non publiées avec filtre :
```bash
GET http://localhost:8081/api/colocations/non-published?page=1&size=1&search=sss
Authorization: Bearer <votre_token>
```

---

## 🧪 Notes importantes

- Les champs comme `hasWifi`, `isFurnished`, etc., peuvent être `true`, `false` ou `null`.
- Les dates (`createdAt`, `updatedAt`, `availableFrom`) sont au format **`YYYY-MM-DD`**.
- La pagination commence à la page 0 côté serveur (`pageNumber`) mais peut être demandée à partir de la page 1 côté client (`page=1`).
- Si `empty` vaut `true`, cela signifie qu’il n’y a pas de données disponibles pour cette page.
- Le token Bearer est obligatoire pour effectuer cette action.

---
