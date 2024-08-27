# Funções em PHP

## Introdução

Funções são blocos de código que podem ser reutilizados em diferentes partes de um programa. Em PHP, você pode usar funções internas (built-in) fornecidas pela linguagem, criar suas próprias funções personalizadas, e até mesmo utilizar funções anônimas e callbacks. 

## Funções Internas (Built-in)

PHP vem com uma vasta biblioteca de funções internas que podem ser usadas para realizar diversas tarefas, desde manipulação de strings até operações matemáticas complexas.

### Exemplos de Funções Internas
- **`strlen()`**: Retorna o comprimento de uma string.
  ```php
  $texto = "Olá, mundo!";
  echo strlen($texto); // Output: 12
  ```

- **`array_merge()`**: Combina dois ou mais arrays.
  ```php
  $array1 = array("Maçã", "Banana");
  $array2 = array("Laranja", "Uva");
  $resultado = array_merge($array1, $array2);
  print_r($resultado); // Output: Array ( [0] => Maçã [1] => Banana [2] => Laranja [3] => Uva )
  ```

- **`date()`**: Formata uma data/hora local.
  ```php
  echo date("Y-m-d H:i:s"); // Output: 2024-08-26 12:34:56
  ```

- **`strpos()`**: Encontra a posição da primeira ocorrência de uma substring.
  ```php
  $texto = "Olá, mundo!";
  echo strpos($texto, "mundo"); // Output: 5
  ```

Essas são apenas algumas das muitas funções internas disponíveis em PHP. Elas ajudam a reduzir o tempo de desenvolvimento, fornecendo soluções prontas para problemas comuns.

## Definição e Uso de Funções Personalizadas

Você pode criar suas próprias funções em PHP para encapsular código que precisa ser reutilizado.

### Definindo Funções

- **Sintaxe:**
  ```php
  function nome_da_funcao($parametro1, $parametro2) {
      // Código a ser executado
      return $resultado;
  }
  ```

- **Exemplo:**
  ```php
  function soma($a, $b) {
      return $a + $b;
  }

  echo soma(5, 3); // Output: 8
  ```

### Funções com Parâmetros Opcionais

- **Descrição:**
  - Você pode definir parâmetros opcionais em suas funções, atribuindo valores padrão a eles.
  
- **Exemplo:**
  ```php
  function saudacao($nome = "Visitante") {
      return "Olá, " . $nome . "!";
  }

  echo saudacao(); // Output: Olá, Visitante!
  echo saudacao("João"); // Output: Olá, João!
  ```

### Funções que Não Retornam Valores

- **Descrição:**
  - Funções podem executar uma ação sem retornar um valor explicitamente.
  
- **Exemplo:**
  ```php
  function exibir_mensagem($mensagem) {
      echo $mensagem;
  }

  exibir_mensagem("Bem-vindo ao PHP!"); // Output: Bem-vindo ao PHP!
  ```

## Escopo de Variáveis e Globalização

O escopo de uma variável refere-se à área do script onde essa variável é acessível. Em PHP, o escopo das variáveis pode ser global ou local.

### Escopo Local
- **Descrição:**
  - Variáveis definidas dentro de uma função têm escopo local e não são acessíveis fora da função.
  
- **Exemplo:**
  ```php
  function exemplo() {
      $mensagem = "Olá, mundo!";
      echo $mensagem;
  }

  exemplo(); // Output: Olá, mundo!
  // echo $mensagem; // Isso causaria um erro porque $mensagem não é acessível fora da função.
  ```

### Escopo Global
- **Descrição:**
  - Variáveis globais são definidas fora de funções e estão disponíveis em todo o script. No entanto, dentro de uma função, você precisa usar a palavra-chave `global` para acessar essas variáveis.
  
- **Exemplo:**
  ```php
  $contador = 10;

  function incrementar() {
      global $contador;
      $contador++;
  }

  incrementar();
  echo $contador; // Output: 11
  ```

### `static` Variáveis
- **Descrição:**
  - Variáveis estáticas dentro de uma função mantêm seu valor entre chamadas da função.
  
- **Exemplo:**
  ```php
  function contador() {
      static $count = 0;
      $count++;
      echo $count;
  }

  contador(); // Output: 1
  contador(); // Output: 2
  contador(); // Output: 3
  ```

## Funções Anônimas e Callbacks

### Funções Anônimas
- **Descrição:**
  - Funções anônimas, também conhecidas como closures, são funções sem nome que podem ser armazenadas em variáveis ou passadas como parâmetros para outras funções.
  
- **Sintaxe:**
  ```php
  $saudacao = function($nome) {
      return "Olá, " . $nome . "!";
  };

  echo $saudacao("João"); // Output: Olá, João!
  ```

### Passando Funções Anônimas como Parâmetros
- **Descrição:**
  - Você pode passar funções anônimas como parâmetros para outras funções, o que é comum em operações como `array_map()` ou `usort()`.
  
- **Exemplo:**
  ```php
  $numeros = array(1, 2, 3, 4, 5);

  $dobrados = array_map(function($n) {
      return $n * 2;
  }, $numeros);

  print_r($dobrados); // Output: Array ( [0] => 2 [1] => 4 [2] => 6 [3] => 8 [4] => 10 )
  ```

### Callbacks
- **Descrição:**
  - Uma função de callback é uma função passada como argumento para outra função e que é chamada dentro dessa função.

- **Exemplo com `usort()`:**
  ```php
  $frutas = array("laranja", "banana", "maçã");

  usort($frutas, function($a, $b) {
      return strlen($a) - strlen($b);
  });

  print_r($frutas); // Output: Array ( [0] => maçã [1] => banana [2] => laranja )
  ```

## Tipagem de Funções

PHP suporta tipagem de funções, o que permite que você especifique o tipo de dados esperado para os parâmetros e o tipo de retorno de uma função. Isso ajuda a garantir que a função seja usada corretamente e pode evitar erros em tempo de execução.

### Tipagem de Parâmetros
- **Descrição:**
  - Você pode especificar o tipo de dado que um parâmetro de uma função deve receber. Se o tipo não corresponder, PHP tentará realizar uma conversão de tipo, ou gerará um erro.
  
- **Exemplo:**
  ```php
  function somar(int $a, int $b) {
      return $a + $b;
  }

  echo somar(5, 10); // Output: 15
  ```

  - Se você passar valores que não são inteiros, PHP tentará convertê-los:
  ```php
  echo somar(5, "10"); // Output: 15
  ```

### Tipagem de Retorno
- **Descrição:**
  - Você também pode especificar o tipo de dado que uma função deve retornar.
  
- **Exemplo:**
  ```php
  function somar(int $a, int $b): int {
      return $a + $b;
  }

  echo somar(5, 10); // Output: 15
  ```

- **Funções que Retornam Tipos Complexos:**
  - A tipagem de retorno pode ser aplicada a tipos complexos, como arrays, objetos, ou mesmo outras funções:
  ```php
  function get_nomes(): array {
      return ["João", "Maria", "Pedro"];
  }

  print_r(get_nomes()); // Output: Array ( [0] => João [1] => Maria [2] => Pedro )
  ```

### Tipos Nulos (`?` antes do tipo)
- **Descrição:**
  - Para permitir que um parâmetro ou valor de retorno seja nulo, use `?` antes do tipo.
  
- **Exemplo:**
  ```php
  function encontrar_usuario(int $id): ?string {
      $usuarios = [1 => "João", 2 => "Maria"];
      return $usuarios[$id] ?? null;
  }

  echo encontrar_usuario(1); // Output: João
  echo encontrar_usuario(3); // Output: (nada, pois retorna null)
  ```
