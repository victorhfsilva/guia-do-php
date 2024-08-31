# REST em PHP

## Introdução

REST (Representational State Transfer) é um estilo arquitetural amplamente utilizado para desenvolver APIs (Application Programming Interfaces) que permitem a comunicação entre diferentes sistemas. Uma API RESTful usa métodos HTTP como GET, POST, PUT, DELETE, entre outros, para realizar operações em recursos representados por URLs. 

## Estrutura Básica de uma API RESTful em PHP

### Configuração Inicial

Crie um novo projeto PHP com a seguinte estrutura de diretórios:

```
/meu_projeto_rest
│
├── /public
│   └── index.php
├── /src
│   ├── /controllers
│   │   └── UserController.php
│   ├── /config
│   │   └── database.php
└── composer.json
```

### Configuração do Servidor

Para desenvolvimento local, você pode usar o PHP embutido para servir o projeto:

```bash
php -S localhost:8000 -t public
```

### Configuração do Banco de Dados

No arquivo `database.php`, configure a conexão com o banco de dados usando PDO:

```php
<?php
function getConnection() {
    $host = '127.0.0.1';
    $db   = 'api_db';
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

## Criando um Controlador

### Criando o `UserController`

O controlador é responsável por lidar com as requisições HTTP e interagir com o modelo.

```php
<?php
namespace App\Controllers;

use PDO;

class UserController {

    private $db;

    public function __construct(PDO $db) {
        $this->db = $db;
    }

    public function getUsers() {
        $stmt = $this->db->query("SELECT * FROM users");
        $users = $stmt->fetchAll();
        echo json_encode($users);
    }

    public function getUser($id) {
        $stmt = $this->db->prepare("SELECT * FROM users WHERE id = :id");
        $stmt->execute(['id' => $id]);
        $user = $stmt->fetch();
        echo json_encode($user);
    }

    public function createUser() {
        $data = json_decode(file_get_contents("php://input"), true);
        $stmt = $this->db->prepare("INSERT INTO users (name, email) VALUES (:name, :email)");
        $stmt->execute(['name' => $data['name'], 'email' => $data['email']]);
        echo json_encode(['status' => 'User created']);
    }

    public function updateUser($id) {
        $data = json_decode(file_get_contents("php://input"), true);
        $stmt = $this->db->prepare("UPDATE users SET name = :name, email = :email WHERE id = :id");
        $stmt->execute(['name' => $data['name'], 'email' => $data['email'], 'id' => $id]);
        echo json_encode(['status' => 'User updated']);
    }

    public function deleteUser($id) {
        $stmt = $this->db->prepare("DELETE FROM users WHERE id = :id");
        $stmt->execute(['id' => $id]);
        echo json_encode(['status' => 'User deleted']);
    }
}
```
## Roteamento

No arquivo `index.php`, defina as rotas que correspondem às URLs para os métodos do controlador.

```php
<?php
require_once '../vendor/autoload.php';

use App\Controllers\UserController;

$method = $_SERVER['REQUEST_METHOD'];
$path = $_SERVER['REQUEST_URI'];
$db = getConnection();
$controller = new UserController($db);

switch ($path) {
    case '/users':
        if ($method == 'GET') {
            $controller->getUsers();
        } elseif ($method == 'POST') {
            $controller->createUser();
        }
        break;

    case preg_match('/\/users\/\d+/', $path) ? true : false:
        $id = basename($path);
        if ($method == 'GET') {
            $controller->getUser($id);
        } elseif ($method == 'PUT') {
            $controller->updateUser($id);
        } elseif ($method == 'DELETE') {
            $controller->deleteUser($id);
        }
        break;

    default:
        http_response_code(404);
        echo json_encode(['message' => 'Resource not found']);
        break;
}
```
