# Composer em PHP

## Introdução

Composer é uma ferramenta de gerenciamento de dependências para PHP. Ele permite que você declare as bibliotecas das quais seu projeto depende e as gerencia automaticamente (instalando, atualizando, etc.). Composer também cuida do autoloading de classes, facilitando a organização do código e a reutilização de bibliotecas de terceiros.

## Instalação do Composer

### Instalação Global

- **Windows:** 
  - Baixe e execute o instalador do Composer disponível no site oficial [getcomposer.org](https://getcomposer.org/download/).

- **macOS/Linux:** 
  - Abra o terminal e execute o seguinte comando:
    ```bash
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    sudo mv composer.phar /usr/local/bin/composer
    ```

- **Verificação da Instalação:**
  - Após a instalação, execute `composer --version` no terminal para verificar se o Composer foi instalado corretamente.

## Configuração Inicial de um Projeto com Composer

### Criando um Arquivo `composer.json`

- **Descrição:** 
  - O `composer.json` é o arquivo de configuração principal do Composer. Nele, você define as dependências do seu projeto, informações sobre o projeto (como nome, descrição, autor) e outras configurações.

#### Usando `composer init`

- **Descrição:** 
  - O comando `composer init` é uma maneira interativa de criar o arquivo `composer.json`. Ele guia você passo a passo, solicitando informações como o nome do projeto, descrição, autor, dependências, entre outros.

- **Comando:**
  ```bash
  composer init
  ```

- **Exemplo Básico de `composer.json`:**
  ```json
  {
      "name": "meuusuario/meuprojeto",
      "description": "Uma breve descrição do meu projeto",
      "require": {
          "monolog/monolog": "^2.0"
      },
      "autoload": {
          "psr-4": {
              "App\\": "src/"
          }
      }
  }
  ```

### Instalando Dependências

- **Descrição:** 
  - Após definir as dependências no `composer.json`, você pode instalar todas elas com o comando `composer install`.

- **Comando:**
  ```bash
  composer install
  ```
  
- **Resultado:** 
  - Este comando cria um diretório `vendor/` e baixa todas as dependências listadas em `composer.json`.

## Gerenciamento de Dependências

### Adicionando Dependências

- **Descrição:** 
  - Para adicionar uma nova dependência ao seu projeto, use o comando `composer require` seguido do nome do pacote.

- **Exemplo:**
  ```bash
  composer require guzzlehttp/guzzle
  ```

- **Resultado:** 
  - O Composer atualizará o `composer.json` para incluir a nova dependência e instalará o pacote.

### Atualizando Dependências

- **Descrição:** 
  - Para atualizar todas as dependências do seu projeto para as versões mais recentes permitidas pelo `composer.json`, use o comando `composer update`.

- **Comando:**
  ```bash
  composer update
  ```

- **Nota:**
  - Se você deseja atualizar uma única dependência, especifique o nome do pacote:
    ```bash
    composer update guzzlehttp/guzzle
    ```

### Removendo Dependências

- **Descrição:** 
  - Para remover uma dependência do seu projeto, use o comando `composer remove` seguido do nome do pacote.

- **Exemplo:**
  ```bash
  composer remove guzzlehttp/guzzle
  ```

## Autoloading

### Autoloading Automático

- **Descrição:** 
  - O Composer gera automaticamente um arquivo de autoload em `vendor/autoload.php`, que carrega todas as dependências e as classes do seu projeto.

- **Uso do Autoload:**
  ```php
  require 'vendor/autoload.php';

  // Agora você pode usar classes das dependências e do próprio projeto
  $logger = new Monolog\Logger('nome_do_canal');
  ```

### Autoloading Personalizado

- **Descrição:** 
  - No `composer.json`, você pode configurar o autoloading das suas próprias classes usando o padrão PSR-4.

- **Exemplo de Configuração PSR-4:**
  ```json
  "autoload": {
      "psr-4": {
          "Root\\NameSpace\\": "rootDir/"
      }
  }
  ```

- **Comando para Gerar Autoload:**
  - Após configurar o autoload, execute:
    ```bash
    composer dump-autoload
    ```


### Autoloading com `classmap`

- **Descrição:** 
  - O `classmap` é uma estratégia de autoloading em que o Composer escaneia os diretórios especificados e cria um mapa de todas as classes encontradas, independentemente da estrutura de diretórios ou do namespace.

- **Uso do `classmap`:**
  - `classmap` é útil quando você tem classes em diretórios que não seguem o padrão PSR-4 ou se você deseja incluir classes específicas.

- **Exemplo de Configuração `classmap`:**
  ```json
  "autoload": {
      "classmap": [
          "src/",
          "lib/",
          "app/specificClass.php"
      ]
  }
  ```

- **Comando para Gerar o `classmap`:**
  - Após configurar o `classmap`, execute:
    ```bash
    composer dump-autoload
    ```

- **Resultado:** 
  - O Composer irá escanear os diretórios e arquivos especificados e mapear todas as classes para autoloading, garantindo que possam ser carregadas automaticamente quando usadas.

### Autoloading com `files`

- **Descrição:** 
  - A estratégia `files` no autoload do Composer permite que você especifique arquivos PHP que devem ser incluídos automaticamente em cada requisição, independentemente de classes ou namespaces. Isso é útil para carregar arquivos que contêm funções globais, constantes ou outras configurações que precisam estar disponíveis em todo o projeto.

- **Uso do `files`:**
  - `files` é ideal para incluir automaticamente arquivos que não seguem a estrutura de classes, como arquivos de configuração, funções auxiliares, ou scripts que definem constantes.

- **Exemplo de Configuração `files`:**
  ```json
  "autoload": {
      "files": [
          "app/helpers.php",
          "app/constants.php"
      ]
  }
  ```

- **Comando para Gerar o Autoload:**
  - Após configurar o `files`, execute:
    ```bash
    composer dump-autoload
    ```

- **Resultado:** 
  - O Composer incluirá automaticamente os arquivos especificados na configuração `files` em cada requisição do seu projeto, garantindo que qualquer código nesses arquivos esteja disponível globalmente.
  - 
## Scripts do Composer

### Scripts Automatizados

- **Descrição:** 
  - O Composer permite definir scripts que são comandos a serem executados automaticamente em momentos específicos, como antes ou depois da instalação das dependências. Esses scripts podem ser usados para automatizar tarefas comuns no seu projeto, como executar migrações, rodar testes ou limpar o cache.

- **Exemplo de Script no `composer.json`:**
  ```json
  "scripts": {
      "post-install-cmd": [
          "php artisan migrate"
      ]
  }
  ```

- **Executando Scripts Manualmente:**
  - Você também pode executar scripts definidos manualmente:
    ```bash
    composer run-script post-install-cmd
    ```

### Chamando Scripts já definidos

- **Descrição:**
  - Você pode chamar scripts já definidos dentro de outro script utilizando o símbolo `@`. Isso é útil para criar scripts compostos ou para reutilizar scripts em diferentes contextos.

- **Exemplo:**
  ```json
  "scripts": {
      "clear-cache": "php artisan cache:clear",
      "migrate": "php artisan migrate",
      "deploy": [
          "@clear-cache",
          "@migrate",
          "php artisan config:cache"
      ]
  }
  ```
  - Neste exemplo, o script `deploy` executa os scripts `clear-cache` e `migrate`, seguidos por um comando adicional de cache.

- **Execução:**
  - Para executar o script `deploy` e, consequentemente, os scripts `clear-cache` e `migrate`, você pode usar:
    ```bash
    composer run-script deploy
    ```

### Adicionando Descrição aos Scripts

- **Descrição:**
  - Você pode adicionar descrições aos scripts no `composer.json`. Essas descrições aparecem quando você executa o comando `composer list`, facilitando a identificação e o propósito de cada script.

- **Exemplo de Script com Descrição:**
  ```json
  "scripts": {
      "clear-cache": {
          "description": "Limpa o cache da aplicação",
          "command": "php artisan cache:clear"
      },
      "migrate": {
          "description": "Executa as migrações de banco de dados",
          "command": "php artisan migrate"
      },
      "deploy": {
          "description": "Realiza o processo completo de deploy",
          "command": [
              "@clear-cache",
              "@migrate",
              "php artisan config:cache"
          ]
      }
  }
  ```


- **Resultado Esperado:**
  - O Composer mostrará uma lista de todos os scripts definidos, acompanhados das descrições que você especificou, facilitando o entendimento e a execução das tarefas automatizadas no seu projeto.

## Arquivos de Bloqueio (`composer.lock`)

### O Que é `composer.lock`?

- **Descrição:** 
  - O arquivo `composer.lock` armazena a versão exata de cada dependência instalada. Isso garante que, ao compartilhar o projeto, todos os desenvolvedores ou ambientes usem exatamente as mesmas versões das dependências.

### Importância do `composer.lock`

- **Controle de Versão:** 
  - O `composer.lock` deve ser incluído no controle de versão (por exemplo, Git) para garantir consistência entre diferentes ambientes de desenvolvimento e produção.

- **Instalação Consistente:** 
  - Quando você clona um projeto e executa `composer install`, as versões das dependências serão exatamente as mesmas definidas no `composer.lock`.

## Repositórios Personalizados

### Usando Repositórios Personalizados

- **Descrição:** 
  - O Composer permite que você adicione repositórios personalizados, como pacotes privados ou repositórios Git.

- **Exemplo de Configuração no `composer.json`:**
  ```json
  "repositories": [
      {
          "type": "vcs",
          "url": "https://github.com/usuario/meu-pacote.git"
      }
  ]
  ```

- **Instalando Pacote de Repositório Personalizado:**
  ```bash
  composer require usuario/meu-pacote
  ```

## Pacotes Globais

### Instalação Global de Pacotes

- **Descrição:** 
  - O Composer permite instalar pacotes globalmente, para que estejam disponíveis em todos os seus projetos.

- **Exemplo:**
  ```bash
  composer global require laravel/installer
  ```

- **Nota:**
  - Para usar pacotes globais, certifique-se de que o caminho do Composer global está no seu `PATH`. Em sistemas Unix, geralmente é `~/.composer/vendor/bin`.

