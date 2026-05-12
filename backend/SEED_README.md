# 🌱 Guide d'utilisation du Seed

Ce script permet de créer rapidement des utilisateurs de test dans votre base de données pour tester l'application.

## 🚀 Utilisation

### Option 1 : Utiliser le script de seed (Recommandé)

1. **Assurez-vous que votre base de données est configurée** dans le fichier `.env`

2. **Exécutez le script de seed** :
   ```bash
   npm run seed
   ```

   Ou directement :
   ```bash
   node seed.js
   ```

3. **Les comptes suivants seront créés** :

   - **👨‍💼 Administrateur**
     - Email: `admin@hestim.ma`
     - Mot de passe: `password123`

   - **👨‍🏫 Enseignant de démonstration**
     - Email: `alain.bennis0@hestim.ma`
     - Mot de passe: `password123`

   - **👨‍🎓 Étudiant de démonstration**
     - Email: `hamza.benali0@hestim.ma`
     - Mot de passe: `password123`

4. **Connectez-vous** avec l'un de ces comptes sur la page de connexion !

### Option 2 : Utiliser la route d'inscription

Vous pouvez également créer un compte via l'API d'inscription :

**Endpoint** : `POST /api/auth/register`

**Body** :
```json
{
  "nom": "Votre Nom",
  "prenom": "Votre Prénom",
  "email": "votre.email@hestim.ma",
  "password": "VotreMotDePasse123!",
  "role": "etudiant" // ou "enseignant" ou "admin"
}
```

**Exemple avec curl** :
```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "nom": "Test",
    "prenom": "User",
    "email": "test@hestim.ma",
    "password": "Test123!@#",
    "role": "etudiant"
  }'
```

## 📋 Données créées par le seed

Le script crée également :
- ✅ 5 filières, 27 groupes et 60 cours
- ✅ 35 salles réparties sur les bâtiments Gandhi et Stendhal
- ✅ 30 créneaux horaires sur 6 jours
- ✅ 90 enseignants et 701 étudiants
- ✅ 60 affectations de planning sur la période de démonstration
- ✅ 1 session de génération automatique et 1 snapshot actif
- ✅ Des disponibilités/indisponibilités enseignants
- ✅ 3 demandes de report (`en_attente`, `approuve`, `refuse`)
- ✅ 2 conflits volontaires pour démontrer l'arbitrage
- ✅ Des notifications pour les rôles admin, enseignant et étudiant

## ⚠️ Notes importantes

- Le script utilise `findOrCreate`, donc il ne créera pas de doublons si vous l'exécutez plusieurs fois
- Le mot de passe par défaut est `password123` pour tous les comptes de test
- Pour la production, changez ces mots de passe !

## 🔄 Réinitialiser les données

Si vous voulez réinitialiser complètement la base de données :

1. Supprimez toutes les tables dans votre base de données MySQL
2. Redémarrez le serveur (les tables seront recréées)
3. Exécutez `npm run seed` pour créer les données de test
