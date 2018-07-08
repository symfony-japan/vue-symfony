2018/07/08 Symfony Meetup #21 ハンズオン
===

### 事前準備

Symfony4のプロジェクトを作成し、Vue.jsをインストールします
```
composer create-project symfony/website-skeleton vue-symfony
cd vue-symfony
yarn add --dev vue vue-loader@14 vue-template-compiler
```

### Controllerの作成

```
php bin/console make:controller Default
```

```.php
<?php

namespace App\Controller;

use Symfony\Component\Routing\Annotation\Route;
use Symfony\Bundle\FrameworkBundle\Controller\Controller;

class DefaultController extends Controller
{
   /**
    * @Route("/", name="default")
    */
   public function index()
   {
       return $this->render('default/index.html.twig');
   }
}
```

### テンプレートの編集

#### templates/default/index.html.twig

```.html
{% extends 'base.html.twig' %}
{% block body %}

   <div class="text-center">
       <h3>My Symfony 4 sample project</h3>

       <div class="jumbotron text-center">
           <example></example>
       </div>
   </div>

{% endblock %}
```

#### templates/base.html.twig

```.html
<!DOCTYPE html>
<html>
 <head>
     <meta charset="UTF-8">
     <title>{% block title %}Welcome!{% endblock %}</title>
     {% block stylesheets %}
       <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
     {% endblock %}
 </head>
 <body>
   <div id="app">
     {% block body %}{% endblock %}
   </div>
   {% block javascripts %}
     <script src="{{ asset('build/js/app.js') }}"></script>
   {% endblock %}
 </body>
</html>
```

### Webpack

#### webpack.config.js

```.js
var Encore = require('@symfony/webpack-encore'); Encore
  .setOutputPath('public/build/')
  .setPublicPath('/build')
  .cleanupOutputBeforeBuild()
  .enableSourceMaps(!Encore.isProduction())
  .addEntry('js/app', './assets/js/app.js')
  // .addStyleEntry('css/app', './assets/css/app.scss')
  // .enableSassLoader()
  // .autoProvidejQuery()


  // Enable Vue loader
  .enableVueLoader()
;

module.exports = Encore.getWebpackConfig();
```

### JavaScript

#### assets/js/app.js

```.js
// assets/js/app.js
import Vue from 'vue';

import Example from './components/Example'

/**
* Create a fresh Vue Application instance
*/
new Vue({
 el: '#app',
 components: {Example}
});
```

#### assets/js/components/Example.vue

```.vue
<template>
 <div>
   <p>This is an example of a new components in VueJs</p>
 </div>
</template>

<script>
 export default {
   name: 'example'
 }
</script>

<style scoped>

</style>
```

### ローカルサーバーの立ち上げ

```
php bin/console server:run
```

### Watch

```
yarn run encore dev --watch
```

open [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

### License

The MIT License (MIT). Please see [LICENSE](LICENSE) for more information.
