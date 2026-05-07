# 📱 Lab 23 — JNIDemo (Android + JNI + C++)

---

## 📌 Présentation

Dans ce laboratoire, l’objectif est de construire une application Android nommée **JNIDemo** capable de communiquer avec du code natif **C++** via **JNI**.

L’application permet :

* d’appeler des fonctions natives ;
* d’envoyer des paramètres depuis Java vers C++ ;
* de récupérer des résultats du code natif ;
* de charger correctement une bibliothèque `.so`.

JNI est utilisé dans plusieurs cas :

* calcul intensif ;
* réutilisation de bibliothèques C/C++ ;
* sécurité et anti reverse engineering ;
* traitement temps réel.

⚠️ Bonne pratique : limiter les allers-retours entre Java et C++.

---

## 🎯 Objectifs pédagogiques

À la fin de ce lab, vous serez capable de :

* créer un projet Android avec C++ ;
* comprendre JNI, NDK et CMake ;
* appeler des méthodes natives ;
* échanger des données Java ↔ C++ ;
* gérer les erreurs JNI ;
* lire les logs natifs ;
* appliquer les bonnes pratiques.

---

## ⚙️ Fonctionnalités de l’application

L’application réalise :

1. Appel d’une fonction native simple
2. Calcul d’un factoriel en C++
3. Inversion d’une chaîne
4. Traitement d’un tableau `int[]`

---

## 🧰 Prérequis

* Android Studio
* SDK Android
* NDK
* CMake
* LLDB
* Bases en Java et Android

---

## 🏗️ Architecture

```
Java (MainActivity)
        ↓
System.loadLibrary("native-lib")
        ↓
JNI
        ↓
C++ (native-lib.cpp)
        ↓
Résultat → Java → UI
```

---

## 🚀 Étape 1 — Création du projet

Configuration :

* Name : `JNIDemo`
* Language : Java
* Min SDK : 24
* Include C++ support : ✔️
* Build system : CMake

### 📁 Structure générée

```
app/
 └── src/
     └── main/
         ├── cpp/
         │    ├── native-lib.cpp
         │    └── CMakeLists.txt
         └── java/
```

---

## 🔍 Étape 2 — Comprendre les composants

### JNI

Interface entre Java et C++.

### NDK

Permet d’exécuter du code natif.

### CMake

Outil de compilation du code C++.

### .so

Bibliothèque native Android.

---

## ⚙️ Étape 3 — Configuration Gradle

```gradle
android {
    namespace "com.example.jnidemo"
    compileSdk 35

    defaultConfig {
        applicationId "com.example.jnidemo"
        minSdk 24
        targetSdk 35
        versionCode 1
        versionName "1.0"
    }

    externalNativeBuild {
        cmake {
            path file("src/main/cpp/CMakeLists.txt")
        }
    }
}
```

📌 Important : le chemin CMake doit être correct.

---

## 🧩 Étape 4 — CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.22.1)

project("jnidemo")

add_library(
        native-lib
        SHARED
        native-lib.cpp)

find_library(
        log-lib
        log)

target_link_libraries(
        native-lib
        ${log-lib})
```

### 📖 Explication

* `add_library` : crée la bibliothèque `.so`
* `find_library` : récupère la lib Android `log`
* `target_link_libraries` : fait le lien

---

## ⚠️ Point critique

Le nom doit correspondre :

```java
System.loadLibrary("native-lib");
```

---

## ✅ Conclusion

Ce lab permet de comprendre :

* la communication Java ↔ C++ ;
* la compilation native ;
* l’utilisation de JNI dans Android moderne.

JNI est puissant mais doit être utilisé avec précaution pour garder de bonnes performances.

---

## 📌 Suite

👉 Envoie-moi les prochains screenshots pour compléter :

* MainActivity
* native-lib.cpp
* Fonctions JNI
* Gestion des types

Je vais ajouter les étapes avec **code complet à la place des images**.
