# Guide de developpeur Drupal pour Accessibilité web

#### Contenu 

 1. C'est quoi l'Accessibilité web ?
 2. Comment Drupal gere l'aspect d'Accessibilité 
 3. Les bonnes pratiques
 4. Accessibilité Testing
 

## C'est quoi l'Accessibilité web ?

L'accessibilité web c'est un ensemble des bonnes pratiques pour les développeurs et designers à mettre en place , dans le but de crée des sites web de haute qualité , et sans exclut les personnes âgées ou ayant des capacités diminuées à utiliser , comprendre , naviguer et interagir avec le web.

## Comment Drupal gere d'Accessibilité 

## Les bonnes pratiques

 ### pour les developpeurs back-end :

+ Utiliser * hook_form_alter * pour ajouter les tages *aria* aux elements des formulaires.

+ Changer ou supprimer le message des liens "read more" sur les teasers des nodes á l'aide de  *hook_link_alter* .

+ Ajouter les attributs *aria* aux blocs grace au module [Block ARIA Landmark Roles](https://www.drupal.org/project/block_aria_landmark_roles).

+ Fournir aux utilisateurs une outile pour changer la taille de texte , á l'aide de module [Text Resize](https://www.drupal.org/project/text_resize).   
+ Utiliser *Drupal.announce()* pour notifier les utilisateurs avec les "Lecteur d'Ecrans" les changements fait sur la page en AJAX ou JS .
+ Eviter le *Caputcha* le plus possible .
+ Ajouter un alt texte pour les images avec un texte qui décrit l'image .
+ Ameliorer l'affichage des messages d'erreurs , par exemple: 

``` [X]Le champs Nom est incorrecte ``` 

``` [✓]Le champs Nom doit contenaire que des lettres uniquement ```
> ### pour les developpeurs front-end :
+ Associer un label avec tout elements de form (input,select, textarea ..).

> ex:
```html


```
+ Identifier la langue de la page , specificment pour les sites multilangue.
+ Mettre en places les attributs *aria-* sur non-standard elements, ( Slider , caroussel , list block).
 Ex :

	```
	role="menuItem"
	aria-checked="true" (pour les formulaires)
	aria-disabled="false" (pour les formulaires)
	aria-expanded="true" (ex : toggle menu)
	aria-labelledby="label" (pour les formulaires)
	aria-describedby="idDedescirption" (tout les elements)
	aria-required="true " (pour les formulaires)
	aria-hidden="true" (tout les elements)
	aria-current="page" (lien de navigation)
	aria-pressed="true" (button pressed)
	```

+ Assurer que tout les elements interactive sont accessible par le clavier.
+ L'augmentation de la taille de texte ne doit pas impacter les autres elements .
+ Eviter le plus possible **display: none** et remplacer par **aria-hidden** :
> Ex : 
```html
<div class="text">
    <label id="tp1-label" for="first">First Name:</label>
    <input type="text" id="first" name="first" size="20"
           aria-labelledby="tp1-label"
           aria-describedby="tp1"
           aria-required="false" />
    <div id="tp1" class="tooltip"
         role="tooltip"
         aria-hidden="true">Your first name is optional</div>
</div>
```

> Et en css : ( n'est supporter sur IE9)

```css
div[aria-hidden="true"] {display:none;}
div[aria-hidden="false"] {display:block;}
```

## Accessibilité Testing

[A11y.css](https://github.com/ffoodd/a11y.css)  : L’objectif de ce fichier CSS est d’alerter l’intégrateur sur les erreurs et risques potentiels dans le code .

[A11y Checker](https://muhnad.github.io/a11y-checker/)  : une biblio Js qui aide a detecter la none-conformité aux regles de WCAG.

[Gulp Accessibility ](https://github.com/yargalot/gulp-accessibility)  : une extension gulp qui permet de sigaler les elements qui respect pas les norme d'accissibilité .


