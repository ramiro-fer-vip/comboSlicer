# comboSlicer

Segment hiérarchique à liste déroulante pour Power BI. Version **1.0.0.34**.

## 1. Mini manuel d'utilisation

### Installation
1. Prends le package `.pbiviz` dans le dossier `comboSilcer` sur https://github.com/ramiro-fer-vip/comboSlicer/.
2. Dans Power BI Desktop : `...` (autres visuels) > **Importer un visuel à partir d'un fichier**, puis sélectionne le package.
3. Le visuel `comboSlicer` apparaît dans le volet des visualisations.

### Affectation des données
Fais glisser les champs vers les rôles du visuel :
- **Hierarchy Fields** (1–15 colonnes) : les niveaux de hiérarchie, ex. Pays > Province > Ville, ou Année > Mois.
- **Filter Measure** (facultative, 0–1) : masque les membres à valeur zéro/vide et affiche la valeur à côté de chaque élément, ex. `(9 267,38)`.
- **Tooltips** (facultatives, 0–10) : mesures supplémentaires au survol.

### Interaction
- Clique l'en-tête pour développer/réduire. Clique une ligne pour la cocher ; cocher un parent coche tous ses enfants.
- États de l'en-tête : `(Tous)` = aucun filtre, une valeur unique, `Multiple (n)`, ou le nom de l'ancêtre commun quand toute la sélection partage un parent (ex. `Colombia (3)`).
- Utilise la loupe pour rechercher, l'icône de case pour Tout sélectionner et `✕` pour effacer.
- `Entrée` valide la recherche, `Échap` l'efface.
- Clic droit sur une ligne pour le menu natif (exploration).
- Les sélections filtrent les autres visuels du rapport et sont enregistrées dans le `.pbix` (y compris signets et segments synchronisés).

### Mise en forme (onglet Visuel)
- **Dropdown** : texte d'espace réservé ; position (`Top`, `Bottom`, `Top-right`, `Bottom-right` — les variantes `-right` ancrent le contrôle au bord droit) ; zone de recherche ; Tout sélectionner ; taille de police ; largeur fixe de l'en-tête ; fermer au départ de la souris ; fermer à la sélection ; hauteur du contrôle (`36` par défaut) ; espacement de l'étiquette (`4` par défaut).
- **Slicer header** : titre facultatif au-dessus du contrôle (nom du champ par défaut), avec police, gras et italique.
- **Dropdown expanded** : tout développer par défaut ; largeur/hauteur développées (`0` = automatique) ; typographie de la liste — taille (`12` par défaut), police (`Segoe UI`), gras, italique ; afficher les valeurs de mesure (désactivé par défaut).
- **Data Filtering** : masquer zéros/vides, texte d'état vide.
- **Hierarchy & Prefixes** : préfixes par niveau (séparés par des virgules) à retirer du texte (ex. `Univ., Université`), sans tenir compte de la casse.
- **Sorting** : ordre par niveaux 1–3 (`A-Z` par défaut ; aussi `Z-A` et `Ordre du modèle`, qui respecte le OrderBy) ; `Sort order` s'appelle désormais `Other levels order` et vaut pour les niveaux profonds. Le tri depuis l'en-tête (`...`) est prioritaire sauf `Ignorer le tri d'en-tête`.
- **Colors & Style** : arrière-plans en-tête/liste, couleurs de texte, accent des cases, bordure de sélection.

### Conseils de disposition
- La liste développée ne peut pas dépasser le cadre du visuel : dimensionne le cadre en hauteur (en-tête + liste).
- Garde les segments au premier plan dans le volet **Sélection** ; la zone vide laisse passer les clics et les visuels derrière restent modifiables.
- Les cartes de l'onglet **Général** (arrière-plan, effets, remplissage, titre) appartiennent au conteneur hôte et le visuel ne peut pas les prédéfinir — utilise un thème de rapport pour des valeurs uniformes.

## 2. Caractéristiques principales
- Segment hiérarchique multi-niveaux avec UX de liste déroulante.
- Filtrage par filtre JSON tuple (même canal que HierarchySlicer) : filtrage croisé fiable, persistance et aucune erreur de sélection de l'hôte.
- Suppression des préfixes par niveau, localisation en 5 langues (`en-US`, `es-ES`, `it-IT`, `fr-FR`, `de-DE`).
- Masquage des membres sans données piloté par la mesure, avec valeurs en ligne et info-bulles.

## 3. Modifications récentes
- **1.0.0.21** : filtrage migré vers JSON tuple (`applyJsonFilter`) + synchronisation des filtres ; sélection restaurée depuis les filtres du rapport.
- **1.0.0.22** : robustesse face aux vues de données dégénérées (changement de visuel).
- **1.0.0.23** : l'en-tête affiche l'ancêtre commun (`Colombia (3)`).
- **1.0.0.24** : fenêtre de données dans l'ordre du modèle (aucun tri par mesure).
- **1.0.0.25** : hauteur du contrôle (36 par défaut) et espacement supérieur (0 par défaut) ; tri par défaut de nouveau A-Z.
- **1.0.0.26** : positions `Top-right` / `Bottom-right` (contrôle ancré à droite).
- **1.0.0.27** : espacement supérieur remplacé par espacement de l'étiquette (4 par défaut).
- **1.0.0.28** : police, gras et italique dans l'en-tête.
- **1.0.0.29** : carte typographique `Dropdown expanded` ; exemples de préfixes en anglais ; séparateur `;` pour les préfixes.
- **1.0.0.30** : largeur/hauteur/tout-développer déplacés vers `Dropdown expanded` ; valeurs typographiques concrètes (12, Segoe UI).
- **1.0.0.31** : textes par défaut en anglais ; police d'en-tête Segoe UI ; afficher les valeurs déplacé vers `Dropdown expanded`, désactivé par défaut.
- **1.0.0.32** : tri par niveau (1–3) + `Ignorer le tri d'en-tête`.
- **1.0.0.33** : tout sélectionner conserve les coches (filtre complet explicite) ; résilience au changement de source (réinitialisation session, nettoyage filtres obsolètes, mesure désalignée ignorée).
- **1.0.0.34** : révision technique de la localisation (terminologie plateforme par langue).
