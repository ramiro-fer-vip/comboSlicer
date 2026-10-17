# comboSlicer

Segment hiérarchique à liste déroulante pour Power BI. Version **1.0.0.42**.

Segment à liste déroulante qui construit une hiérarchie multiniveau à partir de plusieurs champs, filtre le rapport via le modèle de filtres standard de Power BI et gère la suppression de préfixes, le tri, le filtrage piloté par mesure et la sélection simple ou multiple.

---

## 1. Mini manuel d'utilisation

### Installation
1. Récupère le package `.pbiviz` dans le dossier `comboSilcer` sur https://github.com/ramiro-fer-vip/comboSlicer/.
2. Dans Power BI Desktop : `...` (autres visuels) > **Importer un visuel à partir d'un fichier**, puis sélectionne le package.
3. Le visuel `comboSlicer` apparaît dans le volet des visualisations. Épingle-le pour le réutiliser.

### Affectation des données
| Rôle | Type | Plage | Usage |
| --- | --- | --- | --- |
| **Hierarchy Fields** | Regroupement | 1–15 | Niveaux de la hiérarchie, ex. Pays > Province > Ville, ou Année > Mois |
| **Filter Measure** | Mesure | 0–1 | Masque les membres à valeur zéro/vide et affiche la valeur à côté de chaque élément, ex. `(9 267,38)` |
| **Tooltips** | Mesure | 0–10 | Mesures supplémentaires au survol |

L'ordre des champs définit la hiérarchie : le **premier champ est le niveau racine**, le dernier est le niveau feuille.

### Interaction
- Clique l'en-tête pour développer ou réduire.
- Clique une ligne pour la cocher/décocher. Cocher un parent coche tous ses enfants ; les sélections partielles affichent un état indéterminé.
- États de l'en-tête : `(Tous)` (aucun filtre), une valeur unique, `Multiple (n)`, ou le nom de l'**ancêtre commun** quand toute la sélection partage un parent (ex. `Colombia (3)`).
- Icônes de la barre : recherche (filtre la liste), Tout sélectionner (case), effacer (`✕`), flèche (développer/réduire) et, si l'auteur l'active, le bouton simple/multiple.
- `Entrée` dans la recherche valide, `Échap` l'efface.
- Clic droit sur une ligne pour le menu natif de Power BI (exploration).
- Les sélections filtrent les autres visuels et sont enregistrées dans le `.pbix`, y compris signets et segments synchronisés.

---

## 2. Référence complète des propriétés (volet Mise en forme > Visuel)

### Menu déroulant
| Propriété | Défaut | Description |
| --- | --- | --- |
| Texte par défaut | *(vide)* | Texte de l'en-tête sans sélection. Vide = `(Tous)` localisé. |
| Position du contrôle | `Haut` | `Haut` / `Bas` / `Haut-droit` / `Bas-droit`. `Haut*` développe vers le bas, `Bas*` vers le haut ; les variantes `-droit` ancrent le contrôle et la liste au bord droit. |
| Afficher la zone de recherche | `Oui` | Affiche l'icône de recherche dans l'en-tête. |
| Afficher Sélectionner tout | `Oui` | Affiche l'icône Tout sélectionner (masquée automatiquement en mode unique). |
| Taille de police | `12` | Taille du texte de l'en-tête. |
| Largeur du contrôle (px) | `0` | Largeur fixe de l'en-tête. `0` = occupe la largeur du visuel. |
| Fermer à la sortie de la souris | `Oui` | Ferme la liste quand le pointeur quitte le contrôle. |
| Fermer lors de la sélection | `Non` | Ferme la liste après chaque sélection. |
| Hauteur du contrôle (px) | `36` | Hauteur de la boîte du contrôle. |
| Espacement de l'étiquette (px) | `2` | Espace entre l'étiquette et la boîte du contrôle. |

### Liste développée
| Propriété | Défaut | Description |
| --- | --- | --- |
| Taille de police | `12` | Taille du texte des éléments. |
| Police | `Segoe UI` | Police des éléments. |
| Gras | `Non` | Éléments en gras. |
| Italique | `Non` | Éléments en italique. |
| Tout développer par défaut | `Oui` | Développe toutes les branches à l'ouverture. |
| Largeur développée (px) | `0` | Largeur fixe de la liste. `0` = comme le contrôle. |
| Hauteur développée (px) | `0` | Hauteur fixe de la liste. `0` = automatique (limitée au cadre). |
| Afficher les valeurs de mesure | `Non` | Affiche la valeur de la mesure en ligne à côté de chaque élément. |

### Sélection multiple
| Propriété | Défaut | Description |
| --- | --- | --- |
| Autoriser la sélection multiple | `Oui` | `Oui` = sélection multiple. `Non` = une seule branche/nœud, Tout sélectionner est masqué et l'indicateur devient un carré plein. |
| Afficher la sélection multiple | `Non` | Affiche un bouton dans l'en-tête pour que l'utilisateur bascule simple/multiple à l'exécution (la modification est enregistrée). |
| Couleur de sélection unique | `#ef4444` | Remplissage et bordure du carré plein utilisé en mode unique. |
| Couleur du bouton | `#990000` | Couleur du bouton d'en-tête (le distingue de Tout sélectionner). |

### En-tête de segment
| Propriété | Défaut | Description |
| --- | --- | --- |
| Afficher l'en-tête | `Oui` | Affiche le titre au-dessus du contrôle. |
| Texte de l'en-tête | *(vide)* | Texte du titre. Vide = nom du premier champ. |
| Taille de police de l'en-tête | `12` | Taille du titre. |
| Couleur de l'en-tête | *(thème)* | Couleur du titre. |
| Police de l'en-tête | `Segoe UI` | Police du titre. |
| Gras / Italique | `Non` | Style du titre. |

### Filtrage des données
| Propriété | Défaut | Description |
| --- | --- | --- |
| Masquer les valeurs à zéro | `Oui` | Supprime les membres dont la mesure de filtre vaut `0`. |
| Masquer les valeurs vides | `Oui` | Supprime les membres dont la mesure de filtre est vide. |
| Texte si aucun enregistrement | *(vide)* | Message affiché dans la liste sans données. Vide = `- Aucun enregistrement -` localisé. |

### Hiérarchie et préfixes
| Propriété | Défaut | Description |
| --- | --- | --- |
| Ignorer la casse des préfixes | `Oui` | Comparaison des préfixes sans tenir compte de la casse. |
| Préfixes à ignorer Niveau 1…5 | *(vide)* | Préfixes séparés par virgule ou point-virgule, retirés du texte affiché à chaque niveau, ex. `Univ. ; Université`. Le nom n'est jamais vide. |

### Tri
| Propriété | Défaut | Description |
| --- | --- | --- |
| Ordre niveau 1 / 2 / 3 | `Alphabétique (A-Z)` | Ordre par niveau : `Alphabétique (A-Z)`, `Alphabétique (Z-A)` ou `Ordre du modèle de données` (respecte **Trier par colonne / OrderBy** du champ). |
| Ordre des autres niveaux | `Alphabétique (A-Z)` | Mêmes options, pour les niveaux 4 et suivants. |
| Ignorer le tri de l'en-tête du visuel | `Non` | `Oui` ignore le tri choisi dans l'en-tête (`...` > Trier l'axe) et rend la main à ce volet (ex. pour rétablir l'ordre du modèle). |

### Couleurs et style
| Propriété | Défaut | Description |
| --- | --- | --- |
| Arrière-plan de l'en-tête | *(thème)* | Fond de la boîte du contrôle. |
| Couleur du texte de l'en-tête | *(thème)* | Couleur du texte de l'en-tête. |
| Arrière-plan du menu déroulant | *(thème)* | Fond de la liste développée. |
| Couleur du texte des éléments | *(thème)* | Couleur des éléments de la liste. |
| Couleur de la case à cocher | *(accent)* | Accent des cases de sélection multiple. |
| Bordure de sélection | `Oui` | Dessine une bordure autour du contrôle lorsqu'une sélection est active. |
| Couleur de bordure avec sélection | `#2563eb` | Couleur de la bordure. |
| Épaisseur de bordure avec sélection | `1` | Épaisseur de la bordure en px. |

### Info-bulle
| Propriété | Défaut | Description |
| --- | --- | --- |
| Afficher les info-bulles | `Non` | Active les cartes d'info-bulle natives (y compris les pages d'info-bulle du rapport). |

---

## 3. Notes de comportement

- **Modèle de filtrage** : les sélections sont appliquées comme filtre JSON tuple via `applyJsonFilter` (même canal que HierarchySlicer). Cela garantit un filtrage croisé fiable, évite les erreurs de sélection de points de données de l'hôte et persiste dans le rapport.
- **Persistance** : la sélection courante est restaurée depuis les filtres du rapport à chaque mise à jour ; elle survit donc à l'enregistrement/réouverture, aux signets et aux segments synchronisés.
- **Changement de source** : si les champs liés changent, le visuel réinitialise son état de session (univers, caches, développements) et nettoie automatiquement les filtres obsolètes. Une mesure de filtre désalignée est ignorée au lieu de masquer des lignes.
- **Exemples de préfixes** : affichés en anglais dans le volet de mise en forme (les espaces réservés ne sont pas localisables dans le modèle de mise en forme actuel).
- **Réduction des données** : utilise `window`, qui conserve l'ordre du modèle (pas de réordonnancement Top-N par mesure).

---

## 4. Conseils de disposition

- La liste développée **ne peut pas dépasser le cadre du visuel** : dimensionne le cadre en hauteur (en-tête + liste). C'est la seule voie fiable dans **Power BI Service**, où chaque visuel s'exécute dans un iframe cross-origin et ne peut pas se placer au-dessus des autres.
- Dans Desktop, le visuel élève son conteneur pendant l'ouverture ; dans le Service, l'ordre se contrôle depuis le rapport.
- Garde les segments au premier plan dans le volet **Sélection** (ou active *Conserver l'ordre des couches*). Les zones transparentes laissent passer les clics, ce qui reste derrière demeure modifiable.
- Les cartes de l'onglet **Général** (arrière-plan, effets, remplissage, titre) appartiennent au conteneur hôte et le visuel ne peut pas les prédéfinir — utilise un thème de rapport pour des valeurs uniformes.

---

## 5. Localisation

Le visuel inclut des traductions complètes pour `en-US`, `es-ES`, `it-IT`, `fr-FR` et `de-DE`.

---

## 6. Journal des modifications (récent)

- **1.0.0.21** : filtrage migré vers JSON tuple (`applyJsonFilter`) + synchronisation des filtres.
- **1.0.0.22** : robustesse face aux vues de données dégénérées.
- **1.0.0.23** : l'en-tête affiche l'ancêtre commun.
- **1.0.0.24** : la fenêtre de données conserve l'ordre du modèle.
- **1.0.0.25–1.0.0.27** : hauteur du contrôle, espacement de l'étiquette, positions `Haut-droit` / `Bas-droit`.
- **1.0.0.28–1.0.0.31** : police/gras/italique de l'en-tête, typographie `Liste développée`, textes par défaut en anglais, valeurs de mesure déplacées et désactivées par défaut.
- **1.0.0.32** : tri par niveau (1–3) et `Ignorer le tri de l'en-tête du visuel`.
- **1.0.0.33** : tout sélectionner conserve les coches ; résilience aux changements de source.
- **1.0.0.34** : révision technique de la localisation.
- **1.0.0.35–1.0.0.36** : titre visible sans données, en-tête stable piloté par le filtre propre, espacement cohérent.
- **1.0.0.37** : espacement de l'étiquette 2px par défaut.
- **1.0.0.38–1.0.0.41** : mode sélection simple/multiple, indicateur carré plein, bouton dans l'en-tête, carte `Sélection multiple` (activé par défaut).
- **1.0.0.42** : élévation du conteneur hôte pendant l'ouverture de la liste ; limite de plateforme documentée dans le Service.
