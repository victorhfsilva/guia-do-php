# PHP em Formulários HTML

## Introdução

Formulários HTML são a principal forma de interação entre usuários e aplicações web. Eles permitem que os usuários enviem dados para o servidor, onde o PHP pode processá-los. 

## Estrutura Básica de um Formulário HTML

### Elementos Essenciais

- **`<form>`**: O elemento HTML que encapsula os controles de entrada.
- **`method`**: Define como os dados do formulário são enviados ao servidor (`POST`, `GET`, etc.).
- **`action`**: Define o URL para onde os dados do formulário serão enviados.

- **Exemplo Básico:**
  ```html
  <form action="processa_form.php" method="post">
      <label for="nome">Nome:</label>
      <input type="text" id="nome" name="nome">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email">
      <input type="submit" value="Enviar">
  </form>
  ```

## Processando Formulários com PHP

### Método `POST`

- **Descrição:**
  - O método `POST` envia dados ao servidor como parte do corpo da requisição. É adequado para enviar informações sensíveis, pois os dados não são expostos na URL.

- **Exemplo de Formulário:**
  ```html
  <form action="processa_post.php" method="post">
      <label for="nome">Nome:</label>
      <input type="text" id="nome" name="nome">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email">
      <input type="submit" value="Enviar">
  </form>
  ```

- **Processamento com PHP:**
  ```php
  <?php
  if ($_SERVER["REQUEST_METHOD"] == "POST") {
      $nome = htmlspecialchars($_POST['nome']);
      $email = htmlspecialchars($_POST['email']);

      echo "Nome: $nome<br>";
      echo "Email: $email<br>";
  }
  ?>
  ```

### Método `GET`

- **Descrição:**
  - O método `GET` anexa os dados do formulário à URL. É útil para consultas e quando você deseja que os dados sejam visíveis na URL. No entanto, não é recomendado para enviar informações sensíveis.

- **Exemplo de Formulário:**
  ```html
  <form action="processa_get.php" method="get">
      <label for="nome">Nome:</label>
      <input type="text" id="nome" name="nome">
      <label for="email">Email:</label>
      <input type="email" id="email" name="email">
      <input type="submit" value="Enviar">
  </form>
  ```

- **Processamento com PHP:**
  ```php
  <?php
  if ($_SERVER["REQUEST_METHOD"] == "GET") {
      $nome = htmlspecialchars($_GET['nome']);
      $email = htmlspecialchars($_GET['email']);

      echo "Nome: $nome<br>";
      echo "Email: $email<br>";
  }
  ?>
  ```
  
## Segurança e Validação de Dados

Independentemente do método utilizado (`POST`, `GET`), é crucial validar e sanitizar os dados de entrada para prevenir ataques como injeção de SQL e XSS.

### Saneamento de Dados

- **Exemplo de Saneamento:**
  ```php
  $nome = filter_var($_POST['nome'], FILTER_SANITIZE_STRING);
  $email = filter_var($_POST['email'], FILTER_VALIDATE_EMAIL);
  ```

### Validação de Dados

- **Exemplo de Validação:**
  ```php
  if (empty($nome) || !filter_var($email, FILTER_VALIDATE_EMAIL)) {
      echo "Dados inválidos!";
  } else {
      echo "Dados válidos!";
  }
  ```