# PCG 2005 Madagascar

Application d'apprentissage du **Plan Comptable Général 2005** de Madagascar et de son **guide annoté**, pour les étudiants et les professionnels.

- Plan Comptable Général 2005 : approuvé par le **décret n° 2004-272 du 18 février 2004**
- Guide annoté du PCG 2005 : **arrêté n° 3169 du 14 avril 2005**
- Élaborés par le Conseil Supérieur de la Comptabilité (CSC), l'OECFM et l'INSTAT

> Outil pédagogique : il ne remplace pas les textes officiels, qui seuls font foi.

## Contenu de l'application

- Fiches essentielles : conventions, qualités de l'information, principes comptables, définitions
- Plan de comptes complet avec le fonctionnement officiel de chaque compte
- 70 écritures types, dont TVA, crédit-bail, stocks, titres, impôts
- Simulateur comptable : journal, grand livre, balance, bilan, compte de résultat
- Modèles officiels des 5 états financiers et tableau de passage
- Calculateurs : amortissements, perte de valeur, cession, TVA
- 160 questions, exercices de saisie d'écritures et de calcul, examen blanc
- Textes intégraux du PCG 2005 et du guide annoté, glossaire, recherche
- Paramètres : thème, couleurs, polices, tailles, présentation

Tout tient dans un seul fichier `index.html`, sans serveur ni base de données. La progression de chaque utilisateur est enregistrée dans son navigateur.

## Organisation du dépôt

```
index.html               l'application complète
manifest.webmanifest     installation sur l'écran d'accueil (PWA)
sw.js                    fonctionnement hors ligne
icons/                   icônes de l'application
android/                 projet Android (WebView) qui embarque index.html
.github/workflows/       construction automatique de l'APK Android
```

---

## 1. Mettre l'application sur GitHub

1. Créez un compte sur [github.com](https://github.com) si vous n'en avez pas.
2. Cliquez sur **New repository**, nommez-le `pcg-2005-madagascar`, choisissez **Public**, puis **Create repository**.
3. Envoyez les fichiers, au choix :
   - **Avec GitHub Desktop** (le plus simple pour tout envoyer, y compris le dossier caché `.github`) : *File → Add local repository*, choisissez ce dossier, puis *Commit to main* et *Push origin*.
   - **Avec le navigateur** : *Add file → Upload files*, glissez tout le contenu du dossier, puis *Commit changes*. Le dossier `.github` est masqué sur certains ordinateurs : si le workflow n'apparaît pas, créez-le avec *Add file → Create new file*, nommez le fichier `.github/workflows/android.yml` et collez son contenu.
   - **En ligne de commande** :
     ```bash
     git init
     git add .
     git commit -m "PCG 2005 Madagascar"
     git branch -M main
     git remote add origin https://github.com/VOTRE-NOM/pcg-2005-madagascar.git
     git push -u origin main
     ```

## 2. Publier le site avec GitHub Pages

1. Dans le dépôt : **Settings → Pages**.
2. *Source* : **Deploy from a branch** ; *Branch* : **main**, dossier **/ (root)** ; **Save**.
3. Après une à deux minutes, l'application est en ligne à l'adresse :
   `https://VOTRE-NOM.github.io/pcg-2005-madagascar/`

Sur un téléphone, ouvrez cette adresse puis :
- **Android (Chrome)** : menu ⋮ → *Installer l'application* ou *Ajouter à l'écran d'accueil*
- **iPhone (Safari)** : Partager → *Sur l'écran d'accueil*

L'application fonctionne ensuite hors ligne.

## 3. Obtenir l'application Android (APK)

Le workflow `.github/workflows/android.yml` construit l'APK automatiquement à chaque envoi sur `main`.

1. Ouvrez l'onglet **Actions** du dépôt.
2. Cliquez sur la dernière exécution de **Construire l'application Android** (ou lancez-la avec *Run workflow*).
3. Quand elle est terminée (coche verte), téléchargez **PCG-2005-Madagascar-apk** en bas de la page. Décompressez le fichier zip obtenu.
4. Copiez `PCG-2005-Madagascar.apk` sur le téléphone, ouvrez-le et autorisez l'installation depuis cette source.

Pour publier une version téléchargeable par tous, créez un tag :
```bash
git tag v1.0
git push origin v1.0
```
L'APK est alors joint automatiquement à une *Release* (onglet **Releases**).

Pour mettre à jour l'application Android, modifiez `index.html` et envoyez-le : l'APK suivant l'intègre automatiquement. Pensez à augmenter `versionCode` et `versionName` dans `android/app/build.gradle`.

## 4. Publier sur Google Play (facultatif)

L'APK produit par le workflow est une version de test (signée en mode debug) : il s'installe directement, mais Google Play exige un paquet **AAB signé avec votre propre clé**. Deux possibilités :

- **PWABuilder** ([pwabuilder.com](https://www.pwabuilder.com)) : saisissez l'adresse GitHub Pages de l'application, choisissez *Android*, et téléchargez un paquet prêt pour le Play Store, avec sa clé de signature. Conservez précieusement cette clé.
- **Android Studio** : ouvrez le dossier `android/`, puis *Build → Generate Signed App Bundle / APK*.

Il faut ensuite un compte développeur Google Play Console pour mettre l'application en ligne.

## 5. Ouvrir le projet Android en local (facultatif)

1. Installez [Android Studio](https://developer.android.com/studio).
2. *Open* → choisissez le dossier `android/`.
3. Lancez l'application sur un téléphone ou un émulateur avec ▶.

La tâche Gradle `copyWebAssets` copie `index.html`, le manifeste et les icônes dans l'APK à chaque construction.
