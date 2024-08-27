# Variáveis, Constantes e Tipos de Dados em PHP

## Introdução

PHP é uma linguagem de script que é amplamente utilizada para desenvolvimento web. Um dos aspectos fundamentais da programação em PHP é a compreensão de variáveis, constantes e tipos de dados. 

## Variáveis em PHP

- **O que é uma Variável?**
  - Em PHP, uma variável é um contêiner usado para armazenar dados que podem ser alterados durante a execução do script.

- **Sintaxe:**
  - As variáveis em PHP sempre começam com o símbolo `$`, seguido por um nome. Por exemplo:
    ```php
    $nome = "João";
    $idade = 30;
    $altura = 1.75;
    ```

- **Regras para Nomear Variáveis:**
  - Devem começar com uma letra ou sublinhado (_), não podem começar com um número.
  - Somente caracteres alfanuméricos e sublinhado são permitidos (A-Z, a-z, 0-9 e _).
  - São sensíveis a maiúsculas e minúsculas (`$nome` e `$Nome` são variáveis diferentes).

- **Atribuição de Valores:**
  - Os valores são atribuídos às variáveis usando o operador `=`. O valor à direita é atribuído à variável à esquerda.

## Constantes em PHP

- **O que é uma Constante?**
  - Constantes são identificadores para valores que não podem ser alterados durante a execução do script. Uma vez definida, o valor de uma constante não pode ser mudado.

- **Sintaxe:**
  - Para definir uma constante, usamos a função `define()`:
    ```php
    define("NOME", "João");
    define("IDADE", 30);
    define("ALTURA", 1.75);
    ```

- **Regras para Constantes:**
  - Diferente das variáveis, constantes não usam o símbolo `$`.
  - Por convenção, os nomes de constantes são escritos em maiúsculas.
  - As constantes são globais e podem ser acessadas de qualquer lugar no script.

## Tipos de Dados em PHP

PHP suporta vários tipos de dados, e é importante entender cada um deles para usar as variáveis e constantes de forma eficaz.

### Inteiros (Integer)
- **Descrição:**
  - Um número inteiro é um número sem ponto decimal. Pode ser positivo ou negativo.
  
- **Exemplo:**
  ```php
  $idade = 30;
  $ano = 2024;
  $temperatura = -10;
  ```

### Ponto Flutuante (Float ou Double)
- **Descrição:**
  - Um número float é um número com ponto decimal, usado para representar números fracionários ou com precisão decimal.

- **Exemplo:**
  ```php
  $altura = 1.75;
  $peso = 70.5;
  ```

### Strings
- **Descrição:**
  - Strings são sequências de caracteres, usadas para armazenar textos.

- **Exemplo:**
  ```php
  $nome = "João";
  $mensagem = "Olá, mundo!";
  ```

- **Concatenação de Strings:**
  - As strings podem ser concatenadas usando o operador `.`:
    ```php
    $nome_completo = $nome . " Silva";
    ```

### Booleanos (Boolean)
- **Descrição:**
  - Um valor booleano representa verdadeiro (`true`) ou falso (`false`). É comumente usado em operações lógicas e controle de fluxo.

- **Exemplo:**
  ```php
  $is_admin = true;
  $has_access = false;
  ```

### Arrays
- **Descrição:**
  - Arrays são coleções de dados, que podem armazenar múltiplos valores em uma única variável. Esses valores podem ser acessados através de chaves.

- **Tipos de Arrays:**
  - **Array Indexado:** Usam números como chaves.
    ```php
    $frutas = array("Maçã", "Banana", "Laranja");
    ```
  - **Array Associativo:** Usa strings como chaves.
    ```php
    $idade = array("João" => 30, "Maria" => 25, "Pedro" => 35);
    ```

- **Acessando Valores de um Array:**
  - Os valores de um array podem ser acessados utilizando a chave correspondente:
    ```php
    echo $frutas[0]; // Output: Maçã
    echo $idade["Maria"]; // Output: 25
    ```

### Objetos (Object)
- **Descrição:**
  - Um objeto é uma instância de uma classe, que pode conter tanto dados (propriedades) quanto funcionalidades (métodos).

- **Exemplo:**
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

  $pessoa = new Pessoa("João", 30);
  echo $pessoa->apresentar(); // Output: Olá, eu sou João e tenho 30 anos.
  ```

### NULL
- **Descrição:**
  - `NULL` é um tipo especial que representa uma variável sem valor.

- **Exemplo:**
  ```php
  $var = NULL;
  ```

### Conversão de Tipos (Type Casting)

- **Descrição:**
  - Em PHP, você pode converter explicitamente uma variável de um tipo para outro usando o casting.

- **Exemplo:**
  ```php
  $num_str = "123";
  $num_int = (int)$num_str; // Converte a string para inteiro
  ```

- **Funções de Conversão:**
  - `intval()`, `floatval()`, `strval()`, etc., também podem ser usadas para conversão de tipos.