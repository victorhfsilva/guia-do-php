# Sessões e Cookies em PHP

## Introdução

Sessões e cookies são dois mecanismos fundamentais em PHP para manter e gerenciar o estado entre as requisições HTTP, que por natureza são stateless (não mantêm o estado). Sessões permitem armazenar informações do usuário no servidor durante a navegação, enquanto cookies armazenam dados no navegador do usuário, que podem ser enviados de volta ao servidor em cada requisição subsequente.

## Sessões em PHP

###O que é uma Sessão?

- **Definição:** 
  - Uma sessão é uma forma de armazenar informações para serem usadas em várias páginas. Ao contrário dos cookies, os dados da sessão são armazenados no servidor, e apenas um identificador de sessão é armazenado no cliente (no navegador, como um cookie).

### Iniciando uma Sessão

- **Descrição:**
  - Antes de armazenar ou acessar dados de sessão, você precisa iniciar a sessão usando `session_start()`. Este comando deve ser o primeiro a ser executado na página, antes de qualquer saída HTML.

- **Exemplo:**
  ```php
  <?php
  session_start(); // Inicia a sessão

  $_SESSION['usuario'] = 'João';
  $_SESSION['email'] = 'joao@example.com';

  echo 'Sessão iniciada para o usuário: ' . $_SESSION['usuario'];
  ?>
  ```

### Acessando Dados da Sessão

- **Descrição:**
  - Após iniciar a sessão, você pode acessar qualquer dado armazenado nela usando a superglobal `$_SESSION`.

- **Exemplo:**
  ```php
  <?php
  session_start(); // Inicia a sessão

  echo 'Usuário: ' . $_SESSION['usuario'] . '<br>';
  echo 'Email: ' . $_SESSION['email'];
  ?>
  ```

### Encerrando uma Sessão

- **Descrição:**
  - Você pode destruir uma sessão (e seus dados) usando `session_destroy()`. Isso geralmente é feito quando o usuário se desconecta.

- **Exemplo:**
  ```php
  <?php
  session_start(); // Inicia a sessão

  session_unset(); // Remove todas as variáveis de sessão
  session_destroy(); // Destroi a sessão

  echo 'Sessão encerrada.';
  ?>
  ```

### Configurações da Sessão

- **Descrição:**
  - PHP permite configurar vários aspectos da sessão, como o tempo de expiração, o nome da sessão, e onde os dados da sessão são armazenados.

- **Exemplo:**
  ```php
  ini_set('session.gc_maxlifetime', 3600); // Tempo de expiração de 1 hora
  session_name('meu_sessao'); // Nome da sessão

  session_start(); // Inicia a sessão com as configurações personalizadas
  ```

## Cookies em PHP

### O que é um Cookie?

- **Definição:**
  - Um cookie é um pequeno arquivo de texto que o servidor pode armazenar no navegador do usuário. Cookies são enviados de volta ao servidor em cada requisição subsequente, permitindo que o servidor reconheça usuários e mantenha informações de estado.

### Criando um Cookie

- **Descrição:**
  - Para definir um cookie em PHP, usa-se a função `setcookie()`. Um cookie deve ser definido antes de qualquer saída HTML.

- **Sintaxe:**
  ```php
  setcookie(name, value, expire, path, domain, secure, httponly);
  ```

- **Exemplo:**
  ```php
  <?php
  $nome = 'nome_usuario';
  $valor = 'João';
  $expiracao = time() + (86400 * 30); // 30 dias
  setcookie($nome, $valor, $expiracao);

  echo 'Cookie definido!';
  ?>
  ```

### Acessando um Cookie

- **Descrição:**
  - Cookies podem ser acessados usando a superglobal `$_COOKIE`. Eles estarão disponíveis em todas as requisições subsequentes feitas ao servidor enquanto o cookie não expirar.

- **Exemplo:**
  ```php
  <?php
  if(isset($_COOKIE['nome_usuario'])) {
      echo 'Usuário: ' . $_COOKIE['nome_usuario'];
  } else {
      echo 'Cookie não definido.';
  }
  ?>
  ```

### Excluindo um Cookie

- **Descrição:**
  - Para excluir um cookie, basta definir sua data de expiração para um tempo no passado.

- **Exemplo:**
  ```php
  <?php
  setcookie('nome_usuario', '', time() - 3600); // Expira o cookie

  echo 'Cookie excluído!';
  ?>
  ```

### Opções Avançadas de Cookies

- **Descrição:**
  - Ao definir um cookie, você pode configurar opções adicionais, como o caminho (`path`), o domínio (`domain`), se o cookie deve ser enviado apenas em conexões seguras (`secure`), e se ele deve ser acessível apenas via HTTP (`httponly`).

- **Exemplo:**
  ```php
  setcookie(
      'nome_usuario',
      'João',
      time() + (86400 * 30), // 30 dias
      '/', // Caminho
      '.exemplo.com', // Domínio
      true, // Secure
      true  // HttpOnly
  );
  ```

## Comparação entre Sessões e Cookies

- **Armazenamento:**
  - **Sessões:** Armazenadas no servidor, com um identificador de sessão armazenado no cliente.
  - **Cookies:** Armazenados no navegador do cliente.

- **Segurança:**
  - **Sessões:** Mais seguras, pois os dados são armazenados no servidor.
  - **Cookies:** Menos seguros, pois os dados são armazenados no cliente e podem ser manipulados.

- **Tamanho:**
  - **Sessões:** Podem armazenar grandes quantidades de dados, limitados apenas pela capacidade do servidor.
  - **Cookies:** Limitados a aproximadamente 4KB de dados.

- **Persistência:**
  - **Sessões:** Por padrão, duram até o fechamento do navegador ou até que sejam explicitamente destruídas.
  - **Cookies:** Podem ser configurados para expirar após um certo período ou persistir indefinidamente.
