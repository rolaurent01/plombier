# PROMPT CLAUDE CODE — Refonte site Plombier Lyon

> **Site actuel :** https://lyon.plomberie-roche.fr/
> **Framework :** Astro
> **Style :** Artisan premium (chaleureux, confiance)
> **Objectif :** Devenir le plombier le plus visible à Lyon sur Google et transformer chaque visite en appel

---

## PHASE 0 — Crawl & Analyse du site existant

Avant toute chose, parcours le site actuel https://lyon.plomberie-roche.fr/ pour :

1. **Récupérer tout le contenu existant** : textes, services mentionnés, numéro de téléphone, adresse, nom de l'entreprise, horaires, tarifs affichés, zones d'intervention
2. **Capturer la structure actuelle** : pages existantes, navigation, URLs
3. **Identifier les assets réutilisables** : logo, images, couleurs actuelles
4. **Noter les points faibles UX/SEO** : ce qui manque, ce qui est mal structuré

Consigne : **Ne perds aucune information existante.** Tout doit être récupéré et réintégré dans la nouvelle version, en mieux.

---

## PHASE 1 — Architecture du projet Astro

Crée un projet Astro avec cette structure :

```
src/
├── layouts/
│   └── BaseLayout.astro          # Layout principal (head SEO, header, footer, schema.org)
├── components/
│   ├── Header.astro              # Navigation + téléphone sticky
│   ├── Footer.astro              # Infos contact, liens, zones
│   ├── HeroBanner.astro          # Banner principal avec CTA appel
│   ├── ServiceCard.astro         # Carte service réutilisable
│   ├── TestimonialCard.astro     # Carte avis client
│   ├── PriceTable.astro          # Tableau tarifs transparent
│   ├── CTACall.astro             # Bouton appel flottant mobile
│   ├── TrustBadges.astro         # Badges confiance (24/7, garantie, etc.)
│   ├── ZoneMap.astro             # Carte zones d'intervention
│   ├── BeforeAfter.astro         # Composant avant/après intervention
│   ├── FAQAccordion.astro        # FAQ en accordéon (SEO rich snippets)
│   └── BlogPostCard.astro        # Carte article blog
├── pages/
│   ├── index.astro               # Page d'accueil /plombier-lyon
│   ├── services/
│   │   ├── fuite-eau-lyon.astro
│   │   ├── debouchage-canalisation-lyon.astro
│   │   ├── reparation-chauffe-eau-lyon.astro
│   │   ├── wc-bouche-lyon.astro
│   │   ├── recherche-fuite-lyon.astro
│   │   └── installation-chauffe-eau-lyon.astro
│   ├── zones/
│   │   ├── plombier-lyon-1.astro
│   │   ├── plombier-lyon-2.astro
│   │   ├── plombier-lyon-3.astro
│   │   ├── plombier-lyon-4.astro
│   │   ├── plombier-lyon-5.astro
│   │   ├── plombier-lyon-6.astro
│   │   ├── plombier-lyon-7.astro
│   │   ├── plombier-lyon-8.astro
│   │   ├── plombier-lyon-9.astro
│   │   ├── plombier-villeurbanne.astro
│   │   ├── plombier-bron.astro
│   │   ├── plombier-caluire.astro
│   │   ├── plombier-venissieux.astro
│   │   └── plombier-decines.astro
│   └── blog/
│       ├── index.astro
│       ├── que-faire-fuite-eau.astro
│       ├── comment-couper-eau-appartement.astro
│       ├── comment-deboucher-evier.astro
│       ├── pourquoi-chauffe-eau-fuit.astro
│       └── wc-bouche-que-faire.astro
├── data/
│   ├── services.json             # Données services (titre, description, prix, slug)
│   ├── zones.json                # Données zones (nom, arrondissement, description, spécificités)
│   ├── testimonials.json         # Avis clients
│   └── prices.json               # Grille tarifaire
├── styles/
│   └── global.css                # Design system + variables CSS
└── utils/
    └── seo.ts                    # Helpers SEO (meta, schema.org, sitemap)
```

---

## PHASE 2 — Design System "Artisan Premium"

### Direction artistique

Le design doit inspirer **confiance immédiate** et **chaleur humaine**. On vise l'image d'un artisan sérieux, local, fiable — pas une grosse franchise froide.

### Palette de couleurs

```css
:root {
  /* Couleurs principales */
  --color-primary: #1B4965;       /* Bleu profond — confiance, professionnalisme */
  --color-primary-light: #5FA8D3; /* Bleu clair — accents */
  --color-accent: #F4A261;        /* Orange chaud — urgence, CTA, chaleur artisan */
  --color-accent-dark: #E76F51;   /* Orange foncé — hover CTA */

  /* Neutres */
  --color-bg: #FAFAF8;            /* Fond crème très léger — chaleureux */
  --color-bg-alt: #F0EDE8;        /* Fond sections alternées */
  --color-text: #2D2D2D;          /* Texte principal */
  --color-text-light: #6B6B6B;    /* Texte secondaire */

  /* Confiance */
  --color-success: #2D6A4F;       /* Vert — garantie, validation */
  --color-stars: #F4A261;         /* Étoiles avis */
}
```

### Typographie

- **Titres :** Police serif chaleureuse (ex: Playfair Display, Lora, ou Merriweather) — évoque le savoir-faire artisan
- **Corps :** Sans-serif lisible (Inter, Source Sans Pro) — modernité et lisibilité
- **Tailles :** Hiérarchie claire, H1 grand et impactant, corps 16px minimum pour le mobile

### Principes de design

- **Mobile-first absolu** — 80%+ du trafic sera mobile (urgence = smartphone)
- **Bouton appel flottant** toujours visible sur mobile (position: fixed, bas de l'écran)
- **Numéro de téléphone cliquable** partout, visible dans le header sticky
- **Espacement généreux** — respiration, pas d'étouffement
- **Photos réelles** plutôt qu'illustrations génériques quand possible
- **Micro-animations subtiles** — entrées en scroll, hover states soignés
- **Aucun carrousel** — tout doit être visible sans interaction

---

## PHASE 3 — Pages à produire

### 3.1 Page d'accueil (`/` = `/plombier-lyon`)

**Titre SEO :** `Plombier Lyon (69000) — Dépannage Urgent 24/7 | Intervention 30 min`

**Meta description :** `Plombier à Lyon disponible 24h/24 pour dépannage plomberie : fuite d'eau, débouchage canalisation, réparation chauffe-eau. Intervention rapide en 30 minutes. Devis gratuit.`

**Structure de la page :**

1. **Hero Banner**
   - Titre H1 : "Plombier à Lyon — Dépannage Urgent 24h/24"
   - Sous-titre : "Intervention en 30 minutes dans tout Lyon et sa métropole"
   - Bouton CTA principal : "Appeler maintenant — [NUMÉRO]" (lien tel:)
   - Bouton secondaire : "Devis gratuit"
   - Badges de confiance en ligne : ⏰ 24h/24 • 🔧 Garanti • 💰 Devis clair • ⭐ 4.8/5

2. **Bandeau de confiance**
   - Note Google (étoiles + nombre d'avis)
   - Années d'expérience
   - Nombre d'interventions
   - Certifications / assurance

3. **Section Services** (grille de 6 cartes)
   - Fuite d'eau
   - Débouchage canalisation
   - Réparation chauffe-eau
   - WC bouché
   - Recherche de fuite
   - Installation chauffe-eau
   - Chaque carte → lien vers sa page dédiée

4. **Section Tarifs transparents**
   - Tableau clair avec prix indicatifs
   - "Pas de surprise, pas de frais cachés"
   - Déplacement : 60€
   - Débouchage : à partir de 90€
   - Recherche de fuite : à partir de 120€

5. **Section Avis clients**
   - 3-4 témoignages avec nom, arrondissement, étoiles
   - Lien vers les avis Google

6. **Section "Pourquoi nous choisir"**
   - Artisan local lyonnais
   - Intervention garantie
   - Prix fixés à l'avance
   - Disponibilité 24/7

7. **Section Zones d'intervention**
   - Carte ou liste visuelle des arrondissements + villes
   - Liens internes vers chaque page zone

8. **FAQ**
   - 5-6 questions fréquentes (avec schema.org FAQPage)
   - "Combien coûte un dépannage plomberie ?"
   - "En combien de temps intervenez-vous ?"
   - "Intervenez-vous le dimanche ?"
   - "Faut-il un devis avant intervention ?"

9. **CTA final**
   - "Une urgence plomberie ? Appelez-nous maintenant"
   - Bouton appel + numéro

---

### 3.2 Pages Services (×6)

**Template commun, contenu unique par service.**

Chaque page service doit contenir :

- **H1** : "[Service] à Lyon — Intervention Rapide 24h/24"
- **Introduction** : Description du problème que le client rencontre (empathie)
- **Section "Le problème"** : Explication simple, causes courantes
- **Section "Notre solution"** : Comment on intervient, étapes
- **Prix indicatif** : Tarif clair
- **Témoignage client** lié à ce service
- **FAQ spécifique** au service (3-4 questions, schema.org)
- **CTA appel** : Bouton + numéro
- **Liens internes** vers autres services et zones

**Titres SEO par page :**

| Page | Title |
|------|-------|
| fuite-eau-lyon | Fuite d'eau Lyon — Réparation Urgente 24/7 \| Plombier Lyon |
| debouchage-canalisation-lyon | Débouchage Canalisation Lyon — Intervention Rapide \| Plombier Lyon |
| reparation-chauffe-eau-lyon | Réparation Chauffe-eau Lyon — Dépannage Express \| Plombier Lyon |
| wc-bouche-lyon | WC Bouché Lyon — Débouchage Urgent 24h/24 \| Plombier Lyon |
| recherche-fuite-lyon | Recherche de Fuite Lyon — Détection Professionnelle \| Plombier Lyon |
| installation-chauffe-eau-lyon | Installation Chauffe-eau Lyon — Pose & Remplacement \| Plombier Lyon |

---

### 3.3 Pages Zones géographiques (×14)

**Template commun, contenu unique par zone.**

Chaque page zone doit contenir :

- **H1** : "Plombier [Zone] — Dépannage Urgent 24h/24"
- **Introduction localisée** : "Votre plombier intervient à [Zone] en 30 minutes..."
- **Services disponibles** dans cette zone (liens internes)
- **Spécificités locales** (type de bâti, problèmes courants dans le quartier)
- **Témoignage client** de cette zone
- **Temps d'intervention** estimé pour cette zone
- **CTA appel**

**Consignes SEO zones :**

- Chaque page doit avoir un contenu unique (pas de copier-coller entre zones)
- Mentionner des rues, quartiers, repères locaux connus
- Intégrer le code postal quand pertinent

**Arrondissements Lyon :**
- Lyon 1 (69001) — Pentes Croix-Rousse, Terreaux
- Lyon 2 (69002) — Presqu'île, Bellecour, Confluences
- Lyon 3 (69003) — Part-Dieu, Villette, Montchat
- Lyon 4 (69004) — Croix-Rousse
- Lyon 5 (69005) — Vieux Lyon, Fourvière, Point du Jour
- Lyon 6 (69006) — Parc Tête d'Or, Brotteaux, Foch
- Lyon 7 (69007) — Jean Macé, Gerland, Guillotière
- Lyon 8 (69008) — Monplaisir, Mermoz, Grand Trou
- Lyon 9 (69009) — Vaise, Gorge de Loup, Duchère

**Villes périphériques :**
- Villeurbanne (69100) — Gratte-Ciel, Tonkin, Charpennes
- Bron (69500)
- Caluire-et-Cuire (69300)
- Vénissieux (69200)
- Décines-Charpieu (69150)

---

### 3.4 Blog SEO (×5 articles)

**Objectif :** Capter du trafic informationnel et le convertir en appels.

Chaque article :

- **H1 optimisé** pour la requête cible
- **Introduction** : problème courant, empathie
- **Contenu utile** : conseils pratiques, étapes à suivre
- **Quand appeler un pro** : section qui redirige vers l'appel
- **CTA** : "Si le problème persiste, appelez-nous"
- **Liens internes** vers les pages services correspondantes
- **Schema.org** : Article + HowTo si applicable

**Articles à créer :**

| Slug | H1 | Requête cible |
|------|-----|---------------|
| que-faire-fuite-eau | Que faire en cas de fuite d'eau ? Guide complet | fuite d'eau que faire |
| comment-couper-eau-appartement | Comment couper l'eau dans un appartement ? | couper eau appartement |
| comment-deboucher-evier | Comment déboucher un évier ? 5 méthodes efficaces | déboucher évier |
| pourquoi-chauffe-eau-fuit | Pourquoi mon chauffe-eau fuit ? Causes et solutions | chauffe-eau fuit |
| wc-bouche-que-faire | WC bouché : que faire ? Solutions rapides | wc bouché que faire |

---

## PHASE 4 — SEO technique

### Balises obligatoires (dans BaseLayout.astro)

Chaque page doit avoir :

```html
<title>{title}</title>
<meta name="description" content="{description}" />
<link rel="canonical" href="{canonicalUrl}" />
<meta name="robots" content="index, follow" />

<!-- Open Graph -->
<meta property="og:title" content="{title}" />
<meta property="og:description" content="{description}" />
<meta property="og:type" content="website" />
<meta property="og:url" content="{canonicalUrl}" />
<meta property="og:locale" content="fr_FR" />

<!-- Géolocalisation -->
<meta name="geo.region" content="FR-69" />
<meta name="geo.placename" content="Lyon" />
```

### Schema.org (données structurées)

**Sur toutes les pages — LocalBusiness :**

```json
{
  "@context": "https://schema.org",
  "@type": "Plumber",
  "name": "[NOM ENTREPRISE récupéré du site]",
  "telephone": "[NUMÉRO récupéré du site]",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Lyon",
    "addressRegion": "Auvergne-Rhône-Alpes",
    "postalCode": "69000",
    "addressCountry": "FR"
  },
  "areaServed": ["Lyon", "Villeurbanne", "Bron", "Caluire-et-Cuire", "Vénissieux", "Décines-Charpieu"],
  "openingHours": "Mo-Su 00:00-23:59",
  "priceRange": "€€",
  "image": "[URL logo]",
  "url": "[URL site]"
}
```

**Sur la page d'accueil et les pages services — FAQPage :**

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "...",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "..."
      }
    }
  ]
}
```

**Sur les articles blog — Article + HowTo :**

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "...",
  "author": { "@type": "Organization", "name": "[NOM ENTREPRISE]" },
  "datePublished": "...",
  "publisher": { "@type": "Organization", "name": "[NOM ENTREPRISE]" }
}
```

### Sitemap XML

Générer automatiquement via Astro un sitemap.xml incluant toutes les pages.

### Robots.txt

```
User-agent: *
Allow: /
Sitemap: https://lyon.plomberie-roche.fr/sitemap.xml
```

---

## PHASE 5 — Optimisation Performance & Mobile

### Performance

- **Score Lighthouse ≥ 90** sur toutes les catégories
- **Pas de JavaScript inutile** — Astro est parfait pour ça, composants statiques par défaut
- **Images optimisées** : format WebP, lazy loading, dimensions explicites
- **Fonts** : preload des polices, font-display: swap
- **CSS** : inline critical CSS, purger le non utilisé

### Mobile (priorité absolue)

- **Bouton "Appeler" flottant** : toujours visible, position fixed en bas, couleur accent, gros touch target (min 48px)
- **Numéro cliquable** (`<a href="tel:..."`) partout
- **Navigation hamburger** simple et rapide
- **Texte lisible** sans zoom (16px minimum)
- **Touch targets** : minimum 44×44px
- **Pas de popup** ni d'éléments qui bloquent sur mobile

---

## PHASE 6 — Composants réutilisables détaillés

### CTACall.astro (le plus important)

```
Bouton flottant mobile :
- Position: fixed bottom 16px, centré
- Background: var(--color-accent)
- Texte blanc, gras : "📞 Appeler — [NUMÉRO]"
- Border-radius arrondi
- Box-shadow pour décoller du fond
- Z-index élevé
- Lien href="tel:[NUMÉRO]"
- Visible uniquement sur mobile (display none desktop)

Version header desktop :
- Dans le header sticky
- Même style mais intégré dans la barre
```

### HeroBanner.astro

```
- Background : image assombrie ou dégradé bleu profond
- H1 blanc, grande taille
- Sous-titre blanc/crème
- 2 boutons : CTA appel (accent) + Devis (outline blanc)
- Badges confiance en ligne en dessous
- Hauteur : 60-70vh sur desktop, 50vh mobile
```

### TrustBadges.astro

```
Ligne horizontale de badges :
- "24h/24 — 7j/7"
- "Intervention en 30 min"
- "Devis gratuit"
- "Garanti"
- "4.8/5 sur Google"
Chaque badge : icône + texte court
Style : fond léger, petites cartes ou pastilles
```

---

## CONSIGNES GÉNÉRALES POUR CLAUDE CODE

### Ce qu'il FAUT faire :

- ✅ Utiliser les skills Astro, Front-end et Marketing fournis
- ✅ Récupérer TOUTES les infos du site actuel (téléphone, adresse, nom, etc.)
- ✅ Produire du code propre, sémantique, accessible (ARIA quand nécessaire)
- ✅ Chaque page doit être complète et fonctionnelle, pas un template vide
- ✅ Le contenu texte doit être rédigé en français, optimisé SEO, naturel et convaincant
- ✅ Intégrer les données structurées schema.org sur chaque page
- ✅ Tout doit fonctionner sans JavaScript côté client quand possible (Astro islands)
- ✅ Générer le sitemap.xml et robots.txt
- ✅ Utiliser des données JSON pour les contenus répétitifs (services, zones, avis)

### Ce qu'il NE FAUT PAS faire :

- ❌ Mettre des textes placeholder "Lorem ipsum" — tout doit être rédigé
- ❌ Oublier le CTA appel sur une page
- ❌ Faire du copier-coller entre pages zones (contenu unique obligatoire)
- ❌ Utiliser des frameworks JS lourds côté client
- ❌ Mettre des images placeholder sans alt text descriptif
- ❌ Oublier les balises SEO (title, meta, canonical, schema.org)
- ❌ Négliger le mobile au profit du desktop

---

## ORDRE D'EXÉCUTION RECOMMANDÉ

1. **Crawl** du site actuel → extraction des données
2. **Setup** projet Astro + design system CSS
3. **Layout** de base + Header + Footer + CTACall
4. **Page d'accueil** complète
5. **Pages services** (6 pages)
6. **Pages zones** (14 pages)
7. **Blog** (5 articles)
8. **SEO technique** : sitemap, robots.txt, schema.org, vérification balises
9. **Test** : build Astro, vérification liens, responsive, Lighthouse

---

*Ce prompt doit être utilisé avec les skills Astro, Front-end et Marketing injectés dans le contexte de Claude Code.*
