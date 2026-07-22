Voici une version retravaillée du `README.md`, adoptant une tonalité sobre, technique et directement orientée pour des équipes de développement web et SIG.

---

# Géoportail Campus TPG - Eau'bservatoire

Ce dépôt contient l'interface web dédiée au visionnage des cartes interactives du réseau d'eau du Campus TPG pour le projet **Eau'bservatoire**.

## Vue d'ensemble et Architecture

L'application est une page web autonome (*standalone*) conçue sans dépendances externes lourdes. Elle sert de passerelle d'affichage entre la plateforme cartographique **ArcGIS Online** et le CMS **WordPress**.

### Flux de données et intégration

```
[ArcGIS Online / WebMap]
          │
          ▼
[Dépôt GitHub (Page HTML/JS)]
          │
          ▼
[Déploiement GitHub Pages]
          │
          ▼
[Intégration WordPress (iFrame / Embed)]

```

## Source des données

Les fonds de carte et couches vectorielles sont gérés sur **ArcGIS Online** (Maison des Sciences de l'Homme d'Aquitaine - MSHA) :

* **WebMap Identifier :** `38e5e248b5674fc5a711974c6412f07d`
* **Configuration d'affichage :** Mode sombre (`theme=dark`) pour assurer la cohérence visuelle avec l'application hôte.

## Structure du code source

Le projet repose sur un fichier HTML unique (`maps.html`) structuré de la façon suivante :

* **Style (`<style>`) :**
* Utilisation des variables CSS natives (`:root`) pour la gestion du thème de couleurs.
* Mise en page fluide via Flexbox pour un affichage pleine hauteur (`100vh`).


* **Structure DOM (`<body>`) :**
* `.map-stack` : Conteneur principal.
* `.card-header` : En-tête de l'interface d'affichage.
* `.card-tabs` : Contrôles de navigation entre les vues.
* `.viewer-panel` : Conteneurs des `<iframe>` ArcGIS avec système de chargement (*loader* CSS).


* **Script (`<script>`) :**
* Fonction ES6 `switchTab(id, btn)` assurant la bascule du style d'affichage (`display: block / none`) et la mise à jour des classes d'onglets actifs sans rechargement de page.



## Paramétrage des vues ArcGIS

Les différentes vues du réseau s'appuient sur l'URL de l'application WebMap ArcGIS et ses arguments de requête :

* **Vue d'ensemble :** Charge le WebMap dans son emprise par défaut.
* **Vue détaillée :** Exploite les paramètres d'URL ArcGIS pour forcer le cadrage et l'échelle :
* `center=-0.607,44.800` (coordonnées WGS84)
* `scale=10000` (niveau de zoom à l'échelle 1:10 000)



## Procédure d'intégration WordPress

### 1. Déploiement source

Le fichier est hébergé via GitHub Pages à l'URL suivante :
`[https://eaubservatoire.github.io/Donn-es-cartographiques-Map-de-Pablo-/maps.html](https://eaubservatoire.github.io/Donn-es-cartographiques-Map-de-Pablo-/maps.html)`

### 2. Implémentation dans le CMS

L'intégration s'effectue dans un bloc HTML personnalisé sous WordPress :

#### Option A : Incrustation via iFrame

```html
<iframe 
    src="https://eaubservatoire.github.io/Donn-es-cartographiques-Map-de-Pablo-/maps.html" 
    width="100%" 
    height="850px" 
    style="border:none;" 
    allow="fullscreen">
</iframe>

```

#### Option B : Lien de redirection externe

```html
<a href="https://eaubservatoire.github.io/Donn-es-cartographiques-Map-de-Pablo-/maps.html" target="_blank" rel="noopener noreferrer">
    Ouvrir le Géoportail
</a>

```

## Spécifications techniques

* **Langages :** HTML5, CSS3 (Custom Properties), JavaScript (Vanilla ES6)
* **API / Service tiers :** ArcGIS WebMap Viewer
* **Polices :** Google Fonts (`DM Sans`, `Playfair Display`)
* **Compatibilité :** Responsive design (Mobile / Desktop)
