# Tratamento de Exceções em PHP

## Introdução

O tratamento de exceções é uma técnica que permite lidar de forma controlada com erros e condições inesperadas durante a execução de um script. Em PHP, as exceções oferecem uma maneira robusta de capturar e tratar esses erros sem interromper o fluxo normal da aplicação. 

## Conceito de Exceção

- **Exceção**: É um evento anômalo que ocorre durante a execução de um programa, sinalizando que algo deu errado. Quando uma exceção é lançada (ou "disparada"), o PHP tenta encontrar um bloco de código que possa capturá-la e tratá-la.

- **Fluxo de Trabalho**:
  1. **Lançar** uma exceção quando um erro é encontrado.
  2. **Capturar** a exceção e tratá-la adequadamente.
  3. **Continuar** a execução ou terminar o programa de forma controlada.

## Estrutura Básica do Tratamento de Exceções

### Blocos `try`, `catch` e `finally`

- **`try`**: Contém o código que pode lançar uma exceção.
- **`catch`**: Captura a exceção lançada e executa um bloco de código para tratá-la.
- **`finally`**: (Opcional) Executa um bloco de código independentemente de uma exceção ter sido lançada ou não. Geralmente usado para limpar recursos.

- **Sintaxe:**
  ```php
  try {
      // Código que pode lançar uma exceção
  } catch (Exception $e) {
      // Código que trata a exceção
  } finally {
      // Código que é sempre executado (opcional)
  }
  ```

- **Exemplo:**
  ```php
  try {
      $divisor = 0;
      if ($divisor == 0) {
          throw new Exception("Divisão por zero.");
      }
      $resultado = 10 / $divisor;
  } catch (Exception $e) {
      echo "Erro: " . $e->getMessage(); // Output: Erro: Divisão por zero.
  } finally {
      echo "Processo finalizado.";
  }
  ```

### Lançando Exceções com `throw`

- **Descrição:** 
  - O comando `throw` é usado para lançar uma exceção manualmente. Quando `throw` é executado, o script imediatamente sai do bloco `try` e entra no bloco `catch`.

- **Exemplo:**
  ```php
  function dividir($a, $b) {
      if ($b == 0) {
          throw new Exception("Divisão por zero não permitida.");
      }
      return $a / $b;
  }

  try {
      echo dividir(10, 0);
  } catch (Exception $e) {
      echo "Erro: " . $e->getMessage(); // Output: Erro: Divisão por zero não permitida.
  }
  ```

## Exceções Personalizadas

### Criando Classes de Exceções Personalizadas

- **Descrição:** 
  - Você pode criar suas próprias classes de exceção para representar erros específicos em sua aplicação. Essas classes herdam da classe `Exception` ou de outra classe de exceção existente.

- **Exemplo:**
  ```php
  class DivisaoPorZeroException extends Exception {}

  function dividir($a, $b) {
      if ($b == 0) {
          throw new DivisaoPorZeroException("Divisão por zero detectada.");
      }
      return $a / $b;
  }

  try {
      echo dividir(10, 0);
  } catch (DivisaoPorZeroException $e) {
      echo "Erro específico: " . $e->getMessage(); // Output: Erro específico: Divisão por zero detectada.
  }
  ```

### Capturando Múltiplas Exceções

- **Descrição:** 
  - Você pode capturar diferentes tipos de exceções usando múltiplos blocos `catch`. Isso permite tratar erros específicos de maneiras diferentes.

- **Exemplo:**
  ```php
  try {
      // Código que pode lançar diferentes tipos de exceção
  } catch (DivisaoPorZeroException $e) {
      echo "Erro de divisão: " . $e->getMessage();
  } catch (Exception $e) {
      echo "Erro geral: " . $e->getMessage();
  }
  ```

## A Classe `Exception`

### Métodos Úteis da Classe `Exception`

- **`getMessage()`**: Retorna a mensagem de erro associada à exceção.
- **`getCode()`**: Retorna o código de erro associado à exceção.
- **`getFile()`**: Retorna o nome do arquivo em que a exceção foi lançada.
- **`getLine()`**: Retorna o número da linha em que a exceção foi lançada.
- **`getTrace()`**: Retorna um array de backtrace da exceção.
- **`getTraceAsString()`**: Retorna uma string de backtrace da exceção.

- **Exemplo:**
  ```php
  try {
      throw new Exception("Um erro ocorreu", 500);
  } catch (Exception $e) {
      echo "Mensagem: " . $e->getMessage() . "<br>";
      echo "Código: " . $e->getCode() . "<br>";
      echo "Arquivo: " . $e->getFile() . "<br>";
      echo "Linha: " . $e->getLine() . "<br>";
  }
  ```

## Boas Práticas no Tratamento de Exceções

- **Não Use Exceções para Controle de Fluxo Regular:** Exceções devem ser usadas para tratar situações excepcionais, não para o fluxo normal do programa.
- **Forneça Mensagens de Erro Claras:** Ao lançar exceções, use mensagens de erro descritivas que ajudem a diagnosticar o problema.
- **Limpe Recursos no `finally`:** Use o bloco `finally` para liberar recursos como conexões de banco de dados, arquivos abertos, etc., garantindo que eles sejam liberados independentemente de uma exceção ter ocorrido ou não.
- **Evite o `catch` Genérico:** Sempre que possível, capture exceções específicas em vez de capturar todas as exceções com um `catch` genérico.
