# Operadores em PHP

## Introdução

Operadores são símbolos que informam ao PHP para realizar operações específicas em valores ou variáveis. Eles são uma parte essencial da linguagem, permitindo desde simples cálculos matemáticos até operações complexas de comparação e lógica. 

## Tipos de Operadores em PHP

### Operadores Aritméticos

Os operadores aritméticos são usados para realizar operações matemáticas básicas, como adição, subtração, multiplicação, etc.

- **Adição (`+`)**: Soma dois valores.
  ```php
  $a = 10;
  $b = 20;
  $c = $a + $b; // $c será 30
  ```

- **Subtração (`-`)**: Subtrai o segundo valor do primeiro.
  ```php
  $c = $b - $a; // $c será 10
  ```

- **Multiplicação (`*`)**: Multiplica dois valores.
  ```php
  $d = $a * $b; // $d será 200
  ```

- **Divisão (`/`)**: Divide o primeiro valor pelo segundo.
  ```php
  $e = $b / $a; // $e será 2
  ```

- **Módulo (`%`)**: Retorna o restante da divisão de dois valores.
  ```php
  $f = $b % $a; // $f será 0
  ```

- **Exponenciação (`**`)**: Eleva o valor da esquerda à potência do valor da direita.
  ```php
  $g = $a ** 2; // $g será 100
  ```

### Operadores de Atribuição

Os operadores de atribuição são usados para atribuir valores às variáveis.

- **Atribuição Simples (`=`)**: Atribui o valor da direita à variável da esquerda.
  ```php
  $a = 10;
  ```

- **Atribuição Combinada**: Combina um operador aritmético com o operador de atribuição.
  - Adição e Atribuição (`+=`):
    ```php
    $a += 5; // Equivalente a $a = $a + 5
    ```
  - Subtração e Atribuição (`-=`):
    ```php
    $a -= 3; // Equivalente a $a = $a - 3
    ```
  - Multiplicação e Atribuição (`*=`):
    ```php
    $a *= 2; // Equivalente a $a = $a * 2
    ```
  - Divisão e Atribuição (`/=`):
    ```php
    $a /= 2; // Equivalente a $a = $a / 2
    ```
  - Módulo e Atribuição (`%=`):
    ```php
    $a %= 3; // Equivalente a $a = $a % 3
    ```

### Operadores de Comparação

Os operadores de comparação são usados para comparar dois valores. Eles retornam um valor booleano (`true` ou `false`).

- **Igual (`==`)**: Verifica se os valores são iguais.
  ```php
  $resultado = ($a == 10); // Retorna true se $a for igual a 10
  ```

- **Idêntico (`===`)**: Verifica se os valores e os tipos são iguais.
  ```php
  $resultado = ($a === 10); // Retorna true se $a for igual a 10 e também do tipo inteiro
  ```

- **Diferente (`!=` ou `<>`)**: Verifica se os valores são diferentes.
  ```php
  $resultado = ($a != 20); // Retorna true se $a não for igual a 20
  ```

- **Não Idêntico (`!==`)**: Verifica se os valores ou os tipos são diferentes.
  ```php
  $resultado = ($a !== "10"); // Retorna true se $a for diferente de "10" (string)
  ```

- **Maior que (`>`)**: Verifica se o valor da esquerda é maior que o da direita.
  ```php
  $resultado = ($a > 5); // Retorna true se $a for maior que 5
  ```

- **Menor que (`<`)**: Verifica se o valor da esquerda é menor que o da direita.
  ```php
  $resultado = ($a < 15); // Retorna true se $a for menor que 15
  ```

- **Maior ou Igual (`>=`)**: Verifica se o valor da esquerda é maior ou igual ao da direita.
  ```php
  $resultado = ($a >= 10); // Retorna true se $a for maior ou igual a 10
  ```

- **Menor ou Igual (`<=`)**: Verifica se o valor da esquerda é menor ou igual ao da direita.
  ```php
  $resultado = ($a <= 10); // Retorna true se $a for menor ou igual a 10
  ```

- **Spaceship (`<=>`)**: Compara dois valores. Retorna -1, 0 ou 1, se o valor da esquerda for menor, igual ou maior, respectivamente.
  ```php
  $resultado = $a <=> $b; // Retorna -1 se $a < $b, 0 se $a == $b, 1 se $a > $b
  ```

### Operadores de Incremento/Decremento
Estes operadores são usados para aumentar ou diminuir o valor de uma variável em 1.

- **Incremento (`++`)**:
  - **Pré-incremento:** Incrementa o valor antes de utilizá-lo.
    ```php
    ++$a; // $a é incrementado antes de ser usado
    ```
  - **Pós-incremento:** Incrementa o valor após utilizá-lo.
    ```php
    $a++; // $a é usado e depois incrementado
    ```

- **Decremento (`--`)**:
  - **Pré-decremento:** Decrementa o valor antes de utilizá-lo.
    ```php
    --$a; // $a é decrementado antes de ser usado
    ```
  - **Pós-decremento:** Decrementa o valor após utilizá-lo.
    ```php
    $a--; // $a é usado e depois decrementado
    ```

### Operadores Lógicos
Os operadores lógicos são usados para combinar expressões condicionais.

- **E (`&&` ou `and`)**: Retorna `true` se ambas as expressões forem verdadeiras.
  ```php
  $resultado = ($a == 10 && $b == 20); // Retorna true se ambos $a e $b forem verdadeiros
  ```

- **Ou (`||` ou `or`)**: Retorna `true` se pelo menos uma das expressões for verdadeira.
  ```php
  $resultado = ($a == 10 || $b == 30); // Retorna true se pelo menos um for verdadeiro
  ```

- **Xor (`xor`)**: Retorna `true` se uma, e apenas uma, das expressões for verdadeira.
  ```php
  $resultado = ($a == 10 xor $b == 30); // Retorna true se apenas um for verdadeiro
  ```

- **Não (`!`)**: Inverte o resultado da expressão.
  ```php
  $resultado = !($a == 10); // Retorna false se $a for igual a 10
  ```

### Operadores de Strings
Os operadores de strings são usados para manipular e combinar strings.

- **Concatenação (`.`)**: Combina duas strings.
  ```php
  $nome_completo = $nome . " " . $sobrenome; // Combina $nome e $sobrenome
  ```

- **Concatenação e Atribuição (`.=`)**: Concatena e atribui o resultado à variável.
  ```php
  $nome .= " Silva"; // Equivalente a $nome = $nome . " Silva"
  ```

#### Operadores de Arrays
Os operadores de arrays são usados para comparar arrays e combinar seus elementos.

- **União (`+`)**: Combina dois arrays, adicionando elementos do segundo array ao primeiro.
  ```php
  $array1 = array("a" => "apple", "b" => "banana");
  $array2 = array("c" => "cherry", "b" => "blueberry");
  $resultado = $array1 + $array2; // $resultado conterá "a" => "apple", "b" => "banana", "c" => "cherry"
  ```

- **Igualdade (`==`)**: Verifica se dois arrays têm os mesmos pares de chave/valor.
  ```php
  $resultado = ($array1 == $array2); // Retorna true se $array1 e $array2 tiverem os mesmos pares de chave/valor
  ```

- **Identidade (`===`)**: Verifica se dois arrays são idênticos, isto é, possuem os mesmos pares de chave/valor na mesma ordem e do mesmo tipo.
