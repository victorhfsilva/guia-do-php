# Autenticação e Autorização em PHP Web

## Introdução

Autenticação e autorização são componentes fundamentais de qualquer aplicação web que lida com informações de usuários. **Autenticação** verifica a identidade de um usuário (ex.: login), enquanto **autorização** determina o que um usuário autenticado pode fazer (ex.: permissões). Este guia fornecerá uma visão geral sobre como implementar autenticação e autorização em uma aplicação PHP.

## Autenticação Básica em PHP

### Estrutura de Pastas

Primeiro, organizamos a aplicação em uma estrutura de pastas simples:

```
/meu_projeto_auth
│
├── /app
│   ├── /controllers
│   │   └── AuthController.php
│   │   └── DashboardController.php
│   ├── /models
│   │   └── User.php
│   ├── /views
│   │   ├── auth
│   │   │   └── login.php
│   │   │   └── register.php
│   │   └── dashboard
│   │       └── index.php
│   ├── /core
│   │   └── App.php
│   │   └── Controller.php
│   └── /config
│       └── database.php
│
├── /public
│   ├── index.php
├── /vendor
│   └── autoload.php
├── composer.json
└── .htaccess
```

## Configurando o Banco de Dados

No arquivo `database.php`, configure a conexão com o banco de dados usando PDO:

```php
<?php
function getConnection() {
    $host = '127.0.0.1';
    $db   = 'auth_db';
    $user = 'root';
    $pass = '';
    $charset = 'utf8mb4';

    $dsn = "mysql:host=$host;dbname=$db;charset=$charset";
    $options = [
        PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
        PDO::ATTR_EMULATE_PREPARES   => false,
    ];

    try {
        return new PDO($dsn, $user, $pass, $options);
    } catch (\PDOException $e) {
        throw new \PDOException($e->getMessage(), (int)$e->getCode());
    }
}
```

## Criando o Modelo `User`

Este modelo lida com as operações relacionadas ao usuário, como registro, login e verificação de sessão.

```php
<?php

namespace App\Models;

use PDO;

class User {
    private $db;

    public function __construct() {
        $this->db = getConnection();
    }

    public function register($name, $email, $password) {
        $passwordHash = password_hash($password, PASSWORD_BCRYPT);
        $stmt = $this->db->prepare("INSERT INTO users (name, email, password) VALUES (:name, :email, :password)");
        return $stmt->execute([
            'name' => $name,
            'email' => $email,
            'password' => $passwordHash
        ]);
    }

    public function login($email, $password) {
        $stmt = $this->db->prepare("SELECT * FROM users WHERE email = :email");
        $stmt->execute(['email' => $email]);
        $user = $stmt->fetch();

        if ($user && password_verify($password, $user['password'])) {
            $_SESSION['user_id'] = $user['id'];
            return true;
        }

        return false;
    }

    public function isLoggedIn() {
        return isset($_SESSION['user_id']);
    }

    public function logout() {
        session_unset();
        session_destroy();
    }
}
```

## Criando o Controlador de Autenticação

O `AuthController` lida com o processo de login e registro.

```php
<?php

namespace App\Controllers;

use App\Core\Controller;
use App\Models\User;

class AuthController extends Controller {

    public function login() {
        if ($_SERVER['REQUEST_METHOD'] == 'POST') {
            $user = new User();
            if ($user->login($_POST['email'], $_POST['password'])) {
                header('Location: /dashboard');
                exit();
            } else {
                $this->view('auth/login', ['error' => 'Credenciais inválidas']);
                return;
            }
        }
        $this->view('auth/login');
    }

    public function register() {
        if ($_SERVER['REQUEST_METHOD'] == 'POST') {
            $user = new User();
            if ($user->register($_POST['name'], $_POST['email'], $_POST['password'])) {
                header('Location: /login');
                exit();
            } else {
                $this->view('auth/register', ['error' => 'Erro no registro']);
                return;
            }
        }
        $this->view('auth/register');
    }

    public function logout() {
        $user = new User();
        $user->logout();
        header('Location: /login');
        exit();
    }
}
```

### Criando as Páginas de Login e Registro

- **Login (`login.php`):**

```php
<h2>Login</h2>
<?php if (isset($data['error'])): ?>
    <p><?php echo $data['error']; ?></p>
<?php endif; ?>
<form action="/login" method="post">
    <input type="email" name="email" placeholder="Email">
    <input type="password" name="password" placeholder="Senha">
    <input type="submit" value="Entrar">
</form>
```

- **Registro (`register.php`):**

```php
<h2>Registro</h2>
<?php if (isset($data['error'])): ?>
    <p><?php echo $data['error']; ?></p>
<?php endif; ?>
<form action="/register" method="post">
    <input type="text" name="name" placeholder="Nome">
    <input type="email" name="email" placeholder="Email">
    <input type="password" name="password" placeholder="Senha">
    <input type="submit" value="Registrar">
</form>
```

## Protegendo Páginas com Autenticação

Você pode proteger uma página, como um painel de controle, verificando se o usuário está logado.

```php
<?php

namespace App\Controllers;

use App\Core\Controller;
use App\Models\User;

class DashboardController extends Controller {

    public function index() {
        $user = new User();
        if (!$user->isLoggedIn()) {
            header('Location: /login');
            exit();
        }

        $this->view('dashboard/index');
    }
}
```

- **Dashboard (`index.php`):**

```php
<h2>Bem-vindo ao Painel de Controle</h2>
<p>Você está logado.</p>
<a href="/logout">Sair</a>
```

## Autorização em PHP

A autorização verifica se um usuário autenticado tem permissão para realizar determinadas ações. Isso geralmente é feito verificando funções ou papéis atribuídos ao usuário.

### Adicionando Níveis de Acesso

No modelo `User`, você pode adicionar funções ou papéis para o usuário.

```php
<?php

class User {
    // ...

    public function getRole() {
        $stmt = $this->db->prepare("SELECT role FROM users WHERE id = :id");
        $stmt->execute(['id' => $_SESSION['user_id']]);
        return $stmt->fetchColumn();
    }

    public function hasRole($role) {
        return $this->getRole() === $role;
    }
}
```

### Exemplo de Verificação de Função

Você pode verificar a função do usuário para controlar o acesso a certas partes da aplicação.

```php
<?php

class DashboardController extends Controller {

    public function index() {
        $user = new User();
        if (!$user->isLoggedIn()) {
            header('Location: /login');
            exit();
        }

        if (!$user->hasRole('admin')) {
            echo "Acesso negado.";
            exit();
        }

        $this->view('dashboard/index');
    }
}
```
