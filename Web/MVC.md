# MVC em PHP

## Introdução ao MVC

**MVC (Model-View-Controller)** é um padrão de arquitetura de software amplamente utilizado no desenvolvimento de aplicações web. Ele separa a aplicação em três componentes principais: Model, View, e Controller. Essa separação facilita a manutenção, escalabilidade e organização do código.

- **Model (Modelo):** Representa a lógica de dados da aplicação. Ele manipula os dados e interage com o banco de dados.
- **View (Visão):** Responsável pela apresentação. Exibe os dados fornecidos pelo Controller de forma amigável ao usuário.
- **Controller (Controlador):** Atua como intermediário entre Model e View. Recebe as requisições do usuário, processa-as através do Model, e retorna a resposta via View.

## Estrutura Básica de Pastas para um Projeto MVC em PHP

Uma estrutura de pastas bem organizada é crucial para implementar o padrão MVC de forma eficiente. Abaixo está uma estrutura típica de um projeto PHP usando MVC:

```
/meu_projeto_mvc
│
├── /app
│   ├── /controllers
│   │   └── HomeController.php
│   │   └── UserController.php
│   ├── /models
│   │   └── User.php
│   ├── /views
│   │   ├── /home
│   │   │   └── index.php
│   │   ├── /user
│   │   │   └── profile.php
│   │   └── layouts
│   │       └── header.php
│   │       └── footer.php
│   ├── /core
│   │   └── App.php
│   │   └── Controller.php
│   │   └── Model.php
│   └── /config
│       └── config.php
│
├── /public
│   ├── index.php
│   ├── /css
│   │   └── styles.css
│   ├── /js
│   │   └── scripts.js
│   └── /images
│       └── logo.png
│
├── /vendor
│   └── autoload.php
│
├── composer.json
└── .htaccess
```

## Descrição das Pastas e Arquivos

#### `/app`

O diretório principal onde o código da aplicação reside.

- **/controllers:** Contém os controladores que lidam com as requisições e respostas.
  - **HomeController.php:** Controlador responsável pela página inicial.
  - **UserController.php:** Controlador que lida com funcionalidades relacionadas ao usuário.

- **/models:** Contém as classes que representam a lógica de negócios e a manipulação de dados.
  - **User.php:** Modelo que lida com os dados relacionados ao usuário, como interações com o banco de dados.

- **/views:** Contém os arquivos de visualização, responsáveis pela apresentação dos dados ao usuário.
  - **/home/index.php:** Visualização para a página inicial.
  - **/user/profile.php:** Visualização para o perfil do usuário.
  - **/layouts:** Contém layouts compartilhados, como cabeçalho e rodapé.

- **/core:** Contém classes centrais que ajudam a organizar a aplicação.
  - **App.php:** Manipula o roteamento e inicialização da aplicação.
  - **Controller.php:** Classe base para todos os controladores, fornecendo métodos comuns.
  - **Model.php:** Classe base para todos os modelos, fornecendo métodos para interação com o banco de dados.

- **/config:** Contém arquivos de configuração.
  - **config.php:** Configurações da aplicação, como conexões de banco de dados e configurações gerais.

#### `/public`

Este diretório é a raiz pública da aplicação. Todo o conteúdo acessível publicamente deve estar aqui.

- **index.php:** Ponto de entrada para a aplicação. Todas as requisições passam por este arquivo.
- **/css:** Contém arquivos de estilo CSS.
  - **styles.css:** Arquivo de estilo principal da aplicação.
- **/js:** Contém arquivos JavaScript.
  - **scripts.js:** Arquivo JavaScript principal da aplicação.
- **/images:** Contém imagens utilizadas na aplicação.
  - **logo.png:** Exemplo de logo usado na aplicação.

#### `/vendor`

Contém as dependências do Composer. É criado automaticamente quando você instala pacotes com o Composer.

####`composer.json`

Arquivo de configuração do Composer, onde são definidas as dependências do projeto.

#### `.htaccess`

Arquivo de configuração do Apache que pode ser usado para redirecionar URLs para `index.php`, permitindo URLs amigáveis.

## Implementação Básica do MVC em PHP

#### Roteamento Simples (`/core/App.php`)

O roteamento decide qual controlador e método chamar com base na URL.

```php
<?php

namespace App\Core;

class App {

    protected $controller = 'HomeController';
    protected $method = 'index';
    protected $params = [];

    public function __construct() {
        $url = $this->parseUrl();

        if(file_exists('../app/controllers/' . $url[0] . 'Controller.php')) {
            $this->controller = $url[0] . 'Controller';
            unset($url[0]);
        }

        require_once '../app/controllers/' . $this->controller . '.php';
        $this->controller = new $this->controller;

        if(isset($url[1])) {
            if(method_exists($this->controller, $url[1])) {
                $this->method = $url[1];
                unset($url[1]);
            }
        }

        $this->params = $url ? array_values($url) : [];

        call_user_func_array([$this->controller, $this->method], $this->params);
    }

    public function parseUrl() {
        if(isset($_GET['url'])) {
            return explode('/', filter_var(rtrim($_GET['url'], '/'), FILTER_SANITIZE_URL));
        }
    }
}
```

#### Controlador Base (`/core/Controller.php`)

Este é o controlador base do qual todos os controladores herdam.

```php
<?php

namespace App\Core;

class Controller {

    public function model($model) {
        require_once '../app/models/' . $model . '.php';
        return new $model();
    }

    public function view($view, $data = []) {
        require_once '../app/views/' . $view . '.php';
    }
}
```

#### Controlador de Exemplo (`/controllers/HomeController.php`)

```php
<?php

namespace App\Controllers;

use App\Core\Controller;

class HomeController extends Controller {

    public function index() {
        $this->view('home/index');
    }
}
```

#### Modelo de Exemplo (`/models/User.php`)

```php
<?php

namespace App\Models;

use PDO;

class User {
    private $db;

    public function __construct() {
        $this->db = new PDO('mysql:host=127.0.0.1;dbname=meu_banco', 'usuario', 'senha');
    }

    public function getAllUsers() {
        $stmt = $this->db->query("SELECT * FROM users");
        return $stmt->fetchAll(PDO::FETCH_ASSOC);
    }
}
```

#### Visualização de Exemplo (`/views/home/index.php`)

```php
<h1>Bem-vindo ao Meu Site</h1>
<p>Este é o conteúdo da página inicial.</p>
```

#### Ponto de Entrada (`/public/index.php`)

```php
<?php

require_once '../vendor/autoload.php';

use App\Core\App;

$app = new App();
```
