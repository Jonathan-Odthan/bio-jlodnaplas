# JLodna Plas — Social Hub

Site statique (HTML, CSS, JavaScript pur) pour **https://bio.jlodna.com**.
La boutique officielle reste sur **https://www.jlodna.com** : ce projet n'y touche pas.

Aucune base de données, aucune variable d'environnement, aucune dépendance.

## Structure

```
jlodna-social-hub/
├── index.html      page unique (créole par défaut, français au choix)
├── style.css
├── script.js       langues, menu mobile, suivi des clics, analytique optionnelle
├── robots.txt
├── sitemap.xml
├── 404.html
├── vercel.json     en-têtes de sécurité et cache
├── README.md
└── assets/images/
    ├── logo.png      logo principal (fichier d'origine, non modifié)
    └── favicon.png   favicon (fichier d'origine, non modifié)
```

## Déploiement sur Vercel

1. **Préparer le dossier** : garder `jlodna-social-hub/` tel quel, avec `logo.png` et `favicon.png` dans `assets/images/`.
2. **GitHub** : créer un dépôt (ex. `jlodna-social-hub`), puis envoyer tous les fichiers à la racine du dépôt (`index.html` doit être à la racine).
3. **Importer dans Vercel** : *Add New → Project*, choisir le dépôt. Framework Preset : **Other**. Laisser *Build Command* et *Output Directory* vides.
4. **Déployer** : cliquer sur *Deploy*. Vercel donne une adresse `*.vercel.app` : l'ouvrir et tester d'abord là.
5. **Ajouter le domaine** : projet → *Settings → Domains* → ajouter `bio.jlodna.com`.
6. **DNS** : Vercel affiche les valeurs exactes à créer. Pour un sous-domaine, c'est en général **un seul enregistrement** de type `CNAME` pour le nom `bio`. Copier la valeur affichée par Vercel, sans en deviner une autre de mémoire.
7. **Vérifier** : attendre que Vercel indique « Valid Configuration » et que le certificat HTTPS soit émis, puis ouvrir `https://bio.jlodna.com`.
8. **Tester sur téléphone** : ouvrir le lien sur Android/iPhone et suivre la checklist ci-dessous.

### Sécurité DNS pour la boutique

- Ne supprimez et ne modifiez **aucun** enregistrement existant de `www` ni du domaine principal.
- Ajoutez uniquement l'enregistrement du sous-domaine `bio`.
- Les trois adresses (domaine principal, `www`, `bio`) peuvent pointer vers des déploiements différents.

## Modifier les liens plus tard

Les liens sont écrits directement dans `index.html` (ils fonctionnent même sans JavaScript). Rechercher l'ancienne adresse (Ctrl+F) et la remplacer **partout** : elle apparaît dans la carte du réseau, dans le pied de page et dans le bloc JSON-LD (`sameAs`).

| Élément | Adresse actuelle |
|---|---|
| WhatsApp | `https://wa.me/50955561461` (dans `index.html` **et** `WA_BASE` dans `script.js`) |
| Facebook | `https://www.facebook.com/jlodnaplas` |
| Instagram | `https://www.instagram.com/jlodna_plas/` |
| TikTok | `https://www.tiktok.com/@jlodna_plas` |
| Clapper | `https://clapperapp.com/jlodnaplas` |
| YouTube | `https://www.youtube.com/@jlodnaplas` |
| Pinterest | `https://pin.it/1A2hsiZkY` |
| Boutique | `https://www.jlodna.com` |

Les noms d'utilisateur affichés (`@jlodna_plas`, etc.) se changent dans les balises `<p class="handle">` de chaque carte.
Les textes se changent dans le dictionnaire `I18N` de `script.js` (créole `ht` et français `fr`), et le texte initial dans `index.html`.

## Analytique (désactivée par défaut)

Dans `script.js`, `GA_MEASUREMENT_ID = ""` : aucune analytique, aucun script externe, aucune erreur console.
Pour activer GA4, mettre un identifiant `G-XXXXXXXXXX`. Un bandeau de consentement s'affiche et Google Analytics ne se charge **qu'après acceptation**. Mettre alors à jour la phrase de confidentialité du pied de page.
Événements envoyés : `store_click`, `whatsapp_click`, `social_click`, `language_change`.

## Checklist : liens sociaux

À cocher sur ordinateur et sur téléphone :

- [ ] Facebook ouvre la page `jlodnaplas`
- [ ] Instagram ouvre `jlodna_plas`
- [ ] TikTok ouvre `@jlodna_plas`
- [ ] Clapper ouvre `jlodnaplas`
- [ ] YouTube ouvre `@jlodnaplas`
- [ ] Pinterest ouvre le lien `pin.it/1A2hsiZkY`
- [ ] WhatsApp ouvre une discussion avec le +509 5556 1461, message prérempli visible
- [ ] Les 3 boutons « boutique » (en-tête, héros, section boutique) et le lien du pied de page ouvrent `https://www.jlodna.com`
- [ ] Après passage en français, le message WhatsApp prérempli est en français
- [ ] Le menu mobile s'ouvre, se ferme (bouton, lien, touche Échap)
- [ ] Le choix de langue est conservé après rechargement

## Checklist SEO

- [ ] Titre, description, canonical (`https://bio.jlodna.com/`) présents
- [ ] Open Graph et Twitter Card présents
- [ ] JSON-LD (Organization + WebSite) valide : https://validator.schema.org
- [ ] `robots.txt` et `sitemap.xml` accessibles après déploiement
- [ ] Ajouter `bio.jlodna.com` dans Google Search Console et envoyer le sitemap
- [ ] Lighthouse mobile (Chrome DevTools) : performance, accessibilité, SEO

## Notes

- Une seule URL pour les deux langues : il n'y a donc volontairement pas de balises `hreflang`.
- `logo.png` et `favicon.png` pèsent chacun environ 700 Ko (1254 × 1254 px). Les fichiers d'origine n'ont pas été modifiés. Pour accélérer encore la page, vous pouvez en ajouter une version réduite (ex. 512 px) avec un outil comme Squoosh et la référencer à la place.
- Les icônes des réseaux sont de petits glyphes SVG simples intégrés à la page (aucune bibliothèque externe).
