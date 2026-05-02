# UnitSwitch — Application Android de Conversion d'Unités

> Application Android native développée avec Java, ViewPager2 et Material Design 3.  
> Permet de convertir des unités de **température**, **distance** et **masse** via une interface à onglets.

---

## Aperçu

<!-- Pour intégrer une démo vidéo, voir la section "Intégration vidéo" en bas de ce fichier -->

![Architecture](https://img.shields.io/badge/Architecture-Fragment--based-blue)
![SDK](https://img.shields.io/badge/Min%20SDK-24-green)
![Language](https://img.shields.io/badge/Language-Java-orange)
![UI](https://img.shields.io/badge/UI-Material%20Design%203-purple)

---

## Fonctionnalités

| Onglet | Conversion | Exemple |
|--------|-----------|---------|
| 🌡 Température | Celsius ↔ Fahrenheit | 25 °C → 77.00 °F |
| 📍 Distance | Kilomètres ↔ Miles | 10 km → 6.214 mi |
| ⚖️ Masse | Kilogrammes ↔ Livres | 70 kg → 154.323 lb |

**Comportements supplémentaires :**
- Validation des champs : message Toast si la saisie est vide
- Bouton Retour : boîte de dialogue de confirmation avant fermeture
- Résultat affiché avec l'unité (ex. `6.214 mi`)

---

## Structure du projet

```
app/
├── src/
│   └── main/
│       ├── java/com/example/unitswitch/
│       │   ├── MainActivity.java          # Activité principale + gestion onglets
│       │   ├── TabSectionAdapter.java     # Adaptateur ViewPager2 (3 fragments)
│       │   ├── TempFragment.java          # Fragment Température
│       │   ├── DistanceFragment.java      # Fragment Distance
│       │   └── MassFragment.java          # Fragment Masse
│       └── res/
│           └── layout/
│               ├── activity_main.xml      # Layout principal (CoordinatorLayout)
│               ├── fragment_temp.xml      # Layout onglet Température
│               ├── fragment_distance.xml  # Layout onglet Distance
│               └── fragment_mass.xml      # Layout onglet Masse
└── build.gradle
```

---

## Architecture

```
MainActivity
    └── TabSectionAdapter (FragmentStateAdapter)
            ├── position 0 → TempFragment
            ├── position 1 → DistanceFragment
            └── position 2 → MassFragment
```

Chaque `Fragment` est **autonome** : il gère son propre layout, sa validation et sa logique de conversion. La communication entre onglets n'est pas nécessaire pour cette application.

---

## Dépendances (`build.gradle`)

```groovy
dependencies {
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.11.0'
    implementation 'androidx.viewpager2:viewpager2:1.0.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
}
```

---

## Installation & Lancement

1. Cloner ou télécharger le projet
2. Ouvrir dans **Android Studio** (version Hedgehog ou plus récente recommandée)
3. Synchroniser Gradle (`File > Sync Project with Gradle Files`)
4. Lancer sur un émulateur (API 24+) ou un appareil physique

```bash
# Via Android Studio : Run > Run 'app'
# Ou via ligne de commande :
./gradlew assembleDebug
adb install app/build/outputs/apk/debug/app-debug.apk
```

---

## Formules utilisées

### Température
```
Celsius → Fahrenheit : F = (C × 1.8) + 32
Fahrenheit → Celsius : C = (F − 32) / 1.8
```

### Distance
```
Kilomètres → Miles : mi = km / 1.60934
Miles → Kilomètres : km = mi × 1.60934
```

### Masse
```
Kilogrammes → Livres : lb = kg × 2.20462
Livres → Kilogrammes : kg = lb / 2.20462
```

---

## Choix techniques

| Choix | Justification |
|-------|---------------|
| `CoordinatorLayout` + `AppBarLayout` | Respecte les guidelines Material Design 3 |
| `OnBackPressedCallback` | Remplace `onBackPressed()` déprécié depuis API 33 |
| `TextInputLayout` Material | Meilleure UX : label flottant, gestion d'erreur intégrée |
| `newInstance()` sur chaque Fragment | Bonne pratique Android pour l'instanciation des fragments |
| Constantes nommées (`KM_PER_MILE`, `LB_PER_KG`) | Lisibilité et maintenabilité du code |
| Formules dans des méthodes privées | Séparation des responsabilités, facilite les tests unitaires |

---

## Tests manuels

| Scénario | Entrée | Résultat attendu |
|----------|--------|-----------------|
| C → F | 25 | 77.00 °F |
| F → C | 77 | 25.00 °C |
| km → mi | 10 | 6.214 mi |
| mi → km | 6.214 | 10.000 km |
| kg → lb | 70 | 154.323 lb |
| lb → kg | 154.323 | 70.000 kg |
| Champ vide | _(vide)_ | Toast "Saisir une valeur d'abord" |
| Bouton Retour | — | Dialog de confirmation |

---

## Auteur

Projet réalisé dans le cadre du cours de **Développement Mobile Android** — Java.

---
aourik anas
---

