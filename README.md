# Investir en Espagne

Guide complet + simulateur d'investissement pour les Français qui achètent un bien immobilier en Espagne. Site statique à fichier unique, sans backend ni build.

## Les 3 versions du simulateur (test utilisateurs)

Le simulateur existe en trois interfaces, sélectionnables par le bandeau « Version testée » en haut de la page ou par un paramètre d'URL — pratique pour envoyer un lien différent à chaque testeur :

| Lien | Version | Principe |
|---|---|---|
| `?v=1` | **1 — actuelle** | Formulaire en 4 étapes repliables, rapport détaillé à droite |
| `?v=2` | **2 — tableau de bord vivant** | Curseurs, aucun bouton « Calculer », résultat recalculé en direct |
| `?v=3` | **3 — express + verdict** | 5 questions, puis le bilan et la cascade « d'où vient l'argent » en premier, détail replié |

Les trois partagent **le même moteur de calcul** : les contrôles des versions 2 et 3 écrivent dans les champs de la version 1 puis appellent `calculate()`. Un même projet donne donc exactement les mêmes chiffres dans les trois interfaces, et une correction de calcul les met à jour toutes.

## Structure

Tout tient dans **`index.html`** (HTML + CSS + JS inline, ~3 700 lignes) :

- **Accueil** — présentation, formulaire de capture d'intérêt (checklist PDF)
- **Le guide** — parcours en 10 étapes (préparation, NIE, financement, signature, fiscalité...), FAQ, glossaire
- **Le simulateur** — calcule les frais réels d'acquisition (ITP/IVA/AJD par région), le cash-flow locatif sur 3 scénarios de loyer, et une projection patrimoniale sur 30 ans (valeur du bien, capital amorti, cash-flow)
- **Mentions légales**

`og-image.png` est l'image utilisée pour l'aperçu au partage (Open Graph / Twitter Card).

## Lancer en local

Aucune dépendance, aucun build. Ouvrir `index.html` directement dans un navigateur, ou servir le dossier :

```bash
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

## État des langues

Le site est structuré en FR/EN/ES (objet `I18N` dans le JS), mais **seul le français est actif et maintenu** pour l'instant — les sélecteurs EN/ES sont grisés dans l'interface et le site force `lang=fr` au chargement. Le contenu EN/ES existe toujours dans le code mais n'est plus mis à jour.

## À configurer avant mise en ligne

Ces points sont volontairement laissés en placeholder dans le code (recherchables via `À PERSONNALISER` ou `YOUR-` dans `index.html`) :

- **`FORMSPREE_URL`** — capture des emails du formulaire d'intérêt. Tant qu'il n'est pas configuré, un filet de secours ouvre le client mail du visiteur au lieu de perdre le lead silencieusement.
- **`data-domain`** (balise Plausible, `<head>`) — nom de domaine réel une fois le site en ligne.
- **Mentions légales** — responsable de publication, hébergeur (section `#page-legal`), à compléter une fois le statut juridique (micro-entreprise / société existante) tranché.
- **`og:image`** — actuellement en URL relative (`og-image.png`), fonctionnera une fois le domaine fixé.

## Stack

HTML/CSS/JS vanilla, aucune dépendance runtime. Polices Google Fonts (Playfair Display + Inter) chargées via CDN, avec fallback Georgia/system-ui si indisponibles. Analytics via Plausible (script externe, désactivé tant que le domaine n'est pas renseigné).
