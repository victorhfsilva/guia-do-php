# Manipulação de Arrays em PHP

## Introdução

Arrays são uma parte fundamental da programação em PHP. Eles permitem armazenar múltiplos valores em uma única variável e manipulá-los de diversas formas. 

## Arrays Simples e Associativos

### Arrays Simples
- **Descrição:**
  - Um array simples, também conhecido como array indexado, é uma coleção de valores onde cada valor é acessado através de um índice numérico.
  
- **Sintaxe:**
  ```php
  $frutas = array("Maçã", "Banana", "Laranja");
  ```

- **Acessando Valores:**
  - Os valores em um array simples são acessados usando seu índice numérico.
  ```php
  echo $frutas[0]; // Output: Maçã
  ```

### Arrays Associativos
- **Descrição:**
  - Um array associativo é uma coleção de pares chave-valor, onde cada valor é acessado através de uma chave em vez de um índice numérico.
  
- **Sintaxe:**
  ```php
  $idades = array("João" => 25, "Maria" => 30, "Pedro" => 35);
  ```

- **Acessando Valores:**
  - Os valores em um array associativo são acessados usando sua chave correspondente.
  ```php
  echo $idades["João"]; // Output: 25
  ```

## Funções de Manipulação de Arrays

PHP oferece uma vasta gama de funções para manipulação de arrays. Aqui estão algumas das mais comuns e úteis:

### `array_merge()`
- **Descrição:**
  - Combina dois ou mais arrays em um único array.
  
- **Sintaxe:**
  ```php
  $array1 = array("Maçã", "Banana");
  $array2 = array("Laranja", "Uva");
  $resultado = array_merge($array1, $array2);
  print_r($resultado);
  // Output: Array ( [0] => Maçã [1] => Banana [2] => Laranja [3] => Uva )
  ```

### `array_diff()`
- **Descrição:**
  - Retorna um array contendo os valores do primeiro array que não estão presentes em qualquer um dos arrays subsequentes.
  
- **Sintaxe:**
  ```php
  $array1 = array("Maçã", "Banana", "Laranja");
  $array2 = array("Banana", "Uva");
  $resultado = array_diff($array1, $array2);
  print_r($resultado);
  // Output: Array ( [0] => Maçã [2] => Laranja )
  ```

### `array_map()`
- **Descrição:**
  - Aplica uma função callback a cada elemento de um array e retorna um novo array com os resultados.
  
- **Sintaxe:**
  ```php
  function dobrar($n) {
      return $n * 2;
  }

  $numeros = array(1, 2, 3, 4);
  $resultado = array_map("dobrar", $numeros);
  print_r($resultado);
  // Output: Array ( [0] => 2 [1] => 4 [2] => 6 [3] => 8 )
  ```

### `array_filter()`
- **Descrição:**
  - Filtra os elementos de um array usando uma função callback. Retorna um novo array contendo apenas os elementos para os quais a função retorna `true`.
  
- **Sintaxe:**
  ```php
  function maior_que_dois($n) {
      return $n > 2;
  }

  $numeros = array(1, 2, 3, 4);
  $resultado = array_filter($numeros, "maior_que_dois");
  print_r($resultado);
  // Output: Array ( [2] => 3 [3] => 4 )
  ```

### `array_reduce()`
- **Descrição:**
  - Itera sobre os elementos de um array, reduzindo-os a um único valor com base em uma função callback.
  
- **Sintaxe:**
  ```php
  function soma($carry, $item) {
      return $carry + $item;
  }

  $numeros = array(1, 2, 3, 4);
  $resultado = array_reduce($numeros, "soma");
  echo $resultado; // Output: 10
  ```

### `in_array()`
- **Descrição:**
  - Verifica se um valor existe em um array.
  
- **Sintaxe:**
  ```php
  $frutas = array("Maçã", "Banana", "Laranja");
  if (in_array("Banana", $frutas)) {
      echo "Banana está no array.";
  } else {
      echo "Banana não está no array.";
  }
  ```

### `array_keys()`
- **Descrição:**
  - Retorna todas as chaves de um array.
  
- **Sintaxe:**
  ```php
  $idades = array("João" => 25, "Maria" => 30, "Pedro" => 35);
  $chaves = array_keys($idades);
  print_r($chaves);
  // Output: Array ( [0] => João [1] => Maria [2] => Pedro )
  ```

### `array_values()`
- **Descrição:**
  - Retorna todos os valores de um array, ignorando as chaves.
  
- **Sintaxe:**
  ```php
  $idades = array("João" => 25, "Maria" => 30, "Pedro" => 35);
  $valores = array_values($idades);
  print_r($valores);
  // Output: Array ( [0] => 25 [1] => 30 [2] => 35 )
  ```

### `array_push()` e `array_pop()`
- **Descrição:**
  - `array_push()` adiciona um ou mais elementos ao final de um array.
  - `array_pop()` remove o último elemento de um array.
  
- **Sintaxe:**
  ```php
  $frutas = array("Maçã", "Banana");
  array_push($frutas, "Laranja");
  print_r($frutas); // Output: Array ( [0] => Maçã [1] => Banana [2] => Laranja )

  $ultima_fruta = array_pop($frutas);
  echo $ultima_fruta; // Output: Laranja
  print_r($frutas); // Output: Array ( [0] => Maçã [1] => Banana )
  ```

### `array_shift()` e `array_unshift()`
- **Descrição:**
  - `array_shift()` remove o primeiro elemento de um array.
  - `array_unshift()` adiciona um ou mais elementos ao início de um array.
  
- **Sintaxe:**
  ```php
  $frutas = array("Maçã", "Banana");
  array_unshift($frutas, "Laranja");
  print_r($frutas); // Output: Array ( [0] => Laranja [1] => Maçã [2] => Banana )

  $primeira_fruta = array_shift($frutas);
  echo $primeira_fruta; // Output: Laranja
  print_r($frutas); // Output: Array ( [0] => Maçã [1] => Banana )
  ```

## Iteração em Arrays

Iterar sobre arrays é uma tarefa comum em PHP. Aqui estão algumas maneiras de fazer isso:

### `foreach`
- **Descrição:**
  - O loop `foreach` é a forma mais comum de iterar sobre arrays em PHP. Ele percorre cada elemento do array, atribuindo a chave e o valor a variáveis para uso dentro do loop.
  
- **Sintaxe:**
  ```php
  $frutas = array("Maçã", "Banana", "Laranja");

  foreach ($frutas as $fruta) {
      echo "Fruta: $fruta<br>";
  }

  // Com chaves e valores
  $idades = array("João" => 25, "Maria" => 30, "Pedro" => 35);

  foreach ($idades as $nome => $idade) {
      echo "$nome tem $idade anos<br>";
  }
  ```

### `for`
- **Descrição:**
  - O loop `for` pode ser usado para iterar sobre arrays indexados. Você pode controlar manualmente o índice e acessar os elementos do array.
  
- **Sintaxe:**
  ```php
  $frutas = array("Maçã", "Banana", "Laranja");

  for ($i = 0; $i < count($frutas); $i++) {
      echo "Fruta: " . $frutas[$i] . "<br>";
  }
  ```