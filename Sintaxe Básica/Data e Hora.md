# Manipulação de Data e Hora em PHP

## Introdução

Manipular data e hora é uma tarefa comum em muitas aplicações web, e PHP oferece diversas funções e classes para trabalhar com datas e horas de maneira eficaz. 

## Obter a Data e Hora Atuais

### Função `date()`

- **Descrição:** 
  - A função `date()` é usada para formatar a data e hora atuais de acordo com um formato específico.

- **Sintaxe:**
  ```php
  echo date("Y-m-d H:i:s"); // Output: 2024-08-26 12:34:56 (exemplo)
  ```

- **Exemplo:**
  ```php
  echo "Hoje é " . date("d/m/Y") . "<br>"; // Output: Hoje é 26/08/2024
  echo "Hora atual: " . date("H:i:s");     // Output: Hora atual: 12:34:56
  ```

### Função `time()`

- **Descrição:** 
  - A função `time()` retorna o timestamp Unix atual (o número de segundos desde 1º de janeiro de 1970 00:00:00 UTC).

- **Sintaxe:**
  ```php
  echo time(); // Output: 1724188496 (exemplo)
  ```

- **Uso Comum:**
  - Combinada com `date()`, você pode obter a data e hora a partir de um timestamp específico.
  
  ```php
  echo date("Y-m-d H:i:s", time()); // Output: 2024-08-26 12:34:56 (exemplo)
  ```

## Formatando Datas e Horas

### Especificadores de Formato com `date()`

- **Descrição:** 
  - A função `date()` aceita uma string de formato para definir como a data e hora devem ser exibidas.

- **Principais Especificadores:**
  - `Y`: Ano completo (ex: 2024)
  - `m`: Mês com dois dígitos (ex: 08)
  - `d`: Dia do mês com dois dígitos (ex: 26)
  - `H`: Hora em formato 24 horas (ex: 12)
  - `i`: Minutos com dois dígitos (ex: 34)
  - `s`: Segundos com dois dígitos (ex: 56)

- **Exemplo Completo:**
  ```php
  echo date("l, d F Y H:i:s"); // Output: Monday, 26 August 2024 12:34:56 (exemplo)
  ```

## Classe `DateTime`

- **Descrição:** 
  - A classe `DateTime` oferece uma forma orientada a objetos de manipular e formatar datas.

- **Exemplo:**
  ```php
  $data = new DateTime();
  echo $data->format('Y-m-d H:i:s'); // Output: 2024-08-26 12:34:56 (exemplo)
  ```

### Manipulação de Datas

##### Adicionando e Subtraindo Datas com `DateTime`

- **Descrição:** 
  - A classe `DateTime` facilita a adição e subtração de datas usando o método `modify()` ou `add()`/`sub()` com um objeto `DateInterval`.

- **Exemplo com `modify()`:**
  ```php
  $data = new DateTime();
  $data->modify('+1 day');
  echo $data->format('Y-m-d'); // Output: 2024-08-27 (exemplo)
  ```

- **Exemplo com `add()` e `sub()`:**
  ```php
  $data = new DateTime();
  $data->add(new DateInterval('P2W')); // Adiciona 2 semanas
  echo $data->format('Y-m-d'); // Output: 2024-09-09 (exemplo)

  $data->sub(new DateInterval('P1M')); // Subtrai 1 mês
  echo $data->format('Y-m-d'); // Output: 2024-08-09 (exemplo)
  ```

##### Diferença entre Datas

- **Descrição:** 
  - Você pode calcular a diferença entre duas datas usando o método `diff()` da classe `DateTime`, que retorna um objeto `DateInterval`.

- **Exemplo:**
  ```php
  $data1 = new DateTime('2024-08-26');
  $data2 = new DateTime('2024-09-10');
  $diferenca = $data1->diff($data2);

  echo $diferenca->days . " dias de diferença."; // Output: 15 dias de diferença
  ```

## Trabalhando com Fusos Horários

### Configurando o Fuso Horário

- **Descrição:** 
  - O PHP permite configurar o fuso horário padrão para toda a aplicação usando `date_default_timezone_set()`.

- **Exemplo:**
  ```php
  date_default_timezone_set('America/Sao_Paulo');
  echo date('Y-m-d H:i:s'); // Output: 2024-08-26 12:34:56 (exemplo em horário de São Paulo)
  ```

### Usando Fusos Horários com `DateTime`

- **Descrição:** 
  - A classe `DateTime` permite definir um fuso horário específico ao criar o objeto ou usar o método `setTimezone()`.

- **Exemplo:**
  ```php
  $data = new DateTime('now', new DateTimeZone('Europe/London'));
  echo $data->format('Y-m-d H:i:s'); // Output: 2024-08-26 16:34:56 (exemplo em horário de Londres)

  $data->setTimezone(new DateTimeZone('America/Sao_Paulo'));
  echo $data->format('Y-m-d H:i:s'); // Output: 2024-08-26 12:34:56 (exemplo em horário de São Paulo)
  ```

## Funções Úteis para Data e Hora

### `strtotime()`

- **Descrição:** 
  - A função `strtotime()` converte uma string de data e hora para um timestamp Unix.

- **Exemplo:**
  ```php
  $timestamp = strtotime('next Monday');
  echo date('Y-m-d', $timestamp); // Output: 2024-09-02 (exemplo)
  ```

### `mktime()`

- **Descrição:** 
  - A função `mktime()` cria um timestamp Unix para uma data específica.

- **Exemplo:**
  ```php
  $timestamp = mktime(0, 0, 0, 12, 25, 2024);
  echo date('Y-m-d', $timestamp); // Output: 2024-12-25
  ```

### `checkdate()`

- **Descrição:** 
  - A função `checkdate()` valida se uma data fornecida é válida.

- **Exemplo:**
  ```php
  if (checkdate(2, 29, 2024)) {
      echo "Data válida."; // Output: Data válida. (2024 é ano bissexto)
  } else {
      echo "Data inválida.";
  }
  ```