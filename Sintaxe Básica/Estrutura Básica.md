# Estrutura Básica do PHP

## Introdução

PHP (Hypertext Preprocessor) é uma linguagem de script amplamente utilizada para desenvolvimento web. Ele é especialmente popular por sua facilidade de uso e capacidade de se integrar com HTML para criar páginas web dinâmicas. 

## Delimitadores de Código PHP

- **Delimitadores Padrão:** 
  - O código PHP é embutido em arquivos HTML ou usado separadamente em scripts. Para escrever código PHP, você deve envolvê-lo entre os delimitadores `<?php` e `?>`.
  
- **Exemplo:**
  ```php
  <?php
  echo "Olá, mundo!";
  ?>
  ```

- **Short Tags (Depreciado):**
  - Há também a opção de usar `<?` em vez de `<?php`, mas isso não é recomendado devido à falta de suporte consistente.
  - **Exemplo:**
    ```php
    <? echo "Olá, mundo!"; ?>
    ```

- **Nota:** 
  - É uma boa prática usar sempre `<?php` para garantir a compatibilidade com diferentes servidores e configurações.

## Comentários em PHP

Comentários são usados para explicar o código e são ignorados durante a execução.

- **Comentário de Linha Única:** 
  - Usa `//` ou `#`.
  ```php
  // Isso é um comentário de linha única
  # Este também é um comentário de linha única
  ```

- **Comentário de Múltiplas Linhas:** 
  - Usa `/* ... */`.
  ```php
  /* 
  Isso é um comentário de 
  múltiplas linhas 
  */
  ```
## Interação com HTML

PHP é frequentemente usado em conjunto com HTML para criar páginas web dinâmicas.

- **Exemplo de Arquivo PHP com HTML:**
  ```php
  <!DOCTYPE html>
  <html>
  <head>
      <title>Meu Site</title>
  </head>
  <body>
      <h1><?php echo "Bem-vindo ao meu site!"; ?></h1>
      <p><?php echo "Hoje é " . date("d/m/Y"); ?></p>
  </body>
  </html>
  ```
