# ID'coiff — Maquette de site vitrine

Maquette de présentation pour **ID'coiff**, salon de coiffure mixte & barbier à
Amiens (56 boulevard Pasteur). Une **page HTML unique, 100 % autonome** : tout le
CSS et le JavaScript sont inclus dans `index.html`, **aucune dépendance externe**,
**aucune image externe**. Déployable telle quelle.

> **But de la maquette** : montrer au salon un aperçu crédible et haut de gamme de
> ce que pourrait être son site. Le site ne remplace pas Planity — il y conduit
> joliment (bouton « Prendre rendez-vous » partout).

---

## 🎨 Personnalisation en 4 étapes

Tout se règle dans `index.html`. Cherchez les marqueurs entre crochets
(`[ ... ]`) : ce sont les seuls éléments à remplacer.

### 1. Les 2 couleurs de la marque
La maquette est en **thème sombre** : **fond noir, texte et boutons dorés**
(texte noir sur les boutons), repris du logo ID'coiff. Les 2 couleurs pilotes
sont dans le bloc **« COULEURS DE LA MARQUE »** (`:root`) du `<style>` :

```css
--color-primary: #0f0f0f; /* NOIR  — fond principal */
--color-accent:  #c9a227; /* DORÉ  — texte, boutons, détails */
```

**Tout le reste** — fonds, textes, bordures, survols, ombres — en découle
automatiquement via `color-mix()` (contrastes WCAG AA vérifiés). Le bloc de tokens
juste en dessous (`--surface`, `--ink`, `--cta-*`…) définit le thème sombre ;
pour repasser à un thème clair, il suffit d'inverser ce bloc.

Si vous changez la couleur principale, mettez aussi à jour la balise
`<meta name="theme-color">` (seule couleur « en dur », car non dérivable).

### 1 bis. Le logo
Le logo est **intégré directement dans `index.html`** (image encodée en base64
dans la variable CSS `--logo`) : le fichier reste donc **100 % autonome**, sans
aucune image externe. Il s'affiche **en cercle** dans l'en-tête et le pied de page.
Pour changer de logo, remplacez l'URL `data:` de la variable `--logo`.

### 2. Le lien de réservation Planity
Remplacez **toutes** les occurrences de `[LIEN PLANITY]` par l'URL Planity du salon
(en-tête, hero, carte contact, bandeau, barre mobile, pied de page).

### 3. Les photos
Chaque emplacement `[PHOTO À FOURNIR]` est un bloc `<figure class="photo">`.
Remplacez-le par une `<img src="…" alt="…">` (ou un `background-image`) quand les
photos sont disponibles. Le cadre est déjà pensé pour de belles images
(ambiance du salon, réalisations avant/après, équipe).

### 4. Les textes et coordonnées
Remplacez les marqueurs `[À REMPLACER]`, `[Prénom]`, `[Votre nom]`, etc. :
- présentation du salon et de l'équipe,
- **grille de tarifs réelle** (les prix affichés sont *indicatifs* et signalés
  « Tarifs à confirmer » — à valider avec le salon),
- **horaires réels** (ceux affichés sont indicatifs),
- crédit freelance dans le pied de page.

---

## ✅ Checklist avant mise en ligne

- [x] Thème noir & doré réglé — ajuster si besoin
- [x] Logo intégré (base64 dans `index.html`)
- [ ] Remplacer tous les `[LIEN PLANITY]`
- [ ] Remplacer **toutes** les URL `[VOTRE-DOMAINE]` par le vrai domaine
      (`canonical`, `og:url`, `og:image`, et les champs `image`/`url` du JSON-LD)
- [ ] Confirmer et corriger **tarifs** et **horaires** (page + JSON-LD)
- [ ] Insérer les vraies **photos** (+ une image de partage `og:image`)
- [ ] Vérifier téléphone, adresse, lien Facebook
- [ ] Compléter les membres de l'équipe (ou masquer la section)

---

## 🚀 Déploiement (Vercel)

Le dépôt contient un `vercel.json` qui force un **déploiement statique** (aucun
build) :

```json
{ "framework": null, "outputDirectory": "." }
```

Import du dépôt sur Vercel → le site est servi tel quel (`index.html` à la racine).
Si Vercel avait détecté un framework (ex. « Next.js »), ce fichier corrige l'erreur
`No Next.js version detected` en repassant le projet en preset **« Other »**.

Fonctionne aussi sur tout hébergement statique (Netlify, GitHub Pages, o2switch…) :
il suffit de déposer `index.html`.

---

## 🔎 Ce qui est déjà en place

- **Mobile-first** irréprochable dès 375 px : barre d'action collante en bas
  (Appeler + Prendre rendez-vous), zones tactiles ≥ 44 px, aucun défilement
  horizontal, texte lisible sans zoom.
- **SEO local** : `title`, meta description, Open Graph, et données structurées
  **`HairSalon`** (adresse, horaires, prestations) en JSON-LD.
- **Accessibilité** : structure sémantique, lien d'évitement, focus visibles,
  contraste AA garanti (même avec une couleur de marque claire), respect de
  `prefers-reduced-motion`.
- **Design** : un seul rayon d'arrondi, une seule ombre, échelle d'espacement de
  8 px, typographie de titre en serif chic (polices système), apparition douce au
  défilement.

---

## ♻️ Réutiliser pour un autre salon

Le code est commenté et découpé en sections (`===== SECTION =====`). Pour un autre
salon : dupliquer `index.html`, changer les 2 couleurs, le nom, les coordonnées,
les prestations et les photos. Le système de design suit automatiquement.
