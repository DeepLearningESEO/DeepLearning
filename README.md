# Projet de Reconnaissance de Texte par Deep Learning

Ce projet vise à développer un système complet de reconnaissance de texte à partir d'images en utilisant des techniques de deep learning. Le processus est divisé en quatre étapes principales, allant de l'extraction des zones de texte jusqu'à la reconstruction finale du texte.

## Étape 1 : Extraction des zones de texte

**Objectif** : Identifier et extraire les régions contenant du texte dans une image.

- **Entrée** : Image complète
- **Sortie** : Images recadrées ne contenant que du texte
- **Approche** :
  - Création d'un modèle de détection de texte
  - Implémentation d'un algorithme de segmentation pour isoler les zones de texte (bounding-box)
  - Prétraitement des images pour améliorer la qualité de détection

**Ressources** :
- Dataset TextOCR pour l'entraînement et l'évaluation (https://textvqa.org/textocr/download/)
- Bibliothèques : PyTorch, TensorFlow, OpenCV

## Étape 2 : Segmentation des caractères

**Objectif** : Découper les images de texte en caractères individuels.

- **Entrée** : Image contenant du texte
- **Sortie** : Liste d'images, chacune contenant un seul caractère
- **Approche** :
  - Prétraitement (binarisation, normalisation)
  - Analyse des composantes connexes
  - Gestion des caractères qui se touchent (segmentation avancée)
  - Normalisation de la taille des caractères extraits

**Méthodes potentielles** :
- Méthodes basées sur les contours
- Méthodes de projection d'histogramme
- Approches par réseaux de neurones (U-Net)

## Étape 3 : Classification des caractères

**Objectif** : Identifier chaque caractère dans les images segmentées.

- **Entrée** : Image d'un caractère unique
- **Sortie** : Caractère identifié (texte)
- **Approche** :
  - Développement d'un CNN pour la classification
  - Utilisation de techniques d'augmentation de données
  - Évaluation et optimisation du modèle

**Ressources** :
- Dataset TMNIST (94 caractères) pour l'entraînement (https://www.kaggle.com/datasets/nikbearbrown/tmnist-alphabet-94-characters)

## Étape 4 : Reconstruction du texte

**Objectif** : Assembler les caractères identifiés en mots et phrases cohérents.

- **Entrée** : Liste de caractères
- **Sortie** : Texte reconstruit et corrigé
- **Approche** :
  - Regroupement des caractères en mots
  - Vérification orthographique avec dictionnaire
  - Correction contextuelle avec modèles de langage
  - Gestion des cas spéciaux (ponctuation, espaces)

**Techniques avancées** :
- Modèles de langage (n-grammes, BERT)
- Algorithmes de correction d'erreurs
- Analyse syntaxique pour la validation finale

## Structure du projet

```
DeepLearning/
│
├── Data/
│   ├── TextOCR/                # Dataset TextOCR
│   │   ├── Train/              # 21,778 images (6.6GB) + 714,770 annotations (272MB)
│   │   ├── Validation/         # 3,124 images + 107,802 annotations (39MB)
│   │   └── Test/               # 3,232 images (926MB) + metadata (1MB)
│   │
│   ├── TMNIST/                 # Dataset TMNIST pour la classification des caractères
│   │
│   └── Process/              # Données intermédiaires générées
│       ├── Text_Regions/       # Zones de texte extraites
│       ├── Characters/         # Caractères segmentés
│       └── Results/            # Résultats de reconnaissance
│
├── src/
│   ├── step1_text_detection/   # Extraction des zones de texte
│   ├── step2_char_segmentation/ # Segmentation des caractères
│   ├── step3_classification/   # Classification des caractères
│   ├── step4_text_reconstruction/ # Reconstruction du texte
│   └── utils/                  # Fonctions utilitaires
│
├── notebooks/                  # Jupyter notebooks pour l'exploration et les tests
│   ├── dataset_exploration.ipynb  # Analyse du dataset TextOCR
│   ├── model_evaluation.ipynb    # Évaluation des performances
│   └── pipeline_demo.ipynb       # Démonstration du pipeline complet
│
├── Models/                     # Modèles entraînés et checkpoints
│   ├── TextDetector/
│   ├── CharSegmenter/
│   ├── Classification/
│   └── TextReconstruction/
│
├── tests/                      # Tests unitaires et d'intégration
│
├── requirements.txt            # Dépendances du projet
│
└── README.md                   # Documentation principale

```

## Workflow de développement

1. **Configuration de PyCharm** :
   - Configurer l'interpréteur Python pour utiliser l'environnement virtuel
   - Paramétrer le formatage automatique (PEP 8)
   - Configurer les tests automatiques

2. **Gestion de version** :
   - Utiliser Git pour le contrôle de version
   - Créer des branches pour chaque étape du projet
   - Effectuer des revues de code régulières

3. **Méthodologie de travail** :
   - Réunions hebdomadaires pour suivre l'avancement
   - Développement itératif avec tests continus
   - Documentation du code et des décisions de conception

## Évaluation et métriques

- **Étape 1** : IoU (Intersection over Union), Précision/Rappel pour la détection
- **Étape 2** : Taux de segmentation correcte, erreurs de sur/sous-segmentation
- **Étape 3** : Précision, matrice de confusion, F1-score
- **Étape 4** : WER (Word Error Rate), CER (Character Error Rate)

---