# Programação Orientada a Objetos (OOP) em PHP

A Programação Orientada a Objetos (OOP) é um paradigma de programação que utiliza "objetos" e "classes" para criar modelos de conceitos do mundo real. PHP suporta OOP, permitindo que você escreva código modular, reutilizável e mais fácil de manter.

## Classes e Objetos

### Classes
- **Descrição:** Uma classe é um "molde" ou "blueprint" para criar objetos. Ela define propriedades (variáveis) e métodos (funções) que os objetos criados a partir dela terão.

- **Sintaxe:**
```php
class Pessoa {
    public $nome;
    public $idade;

    public function __construct($nome, $idade) {
        $this->nome = $nome;
        $this->idade = $idade;
    }

    public function apresentar() {
        return "Olá, eu sou " . $this->nome . " e tenho " . $this->idade . " anos.";
    }
}
```

### Objetos
- **Descrição:** Um objeto é uma instância de uma classe. Depois de criar uma classe, você pode criar vários objetos baseados nessa classe.

- **Exemplo:**
```php
$pessoa1 = new Pessoa("João", 30);
echo $pessoa1->apresentar(); // Output: Olá, eu sou João e tenho 30 anos.
```

## Tipagem em Classes PHP

A partir do PHP 7, você pode definir tipos de dados para propriedades, parâmetros e valores de retorno em classes. Isso ajuda a garantir que os dados manipulados pela classe sejam do tipo esperado, melhorando a robustez e a legibilidade do código.

### Tipagem de Propriedades

- **Descrição:** 
- Você pode definir o tipo de dado que uma propriedade de classe deve armazenar.

- **Exemplo:**
```php
class Produto {
    public string $nome;
    public float $preco;

    public function __construct(string $nome, float $preco) {
        $this->nome = $nome;
        $this->preco = $preco;
    }
}
```

### Tipagem de Parâmetros e Retorno

- **Descrição:** 
- Você pode definir o tipo de dado que um método aceita como parâmetro e o tipo de dado que ele deve retornar.

- **Exemplo:**
```php
class Calculadora {
    public function somar(int $a, int $b): int {
        return $a + $b;
    }
}

$calc = new Calculadora();
echo $calc->somar(5, 10); // Output: 15
```

### Tipos Nulos

- **Descrição:** 
- Para permitir que uma propriedade, parâmetro ou valor de retorno seja nulo, adicione `?` antes do tipo.

- **Exemplo:**
```php
class Usuario {
    public ?string $nome = null;

    public function setNome(?string $nome) {
        $this->nome = $nome;
    }
}

$usuario = new Usuario();
$usuario->setNome(null); // É permitido
```


## Herança

### Herança
- **Descrição:** Herança permite que uma classe (subclasse ou classe filha) herde propriedades e métodos de outra classe (superclasse ou classe pai). Isso promove a reutilização de código.

- **Sintaxe:**
```php
class Funcionario extends Pessoa {
    public $cargo;

    public function __construct($nome, $idade, $cargo) {
        parent::__construct($nome, $idade);
        $this->cargo = $cargo;
    }

    public function apresentar() {
        return parent::apresentar() . " Eu sou um " . $this->cargo . ".";
    }
}

$funcionario = new Funcionario("Maria", 25, "Desenvolvedora");
echo $funcionario->apresentar();
// Output: Olá, eu sou Maria e tenho 25 anos. Eu sou uma Desenvolvedora.
```

## Encapsulamento (private, protected, public)

### Modificadores de Acesso
- **Descrição:** Encapsulamento envolve a proteção de dados dentro de uma classe, controlando o acesso a eles usando modificadores de acesso:
- **`public`**: Propriedades ou métodos acessíveis de qualquer lugar.
- **`protected`**: Acessíveis apenas dentro da classe e por subclasses.
- **`private`**: Acessíveis apenas dentro da própria classe.

- **Exemplo:**
```php
class Produto {
    private $nome;
    protected $preco;

    public function __construct($nome, $preco) {
        $this->nome = $nome;
        $this->preco = $preco;
    }

    public function getNome() {
        return $this->nome;
    }

    protected function getPreco() {
        return $this->preco;
    }
}

class Eletronico extends Produto {
    public function detalhes() {
        return $this->getNome() . " custa " . $this->getPreco() . " reais.";
    }
}

$produto = new Eletronico("Smartphone", 1500);
echo $produto->detalhes(); // Output: Smartphone custa 1500 reais.
```

## Polimorfismo

### Polimorfismo
- **Descrição:** Polimorfismo permite que uma classe filha substitua métodos da classe pai. Isso permite que objetos de diferentes classes sejam tratados da mesma forma, mesmo que tenham implementações diferentes.

- **Exemplo:**
```php
class Animal {
    public function fazerSom() {
        return "Algum som";
    }
}

class Cachorro extends Animal {
    public function fazerSom() {
        return "Latido";
    }
}

class Gato extends Animal {
    public function fazerSom() {
        return "Miau";
    }
}

$animais = [new Cachorro(), new Gato()];
foreach ($animais as $animal) {
    echo $animal->fazerSom() . "<br>";
}
// Output: Latido
//         Miau
```

## Interfaces e Classes Abstratas

### Interfaces
- **Descrição:** Uma interface define métodos que uma classe deve implementar, sem fornecer a implementação desses métodos. É um contrato que as classes devem seguir.

- **Sintaxe:**
```php
interface Forma {
    public function calcularArea();
}

class Circulo implements Forma {
    private $raio;

    public function __construct($raio) {
        $this->raio = $raio;
    }

    public function calcularArea() {
        return pi() * pow($this->raio, 2);
    }
}

$circulo = new Circulo(5);
echo $circulo->calcularArea(); // Output: 78.539816339745
```

### Classes Abstratas
- **Descrição:** Uma classe abstrata pode conter métodos tanto implementados quanto não implementados. As classes filhas devem implementar os métodos abstratos.

- **Sintaxe:**
```php
abstract class Veiculo {
    protected $marca;

    public function __construct($marca) {
        $this->marca = $marca;
    }

    abstract public function acelerar();
    }

class Carro extends Veiculo {
    public function acelerar() {
        return "O carro da marca " . $this->marca . " está acelerando.";
    }
}

$carro = new Carro("Toyota");
echo $carro->acelerar(); // Output: O carro da marca Toyota está acelerando.
```

## Uso de `this` e `parent` em PHP

### `this`
- **Descrição:** 
- O `$this` é uma palavra-chave que referencia a instância atual da classe. Dentro de um método, você usa `$this` para acessar propriedades e métodos da própria instância da classe.

- **Exemplo:**
```php
class Pessoa {
    public $nome;

    public function setNome($nome) {
        $this->nome = $nome;
    }

    public function getNome() {
        return $this->nome;
    }
}

$pessoa = new Pessoa();
$pessoa->setNome("João");
echo $pessoa->getNome(); // Output: João
```

##### b. `parent`
- **Descrição:** 
- A palavra-chave `parent` é usada para acessar métodos e propriedades da classe pai (superclasse). Ela é especialmente útil em classes que estendem outras classes (herança).

- **Exemplo:**
```php
class Animal {
    public function fazerSom() {
        return "Algum som";
    }
}

class Cachorro extends Animal {
    public function fazerSom() {
        return parent::fazerSom() . " de cachorro";
    }
}

$cachorro = new Cachorro();
echo $cachorro->fazerSom(); // Output: Algum som de cachorro
```

- **Uso Comum:**
- **Chamar o Construtor da Classe Pai:** 
```php
class Pessoa {
    protected $nome;

    public function __construct($nome) {
        $this->nome = $nome;
    }
}

class Funcionario extends Pessoa {
protected $cargo;

public function __construct($nome, $cargo) {
    parent::__construct($nome);
    $this->cargo = $cargo;
}
}
```

## Traits

### Traits
- **Descrição:** Traits permitem reutilizar métodos em várias classes, evitando a repetição de código. São semelhantes a classes, mas não podem ser instanciadas.

- **Sintaxe:**
```php
trait Log {
    public function log($mensagem) {
        echo "[LOG]: " . $mensagem;
    }
}

class Usuario {
    use Log;

    public function criarUsuario($nome) {
        // Lógica para criar usuário
        $this->log("Usuário " . $nome . " criado.");
    }
}

$usuario = new Usuario();
$usuario->criarUsuario("João");
// Output: [LOG]: Usuário João criado.
```

## Namespaces

### Namespaces
- **Descrição:** Namespaces organizam classes e evitam conflitos de nomes, especialmente em projetos grandes ou quando se utiliza bibliotecas externas.

- **Sintaxe:**
```php
namespace App\Controllers;

class UsuarioController {
    public function index() {
        echo "Listando usuários.";
    }
}

// Utilizando a classe
$controller = new \App\Controllers\UsuarioController();
$controller->index(); // Output: Listando usuários.
```

Outra forma de utilizar o namespace é com use:

```php
use \App\Controllers\UsuarioController;

$controller = new UsuarioController();
$controller->index(); // Output: Listando usuários.
```

Ou,

```php
use \App\Controllers\UsuarioController as Controller;

$controller = new Controller();
$controller->index(); // Output: Listando usuários.
```

## Autoload

- **Descrição:** 
  - O autoload em PHP é uma técnica que permite carregar automaticamente as classes necessárias no momento em que elas são instanciadas, sem a necessidade de incluir manualmente cada arquivo de classe com `require` ou `include`. Isso facilita a organização e manutenção do código, especialmente em projetos grandes.

- **Função `spl_autoload_register()`:**
  - A função `spl_autoload_register()` é usada para registrar uma ou mais funções de autoload. Essas funções especificam como PHP deve localizar e carregar as classes automaticamente.

- **Exemplo Simples:**
```php
spl_autoload_register(function (string $className) {
    $path = str_replace('RootNameSpace', 'rootDir', $className) . '.php';
    $path = str_replace('\\', DIRECTORY_SEPARATOR, $path);

    $complete_path = __DIR__ . DIRECTORY_SEPARATOR . $path;

    if (file_exists($complete_path)) {
        require_once $completePath;
    }
});

use \RootNameSpace\{
    MinhaClasse
}

$objeto = new MinhaClasse(); // PHP automaticamente inclui '/rootDir/MinhaClasse.php'
```

