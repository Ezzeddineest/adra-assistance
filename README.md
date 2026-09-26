# ADRA Assistance — site web (base V1)

Site vitrine statique, pensé mobile d'abord, dont le seul objectif est de déclencher un appel au **25 755 755**.

## Contenu du dossier

| Fichier | Rôle |
| --- | --- |
| `index.html` | Homepage complète : HTML, CSS et JS dans un seul fichier, sans dépendance |
| `mentions-legales.html` | Modèle à compléter (raison sociale, MF, adresse, hébergeur) |
| `politique-de-confidentialite.html` | Modèle à faire valider juridiquement |
| `modele-page-locale.html` | Gabarit des futures pages `/depannage-{ville}` et `/remorquage-{ville}` (en `noindex`) |
| `robots.txt`, `sitemap.xml` | SEO technique. Remplacer `VOTRE-DOMAINE.tn` partout |
| `*.woff2`, `logo-adra*`, `favicon.svg` | Polices, logo et favicon, placés à la racine pour simplifier l'envoi sur GitHub |

## Pourquoi une page statique

Pour un site d'urgence, la vitesse sur un réseau mobile moyen compte plus que tout. Une page HTML statique, sans framework, s'affiche immédiatement, s'héberge partout (Netlify, Vercel, Cloudflare Pages, OVH, hébergeur tunisien) pour un coût quasi nul, et reste facile à modifier. Si le site grandit (pages par ville, blog, version arabe), la même structure se transpose telle quelle dans **Astro**, qui génère aussi du HTML statique.

## Mise en ligne : checklist

1. **Photos réelles** : remplacer les illustrations provisoires.
   - Hero : dans `index.html`, décommenter le bloc `<picture>` sous le commentaire « PHOTO RÉELLE À INTÉGRER ICI » et supprimer le `<svg>` qui suit, ainsi que le libellé `.media-tag`.
   - Galerie flotte : remplacer chaque `<svg class="art">` par une `<img>` / `<picture>` avec `loading="lazy"`, `width`/`height` renseignés et un `alt` descriptif. Les classes CSS restent identiques ; ajouter `style="position:absolute;inset:0;width:100%;height:100%;object-fit:cover"`.
   - Formats : AVIF + WebP en 640 / 1280 / 1920 px. Hero sous 180 Ko en 640 px.
2. **Logo** : le logo réel est intégré en JPG/WebP. Le remplacer par une version SVG dès qu'elle est disponible, et générer un favicon à partir de ce SVG.
3. **Domaine** : remplacer `https://www.VOTRE-DOMAINE.tn` dans `index.html`, `robots.txt`, `sitemap.xml`.
4. **SMS** : confirmer que le 25 755 755 reçoit les SMS. Sinon, dans le script, remplacer `smsHref()` par un lien WhatsApp (`https://wa.me/216XXXXXXXX?text=…`).
5. **Formulaire partenaire** : le brancher sur un service d'envoi (Formspree, Getform, ou votre backend) à l'endroit marqué `TODO production`.
6. **Avis** : remplacer les trois emplacements `.rev` par des avis réels (idéalement Google Business Profile). Ne jamais publier d'avis inventés.
7. **Mesure** : installer GA4 via Google Tag Manager. Chaque bouton d'appel pousse `click_to_call` avec son emplacement (`call-hero`, `call-sticky`, `call-final`…) dans `dataLayer` : c'est l'indicateur de conversion principal.
8. **Google Business Profile** : créer/compléter la fiche avec le même nom, le même numéro et le lien du site (cohérence NAP).
9. **Polices** : Barlow et Barlow Condensed sont déjà auto-hébergées dans `fonts/` (WOFF2, licence SIL Open Font License) : aucun appel à Google Fonts.

## Numéro de téléphone

Tous les liens utilisent `tel:+21625755755` (format international). Il fonctionne depuis une SIM tunisienne comme depuis une SIM étrangère (visiteurs algériens, libyens, diaspora), alors que `tel:25755755` échoue hors du réseau tunisien. L'affichage reste « 25 755 755 ».

Le numéro apparaît dans : le header, le hero, la barre d'appel fixe (mobile), l'étape 01, la section « Pourquoi ADRA », la FAQ, le CTA final et le footer.

## Pages locales

Ne créer une page `/depannage-{ville}` que pour une zone réellement couverte. Chaque page doit avoir un texte propre à la ville ; des pages dupliquées en changeant seulement le nom de la ville sont pénalisées par Google. Retirer le `noindex` et ajouter l'URL au `sitemap.xml` une fois la page rédigée.

## Direction artistique (rappel)

Thème blanc et rouge, construit sur le rouge exact du logo ADRA.

| Token | Valeur | Usage |
| --- | --- | --- |
| Blanc | `#FFFFFF` | Fond principal |
| Surface | `#F6F4F3` | Sections alternées, footer |
| Encre | `#17191E` | Titres et texte principal |
| Encre secondaire | `#464C57` | Texte courant |
| Rouge ADRA | `#AE2E2B` | Boutons d'appel, blocs de marque (hero, carte Remorquage, CTA final) |
| Rouge clair | `#C23531` | Survol, dégradés |
| Rouge profond | `#8A221F` | Fin des dégradés |
| Teinte rouge | `#FBF0EF` | Fonds d'icônes, encadrés |

Typographies : Barlow Condensed (titres ; italique 800 pour le H1 et les numéros, en écho au logo), Barlow (texte).
Logo : `img/logo-adra.*` (version complète, footer) et `img/logo-adra-mark.*` (version recadrée sans le numéro, header). Une version vectorielle (SVG) du logo améliorera la netteté.
