# Jekyll Social
> Sélectionner les plates-formes de médias sociaux sur lesquelles vous voulez partager vos posts de blog Jekyll, directement à partir du front matter.

## L'idée
Si vous êtes auteur d'un blog, vous voudrez probablement partager vos posts avec autant de personnes que possible et vous utiliserez probablement les plates-formes de médias sociaux pour faire ça. Au lieu de faire ça à la main, vous pouvez tirer profit des services comme [IFTTT](https://ifttt.com/) pour automatiser ce processus, tout spécialement depuis que Jekyll est livré avec un flux RSS que vous pouvez utiliser pour communiquer avec des tiers.

Mais parfois vous voulez partager chaque post sur un ensemble différent de plates-formes, et c'est là où  **Jekyll Social** devient commode. Il génère un flux pour chaque plate-forme social en se basant sur l'information que vous insérez sur le front matter d'un post.

### Exemple
Disons que vous voulez le *post 1* sur Facebook, le *post 2* sur  Twitter et LinkedIn. Vous insérez ce qui suit dans le front matter du post : 

- *post 1*: `share: facebook`
- *post 2*: `share: twitter linkedin`

Si vous ne voulez pas partager un post, n'incluez pas la propriété `share`.

## Comment ça marche
Au lieu de servir le même fichier de flux sur tous les canaux différents IFTTT, **Jekyll Social** crée un flux individuel pour chaque plate-forme sociale pour laquelle vous pourrez ensuite servir son canal respectif IFTTT. Vous pouvez sélectionner les posts qui iront dans chaque flux en spécifiant la propriété `share` dans le front matter du post.

### Utiliser votre flux normal avec IFTTT
![Avant Jekyll Social](https://eduardoboucas.com/assets/posts/2015-04-28-sharing-jekyll-posts-on-social-media-using-front-matter-and-ifttt/jekyll-social-before.png)

### Utiliser Jekyll Social avec IFTTT
![Après Jekyll Social](https://eduardoboucas.com/assets/posts/2015-04-28-sharing-jekyll-posts-on-social-media-using-front-matter-and-ifttt/jekyll-social-after.png)

## Comment l'utiliser 
Regardez [ce post de blog](https://eduardoboucas.com/blog/2015/04/28/sharing-jekyll-posts-on-social-media-using-front-matter-and-ifttt.html) pour de l'information détaillée sur l'implémentation et comment régler l'ensemble.

## Formats personnalisés
Par défaut, toutes les plates-formes de médias sociaux partagent le même layout dans **Jekyll Social**, mais il est possible de créer un comportement personnalisé pour certaines plates-formes. 

### Twitter et hashtags
Par exemple, nous incluons un format de flux spécifique à Twitter qui a la possibilité de saisir les tags de posts et de les ajouter sous forme de hashtags dans un tweet. Le fichier  [_config.yml](https://github.com/ChristopheDucamp/jekyll-social/blob/master/_config.yml) inclus dans ce repo contient 3 variables que le plugin utilisera pour former vos tweets :

- `twitter_format` : Le format pour les tweets. Les balises  placeholders `@title`, `@url` et `@tags` seront remplacées automatiquement et respectivement par le titre du post, l'url et les tags (sous forme de hashtags). Vous pouvez ajouter du texte personnalisé comme *Blog post :*.
- `twitter_url_length` : Le nombre de caractères utilisé par Twitter pour encoder une URL. Vous ne devriez pas changer la valeur par défaut, à moins que Twitter ne change sa plateforme.
- `twitter_max_length` : La longueur maximum d'un tweet. Elle est actuellement de 140 caractères et je doute que cela changera, mais on ne sait jamais ! 

Si vous voulez utiliser les hashtags dans un post, vous devrez insérer `twitter--hashtags` dans la propriété  `share` du front matter. **NOTE :** Vous aurez encore besoin de l'identifiant `twitter`, par conséquent vous devriez avoir quelque chose qui ressemble à  `share: twitter twitter--hashtags`.

Si vous optez pour utiliser ce layout personnalisé, vous devrez configurer votre trigger IFTTT pour utiliser simplement l'ingrédient `{{EntryTitle}}`, comme titre du post. Les tags et URLs seront tous inclus dans le champ title du flux.
