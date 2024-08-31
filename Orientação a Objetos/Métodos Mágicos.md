# Métodos Mágicos em PHP

## Introdução

Métodos mágicos em PHP são métodos especiais que têm um comportamento específico quando definidos em uma classe. Eles são chamados automaticamente em certos contextos e começam com dois sublinhados (`__`). Estes métodos permitem que você modifique a forma como os objetos se comportam em certas situações, como quando são instanciados, convertidos para string ou acessados como arrays. 

## Principais Métodos Mágicos

### `__construct()`

- **Descrição:** 
  - É o construtor da classe. Este método é chamado automaticamente quando um objeto da classe é criado.

- **Sintaxe:**
  ```php
  class Pessoa {
      public $nome;

      public function __construct($nome) {
          $this->nome = $nome;
      }
  }

  $pessoa = new Pessoa("João");
  echo $pessoa->nome; // Output: João
  ```

### `__destruct()`

- **Descrição:** 
  - É o destrutor da classe. Este método é chamado automaticamente quando um objeto é destruído ou o script termina.

- **Sintaxe:**
  ```php
  class Pessoa {
      public $nome;

      public function __construct($nome) {
          $this->nome = $nome;
      }

      public function __destruct() {
          echo "O objeto de {$this->nome} foi destruído.";
      }
  }

  $pessoa = new Pessoa("João");
  // Quando o script termina ou $pessoa é destruído
  // Output: O objeto de João foi destruído.
  ```

### `__get($nome)`

- **Descrição:** 
  - Este método é chamado quando você tenta acessar uma propriedade que não existe ou que é inacessível (como `private` ou `protected`).

- **Sintaxe:**
  ```php
  class Pessoa {
      private $dados = [];

      public function __get($nome) {
          return $this->dados[$nome] ?? null;
      }

      public function __set($nome, $valor) {
          $this->dados[$nome] = $valor;
      }
  }

  $pessoa = new Pessoa();
  $pessoa->idade = 30;
  echo $pessoa->idade; // Output: 30
  ```

### `__set($nome, $valor)`

- **Descrição:** 
  - Este método é chamado quando você tenta definir o valor de uma propriedade que não existe ou que é inacessível.

- **Sintaxe:** (Ver exemplo acima com `__get`)

### `__isset($nome)`

- **Descrição:** 
  - Este método é chamado quando você usa `isset()` ou `empty()` em uma propriedade inacessível ou não existente.

- **Sintaxe:**
  ```php
  class Pessoa {
      private $dados = [];

      public function __isset($nome) {
          return isset($this->dados[$nome]);
      }

      public function __set($nome, $valor) {
          $this->dados[$nome] = $valor;
      }
  }

  $pessoa = new Pessoa();
  $pessoa->idade = 30;

  if (isset($pessoa->idade)) {
      echo "Idade está definida.";
  }
  ```

### `__unset($nome)`

- **Descrição:** 
  - Este método é chamado quando você usa `unset()` em uma propriedade inacessível ou não existente.

- **Sintaxe:**
  ```php
  class Pessoa {
      private $dados = [];

      public function __unset($nome) {
          unset($this->dados[$nome]);
      }

      public function __set($nome, $valor) {
          $this->dados[$nome] = $valor;
      }
  }

  $pessoa = new Pessoa();
  $pessoa->idade = 30;
  unset($pessoa->idade);
  ```

### `__call($nome, $argumentos)`

- **Descrição:** 
  - Este método é chamado quando você tenta chamar um método inacessível ou inexistente em um objeto.

- **Sintaxe:**
  ```php
  class Pessoa {
      public function __call($nome, $argumentos) {
          echo "Método '$nome' não existe. Argumentos: " . implode(', ', $argumentos);
      }
  }

  $pessoa = new Pessoa();
  $pessoa->andar("rápido", 10); // Output: Método 'andar' não existe. Argumentos: rápido, 10
  ```

### `__callStatic($nome, $argumentos)`

- **Descrição:** 
  - Este método é chamado quando você tenta chamar um método estático inacessível ou inexistente.

- **Sintaxe:**
  ```php
  class Pessoa {
      public static function __callStatic($nome, $argumentos) {
          echo "Método estático '$nome' não existe. Argumentos: " . implode(', ', $argumentos);
      }
  }

  Pessoa::correr("devagar", 5); // Output: Método estático 'correr' não existe. Argumentos: devagar, 5
  ```

### `__toString()`

- **Descrição:** 
  - Este método é chamado quando você tenta tratar um objeto como uma string (por exemplo, usando `echo`).

- **Sintaxe:**
  ```php
  class Pessoa {
      private $nome;

      public function __construct($nome) {
          $this->nome = $nome;
      }

      public function __toString() {
          return $this->nome;
      }
  }

  $pessoa = new Pessoa("João");
  echo $pessoa; // Output: João
  ```

### `__invoke()`

- **Descrição:** 
  - Este método é chamado quando você tenta chamar um objeto como se fosse uma função.

- **Sintaxe:**
  ```php
  class Saudacao {
      public function __invoke($nome) {
          return "Olá, " . $nome;
      }
  }

  $saudacao = new Saudacao();
  echo $saudacao("João"); // Output: Olá, João
  ```

### `__clone()`

- **Descrição:** 
  - Este método é chamado quando um objeto é clonado usando a palavra-chave `clone`.

- **Sintaxe:**
  ```php
  class Pessoa {
      public $nome;

      public function __construct($nome) {
          $this->nome = $nome;
      }

      public function __clone() {
          $this->nome = $this->nome . " (Clonado)";
      }
  }

  $pessoa1 = new Pessoa("João");
  $pessoa2 = clone $pessoa1;
  echo $pessoa2->nome; // Output: João (Clonado)
  ```

### `__sleep()` e `__wakeup()`

- **Descrição:**
  - `__sleep()` é chamado antes de serializar um objeto. Ele deve retornar um array com os nomes das propriedades a serem serializadas.
  - `__wakeup()` é chamado quando um objeto é desserializado, permitindo restaurar qualquer recurso que a classe possa precisar.

- **Exemplo de `__sleep()` e `__wakeup()`:**
  ```php
  class Conexao {
      private $conexao;

      public function __construct() {
          $this->conectar();
      }

      public function conectar() {
          $this->conexao = "Conectado";
      }

      public function __sleep() {
          return ['conexao']; // Apenas a conexão será serializada
      }

      public function __wakeup() {
          $this->conectar(); // Restaura a conexão ao desserializar
      }
  }
  ```

### `__autoload()` (Depreciado) e Autoloading com `spl_autoload_register()`

- **Descrição:** 
  - `__autoload()` era usado para carregar automaticamente classes que não foram incluídas. Ele foi depreciado em favor de `spl_autoload_register()`.

- **Exemplo de `spl_autoload_register()`:**
  ```php
  spl_autoload_register(function ($class_name) {
      include $class_name . '.php';
  });

  $obj = new MinhaClasse(); // Inclui automaticamente "MinhaClasse.php"
  ```
