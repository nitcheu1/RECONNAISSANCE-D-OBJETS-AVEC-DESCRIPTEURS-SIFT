# RECONNAISSANCE-D-OBJETS-AVEC-DESCRIPTEURS-SIFT
Ce projet consiste à l’utilisation des descripteurs SIFT afin de déterminer la classe d’appartenance d’une image fournie en entrée après comparaison des descripteurs de cette image avec un ensemble d’images appartenant à des classes différentes
# PRETRAITEMENT DU DATASET
Comme dataset nous avons porté notre choix sur le dataset Columbia Object Image Library (COIL-100) qui est une base de données constituée d’images en couleur de 100 objets différents avec 72 prises par objets à des positions différentes. Le dataset est donc constitué de 7200 images réparties en 100 classes dont 72 images par classe. Pour le développement de notre modèle, nous avons intégré dans notre programme un module permettant de diviser la base d’image en 50% d’images d’entraînement et 50% d’images test.
# LES DIFFÉRENTES ÉTAPES DU DÉVELOPPEMENT DU MODÈLE
# Transformation des images
Dans le but d’utiliser aisément nos images, nous avons procédé comme il suit:
Chargement des images dans l’espace de travail et Transformation des images en niveau de gris
# Calcul des descripteurs
Grâce à la méthode sift.detectAndCompute fournie dans OpenCV nous avons obtenu les keypoints de chaque image dont nous avons ensuite calculé les descripteurs correspondants. Pour ne pas avoir à recalculer les descripteurs de chaque keypoint à chaque exécution de notre programme, nous avons conservé ces derniers dans deux fichiers différents. Ensuite grâce à la méthode cv.drawKeypoints nous avons affiché les keypoints de chaque image.
# MATCHING ENTRE LES IMAGES
# Entre les deux images
Pour calculer les correspondances entre deux images, on récupère les descripteurs et les keypoints de chacune de ces images et grâce aux fonctions bf = cv.BFMatcher() et bf.knnMatch(des1,des2,k=2), on calcul la correspondance entre les keypoints et à partir de la valeur de k on récupère précisément la correspondance entre k points. Ensuite on calcul le ratio entre les distances les plus proches et l’ensemble des matches points qu’on compare à un certain seuil prédéfini afin d’obtenir les meilleures correspondances dites goodpoints.
# Entre une image et plusieurs autres images
Ici en plus des étapes citées ci-dessus, nous avons calculé la similarité entre l’image d’entrée et l’ensemble d’images d'entraînement. Cette similarité est calculée en faisant le rapport entre les meilleures correspondances sur le total des correspondances. Nous avons ensuite trié les similarités par ordre décroissant . La classe qui a le plus grand score d’apparition sur un nombre k(KNN) est la classe d’appartenance de l’image prise en entrée.
# EVALUATION DU MODELE
Dans le but d’évaluer notre modèle, nous avons effectué une prédiction de la classe d’appartenance de l’ensemble de nos images test. Cette prédiction nous a permis de compter le nombre de prédiction VRAI et le nombre de prédiction FAUSSE. Nous récupérons également les True Label (les vraies valeurs). L’image suivante présente les vraies classes de nos images test. Lorsque le modèle n’a pas pu détecter une classe d’appartenance à une image, il affiche ‘0’.
# MATRICE DE CONFUSION
Grâce aux prédictions faites et les trues labels, nous avons déterminé la matrice deconfusion représentée par la figure ci-dessous. Nous avons également calculé l’accuracy qui a donné une valeur de 92%.
