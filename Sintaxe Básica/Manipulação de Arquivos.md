# Manipulação de Arquivos em PHP

## Introdução

A manipulação de arquivos é uma tarefa comum em PHP, usada para ler, escrever, e modificar arquivos em um servidor. Além disso, você pode gerenciar diretórios, fazer upload de arquivos, e controlar as permissões de arquivos e diretórios. 

## Leitura e Escrita em Arquivos

### Abrindo Arquivos
- **Descrição:**
  - Antes de ler ou escrever em um arquivo, você precisa abri-lo usando a função `fopen()`.
  
- **Sintaxe:**
  ```php
  $arquivo = fopen("caminho/para/arquivo.txt", "modo");
  ```

- **Modos Comuns:**
  - `'r'`  : Abre o arquivo para leitura.
  - `'w'`  : Abre o arquivo para escrita (apaga o conteúdo existente).
  - `'a'`  : Abre o arquivo para escrita, mas preserva o conteúdo existente (adiciona ao final).
  - `'x'`  : Cria um novo arquivo para escrita; retorna `false` se o arquivo já existir.
  - `'r+'` : Abre o arquivo para leitura e escrita.

### Escrevendo em Arquivos
- **Descrição:**
  - Para escrever em um arquivo, use a função `fwrite()`.
  
- **Exemplo:**
  ```php
  $arquivo = fopen("caminho/para/arquivo.txt", "w");
  fwrite($arquivo, "Olá, mundo!");
  fclose($arquivo);
  ```

### Lendo Arquivos
- **Descrição:**
  - Para ler o conteúdo de um arquivo, use a função `fread()`, que lê uma quantidade específica de bytes, ou `fgets()`, que lê uma linha por vez.
  
- **Exemplo:**
  ```php
  $arquivo = fopen("caminho/para/arquivo.txt", "r");
  while ($linha = fgets($arquivo)) {
      echo $linha;
  }
  fclose($arquivo);
  ```

### Lendo Arquivos com `file_get_contents()`
- **Descrição:**
  - Para ler todo o conteúdo de um arquivo em uma única operação, você pode usar `file_get_contents()`.
  
- **Exemplo:**
  ```php
  $conteudo = file_get_contents("caminho/para/arquivo.txt");
  echo $conteudo;
  ```

### Escrevendo Arquivos com `file_put_contents()`
- **Descrição:**
  - Para escrever uma string diretamente em um arquivo, substituindo seu conteúdo, você pode usar `file_put_contents()`.
  
- **Exemplo:**
  ```php
  file_put_contents("caminho/para/arquivo.txt", "Novo conteúdo aqui.");
  ```

## Manipulação de Diretórios

### Criando Diretórios
- **Descrição:**
  - Para criar um novo diretório, use a função `mkdir()`.
  
- **Exemplo:**
  ```php
  mkdir("caminho/para/novo_diretorio");
  ```

### Verificando a Existência de um Diretório
- **Descrição:**
  - Para verificar se um diretório ou arquivo existe, use `file_exists()`.
  
- **Exemplo:**
  ```php
  if (file_exists("caminho/para/novo_diretorio")) {
      echo "O diretório existe.";
  } else {
      echo "O diretório não existe.";
  }
  ```

### Listando Arquivos em um Diretório
- **Descrição:**
  - Você pode listar os arquivos dentro de um diretório usando a função `scandir()`.
  
- **Exemplo:**
  ```php
  $arquivos = scandir("caminho/para/diretorio");
  foreach ($arquivos as $arquivo) {
      echo $arquivo . "<br>";
  }
  ```

### Excluindo Arquivos e Diretórios
- **Descrição:**
  - Use `unlink()` para excluir arquivos e `rmdir()` para excluir diretórios vazios.
  
- **Exemplo:**
  ```php
  unlink("caminho/para/arquivo.txt");
  rmdir("caminho/para/novo_diretorio");
  ```

## Upload de Arquivos

### Configurando o Formulário HTML
- **Descrição:**
  - Para permitir o upload de arquivos, o formulário HTML deve usar o método `POST` e incluir o atributo `enctype="multipart/form-data"`.
  
- **Exemplo:**
  ```html
  <form action="upload.php" method="POST" enctype="multipart/form-data">
      <input type="file" name="arquivo">
      <input type="submit" value="Enviar">
  </form>
  ```

### Processando o Upload em PHP
- **Descrição:**
  - No script PHP, você pode acessar o arquivo carregado através do array superglobal `$_FILES`.
  
- **Exemplo:**
  ```php
  if ($_FILES["arquivo"]["error"] == UPLOAD_ERR_OK) {
      $nome_temporario = $_FILES["arquivo"]["tmp_name"];
      $nome_arquivo = $_FILES["arquivo"]["name"];
      move_uploaded_file($nome_temporario, "uploads/" . $nome_arquivo);
      echo "Arquivo enviado com sucesso!";
  } else {
      echo "Erro no upload do arquivo.";
  }
  ```

### Verificando o Tipo de Arquivo e Tamanho
- **Descrição:**
  - É importante validar o tipo de arquivo e o tamanho do arquivo antes de movê-lo para o servidor.
  
- **Exemplo:**
  ```php
  $tipo_arquivo = $_FILES["arquivo"]["type"];
  $tamanho_arquivo = $_FILES["arquivo"]["size"];
  $tipos_permitidos = array("image/jpeg", "image/png", "application/pdf");

  if (in_array($tipo_arquivo, $tipos_permitidos) && $tamanho_arquivo <= 5000000) {
      move_uploaded_file($nome_temporario, "uploads/" . $nome_arquivo);
      echo "Arquivo enviado com sucesso!";
  } else {
      echo "Tipo de arquivo ou tamanho não permitido.";
  }
  ```

## Permissões de Arquivos

### Alterando Permissões de Arquivos
- **Descrição:**
  - Use `chmod()` para alterar as permissões de arquivos ou diretórios. As permissões são especificadas em notação octal.
  
- **Exemplo:**
  ```php
  chmod("caminho/para/arquivo.txt", 0755);
  ```
