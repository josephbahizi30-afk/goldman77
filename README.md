# 🎯 Système de Réservation - Documentation

Un système complet de gestion des réservations en JavaScript avec interface web et support Node.js.

## 📋 Fonctionnalités

### 1️⃣ **Créer une Réservation**
- Réserver une salle pour une période spécifique
- Vérification automatique de la disponibilité
- Vérification de la capacité de la salle
- Attribution automatique d'un ID unique

```javascript
const systeme = new SystemeReservation();
const reservation = systeme.creerReservation(
  'Jean Dupont',      // Nom du client
  1,                  // ID de la ressource
  '2026-04-01',       // Date de début
  '2026-04-03',       // Date de fin
  10                  // Nombre de personnes
);
```

### 2️⃣ **Vérifier la Disponibilité**
- Consulter les créneaux libres
- Identifier les périodes occupées
- Validez vos nouvelles réservations avant de les créer

```javascript
const disponible = systeme.verifierDisponibilite(
  1,                // ID de la ressource
  '2026-04-05',     // Date de début
  '2026-04-07'      // Date de fin
);

if (disponible) {
  console.log('✓ Cette période est disponible');
} else {
  console.log('✗ Cette période n\'est pas disponible');
}

// Afficher les créneaux
systeme.afficherCreneauxDisponibles(1, '2026-04-01', '2026-04-15');
```

### 3️⃣ **Annuler une Réservation**
- Annuler une réservation existante
- Vérification que la réservation ne s'est pas encore commencée
- Historique des annulations

```javascript
try {
  systeme.annulerReservation(1); // ID de la réservation
  console.log('✓ Réservation annulée');
} catch (erreur) {
  console.error('❌ ' + erreur.message);
}
```

### 4️⃣ **Afficher la Liste**
- Consulter toutes les réservations
- Filtrer par statut (confirmées, annulées)
- Tri automatique par date

```javascript
// Afficher tous les réservations
systeme.afficherListe('toutes');

// Afficher uniquement les confirmées
systeme.afficherListe('confirmées');

// Afficher uniquement les annulées
systeme.afficherListe('annulées');
```

## 📁 Fichiers du Projet

### 1. `reservation.js`
Classe principale `SystemeReservation` pour Node.js.
- Tous les algorithmes de gestion
- Gestion des réservations complète
- Validation et vérification de disponibilité

### 2. `exemples.js`
Exemples d'utilisation et cas de test pour Node.js.
```bash
node exemples.js
```

### 3. `index.html`
Interface web interactive avec style moderne.
- Formulaire de création
- Vérification de disponibilité
- Affichage des réservations
- Statistiques en temps réel

### 4. `reservation-browser.js`
Implémentation JavaScript pour le navigateur.
- Utilise LocalStorage pour la persistance
- Interface réactive dynamique
- Gestion des événements

## 🚀 Utilisation

### Option 1: Interface Web
1. Ouvrez `index.html` dans votre navigateur
2. Remplissez le formulaire pour créer une réservation
3. Vérifiez la disponibilité des salles
4. Consultez et gérez vos réservations
5. Les données sont sauvegardées dans le navigateur (LocalStorage)

### Option 2: Node.js
```bash
# Exécuter les exemples
node exemples.js

# Ou créer votre propre script
```

```javascript
const SystemeReservation = require('./reservation.js');
const systeme = new SystemeReservation();

// Votre code ici...
systeme.creerReservation('Client', 1, '2026-04-01', '2026-04-03', 10);
systeme.afficherListe('confirmées');
```

## 📊 Ressources Disponibles

Le système gère 3 salles par défaut:

| Salle | Capacité | ID |
|-------|----------|-----|
| Salle A | 20 personnes | 1 |
| Salle B | 30 personnes | 2 |
| Salle C | 15 personnes | 3 |

## ⚠️ Gestion des Erreurs

Le système valide automatiquement:

✓ **Date de fin** > Date de début  
✓ **Nombre de personnes** ≤ Capacité de la salle  
✓ **Pas de chevauchement** entre réservations  
✓ **Ressource existe** dans la base de données  
✓ **Annulation avant le début** de la réservation uniquement  

### Exemples d'erreurs

```javascript
// ❌ Date fin avant date début
systeme.creerReservation('Test', 1, '2026-04-10', '2026-04-05', 5);
// Erreur: "La date de fin doit être après la date de début"

// ❌ Capacité dépassée
systeme.creerReservation('Test', 3, '2026-04-15', '2026-04-17', 50);
// Erreur: "Nombre de personnes (50) dépasse la capacité (15)"

// ❌ Chevauchement de réservation
systeme.creerReservation('Test', 1, '2026-04-02', '2026-04-04', 10);
// Erreur: "La ressource n'est pas disponible pour cette période"
```

## 💾 Persistance des Données

### Web (index.html)
Les données sont sauvegardées dans **LocalStorage** du navigateur:
- Automatiquement sauvegardées après chaque action
- Persistent entre les sessions du navigateur
- Effacer le cache pour réinitialiser les données

### Node.js
Les données sont stockées en mémoire:
- À chaque démarrage du script, la base recommence vide
- Pour la persistance, utilisez un fichier JSON

## 📈 Fonctions Supplémentaires

```javascript
// Obtenir une réservation spécifique
const res = systeme.obtenirReservation(1);

// Obtenir les statistiques
const stats = systeme.obtenirStatistiques();
console.log(stats); // { total: 5, confirmees: 4, annulees: 1 }

// Afficher les ressources
systeme.afficherRessources();
```

## 🎨 Interface Web - Fonctionnalités

- **Onglets de filtrage**: Toutes / Confirmées / Annulées
- **Statistiques en direct**: Total, Confirmées, Annulées
- **Validation côté client**: Avant soumission au système
- **Alertes visuelles**: Succès (vert), Erreur (rouge), Info (bleu)
- **Responsive Design**: Adapté pour mobile et desktop
- **Gradient moderne**: Interface avec couleur purpre/violet

## 🔧 Personnalisation

### Ajouter une nouvelle salle
```javascript
systeme.ressources.push({
  id: 4,
  nom: 'Salle D',
  capacite: 50
});
```

### Modifier la capacité
```javascript
systeme.ressources[0].capacite = 25; // Salle A
```

## 📝 Exemples Complets

### Créer 3 réservations
```javascript
systeme.creerReservation('Alice', 1, '2026-04-01', '2026-04-03', 15);
systeme.creerReservation('Bob', 2, '2026-04-02', '2026-04-05', 20);
systeme.creerReservation('Charlie', 3, '2026-04-08', '2026-04-10', 12);
```

### Vérifier et annuler
```javascript
const dispo = systeme.verifierDisponibilite(1, '2026-04-05', '2026-04-07');
if (dispo) {
  systeme.creerReservation('David', 1, '2026-04-05', '2026-04-07', 10);
}

// Annuler après
systeme.annulerReservation(1);
```

### Afficher statistiques
```javascript
systeme.afficherListe('confirmées');
const stats = systeme.obtenirStatistiques();
console.log(`Total: ${stats.total}, Confirmées: ${stats.confirmees}`);
```

## 🐛 Dépannage

### Les données disparaissent après rafraîchissement (Web)
- Vérifiez que LocalStorage n'est pas désactivé
- Essayez en mode normal (pas mode incognito)

### Node.js ne trouve pas le module
- Vérifiez que `reservation.js` est dans le même répertoire
- Utilisez le chemin correct : `require('./reservation.js')`

## 📄 Licence

Système de réservation - Usage libre

---

**Créé en**: Mars 2026  
**Dernière mise à jour**: Mars 2026
#
