# Manipulação de Strings em PHP

## Introdução

Strings são uma parte fundamental de qualquer linguagem de programação, e em PHP, a manipulação de strings é extremamente poderosa e flexível.

## Concatenação de Strings

- **O que é Concatenação?**
  - Concatenação é o processo de unir duas ou mais strings para formar uma nova string.

- **Operador de Concatenação (`.`):**
  - Em PHP, a concatenação é feita usando o operador `.`.
  ```php
  $primeiro_nome = "João";
  $ultimo_nome = "Silva";
  $nome_completo = $primeiro_nome . " " . $ultimo_nome;
  echo $nome_completo; // Output: João Silva
  ```

- **Concatenação e Atribuição (`.=`):**
  - Você pode concatenar uma string a uma variável existente usando o operador `.=`.
  ```php
  $nome = "João";
  $nome .= " Silva";
  echo $nome; // Output: João Silva
  ```

## Funções para Manipulação de Strings

PHP oferece uma ampla gama de funções para manipular strings. Aqui estão algumas das mais utilizadas:

### `strlen()`
- **Descrição:**
  - Retorna o comprimento de uma string, ou seja, o número de caracteres.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  echo strlen($texto); // Output: 12
  ```

### `strpos()`
- **Descrição:**
  - Retorna a posição da primeira ocorrência de uma substring dentro de uma string. Se a substring não for encontrada, retorna `false`.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  $posicao = strpos($texto, "mundo");
  echo $posicao; // Output: 5
  ```

### `substr()`
- **Descrição:**
  - Retorna uma parte de uma string. Pode ser usada para extrair uma substring, começando em uma posição específica e, opcionalmente, com um comprimento definido.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  $parte = substr($texto, 5, 5);
  echo $parte; // Output: mundo
  ```

### `str_replace()`
- **Descrição:**
  - Substitui todas as ocorrências de uma substring por outra em uma string.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  $novo_texto = str_replace("mundo", "PHP", $texto);
  echo $novo_texto; // Output: Olá, PHP!
  ```

### `strtolower()` e `strtoupper()`
- **Descrição:**
  - `strtolower()` converte todos os caracteres de uma string para minúsculas, e `strtoupper()` converte todos para maiúsculas.
  
- **Exemplo:**
  ```php
  $texto = "Olá, Mundo!";
  echo strtolower($texto); // Output: olá, mundo!
  echo strtoupper($texto); // Output: OLÁ, MUNDO!
  ```

### `trim()`
- **Descrição:**
  - Remove espaços em branco (ou outros caracteres) do início e do fim de uma string.
  
- **Exemplo:**
  ```php
  $texto = "  Olá, mundo!  ";
  echo trim($texto); // Output: Olá, mundo!
  ```

### `explode()`
- **Descrição:**
  - Divide uma string em um array, usando um delimitador específico.
  
- **Exemplo:**
  ```php
  $texto = "João, Maria, Pedro";
  $nomes = explode(", ", $texto);
  print_r($nomes); // Output: Array ( [0] => João [1] => Maria [2] => Pedro )
  ```

### `implode()`
- **Descrição:**
  - Junta elementos de um array em uma string, usando um delimitador específico.
  
- **Exemplo:**
  ```php
  $nomes = array("João", "Maria", "Pedro");
  $texto = implode(", ", $nomes);
  echo $texto; // Output: João, Maria, Pedro
  ```

### `strrev()`
- **Descrição:**
  - Retorna a string com os caracteres invertidos.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  echo strrev($texto); // Output: !odnum ,álO
  ```

### `number_format()`
- **Descrição:**
  - Formata um número com milhares agrupados.
  
- **Exemplo:**
  ```php
  $numero = 1234567.89;
  echo number_format($numero, 2, ',', '.'); // Output: 1.234.567,89
  ```

## Expressões Regulares

Expressões regulares (regex) são padrões usados para buscar e substituir texto. PHP fornece funções poderosas para trabalhar com expressões regulares.

### `preg_match()`
- **Descrição:**
  - Verifica se uma string corresponde a um padrão.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  if (preg_match("/mundo/", $texto)) {
      echo "Padrão encontrado!";
  } else {
      echo "Padrão não encontrado.";
  }
  // Output: Padrão encontrado!
  ```

### `preg_match_all()`
- **Descrição:**
  - Encontra todas as correspondências para um padrão em uma string e as retorna em um array.
  
- **Exemplo:**
  ```php
  $texto = "A cor é azul. Azul é uma cor bonita.";
  preg_match_all("/azul/i", $texto, $matches);
  print_r($matches);
  // Output: Array ( [0] => Array ( [0] => azul [1] => Azul ) )
  ```

### `preg_replace()`
- **Descrição:**
  - Substitui todas as ocorrências de um padrão em uma string por uma nova string.
  
- **Exemplo:**
  ```php
  $texto = "Olá, mundo!";
  $novo_texto = preg_replace("/mundo/", "PHP", $texto);
  echo $novo_texto; // Output: Olá, PHP!
  ```

### `preg_split()`
- **Descrição:**
  - Divide uma string em um array com base em um padrão.
  
- **Exemplo:**
  ```php
  $texto = "um,dois;três:quatro";
  $partes = preg_split("/[,;:]/", $texto);
  print_r($partes);
  // Output: Array ( [0] => um [1] => dois [2] => três [3] => quatro )
  ```