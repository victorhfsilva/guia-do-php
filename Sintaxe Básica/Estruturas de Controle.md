# Estruturas de Controle em PHP

## Introdução

As estruturas de controle são elementos fundamentais em PHP que permitem controlar o fluxo de execução de um script. Elas ajudam a tomar decisões, repetir blocos de código e manipular o fluxo de execução de acordo com as condições especificadas. 

## Condicionais

As estruturas condicionais permitem que o código seja executado ou ignorado com base em certas condições.

### `if`
- **Descrição:**
  - A estrutura `if` executa um bloco de código apenas se a condição especificada for avaliada como `true`.

- **Sintaxe:**
  ```php
  if (condição) {
      // Código a ser executado se a condição for verdadeira
  }
  ```

- **Exemplo:**
  ```php
  $idade = 20;

  if ($idade >= 18) {
      echo "Você é maior de idade.";
  }
  ```

### `else`
- **Descrição:**
  - A estrutura `else` define um bloco de código a ser executado se a condição do `if` for avaliada como `false`.

- **Sintaxe:**
  ```php
  if (condição) {
      // Código a ser executado se a condição for verdadeira
  } else {
      // Código a ser executado se a condição for falsa
  }
  ```

- **Exemplo:**
  ```php
  $idade = 16;

  if ($idade >= 18) {
      echo "Você é maior de idade.";
  } else {
      echo "Você é menor de idade.";
  }
  ```

### `elseif`
- **Descrição:**
  - A estrutura `elseif` permite testar múltiplas condições. Se a primeira condição for `false`, a próxima condição `elseif` será avaliada.

- **Sintaxe:**
  ```php
  if (condição1) {
      // Código a ser executado se condição1 for verdadeira
  } elseif (condição2) {
      // Código a ser executado se condição2 for verdadeira
  } else {
      // Código a ser executado se todas as condições forem falsas
  }
  ```

- **Exemplo:**
  ```php
  $nota = 85;

  if ($nota >= 90) {
      echo "Nota A";
  } elseif ($nota >= 80) {
      echo "Nota B";
  } else {
      echo "Nota C";
  }
  ```

### `switch`
- **Descrição:**
  - A estrutura `switch` é usada para comparar o valor de uma variável ou expressão com vários casos diferentes e executar o bloco de código correspondente.

- **Sintaxe:**
  ```php
  switch (expressão) {
      case valor1:
          // Código a ser executado se expressão for igual a valor1
          break;
      case valor2:
          // Código a ser executado se expressão for igual a valor2
          break;
      default:
          // Código a ser executado se expressão não corresponder a nenhum caso
  }
  ```

- **Exemplo:**
  ```php
  $dia = "segunda";

  switch ($dia) {
      case "segunda":
          echo "Hoje é segunda-feira.";
          break;
      case "terça":
          echo "Hoje é terça-feira.";
          break;
      case "quarta":
          echo "Hoje é quarta-feira.";
          break;
      default:
          echo "Hoje não é um dia útil.";
  }
  ```

## Loops

Loops permitem que você execute repetidamente um bloco de código enquanto uma condição for verdadeira ou para cada item em uma coleção.

### `for`
- **Descrição:**
  - O loop `for` é usado quando você sabe o número exato de vezes que deseja executar um bloco de código.

- **Sintaxe:**
  ```php
  for (inicialização; condição; incremento) {
      // Código a ser executado
  }
  ```

- **Exemplo:**
  ```php
  for ($i = 0; $i < 5; $i++) {
      echo "Número: $i<br>";
  }
  ```

### `while`
- **Descrição:**
  - O loop `while` executa um bloco de código repetidamente, enquanto uma condição for verdadeira.

- **Sintaxe:**
  ```php
  while (condição) {
      // Código a ser executado
  }
  ```

- **Exemplo:**
  ```php
  $i = 0;

  while ($i < 5) {
      echo "Número: $i<br>";
      $i++;
  }
  ```

### `do-while`
- **Descrição:**
  - O loop `do-while` é semelhante ao `while`, mas garante que o bloco de código seja executado pelo menos uma vez, pois a condição é verificada após a execução do bloco.

- **Sintaxe:**
  ```php
  do {
      // Código a ser executado
  } while (condição);
  ```

- **Exemplo:**
  ```php
  $i = 0;

  do {
      echo "Número: $i<br>";
      $i++;
  } while ($i < 5);
  ```

### `foreach`
- **Descrição:**
  - O loop `foreach` é usado especificamente para iterar sobre arrays. Para cada elemento do array, o código dentro do loop é executado.

- **Sintaxe:**
  ```php
  foreach ($array as $valor) {
      // Código a ser executado
  }

  // Ou com chaves e valores
  foreach ($array as $chave => $valor) {
      // Código a ser executado
  }
  ```

- **Exemplo:**
  ```php
  $frutas = array("Maçã", "Banana", "Laranja");

  foreach ($frutas as $fruta) {
      echo "Fruta: $fruta<br>";
  }

  // Exemplo com chaves e valores
  $idades = array("João" => 25, "Maria" => 30, "Pedro" => 35);

  foreach ($idades as $nome => $idade) {
      echo "$nome tem $idade anos<br>";
  }
  ```