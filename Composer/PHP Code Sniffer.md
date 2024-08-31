# PHP_CodeSniffer (PHPCS)

## Introdução

PHP_CodeSniffer (PHPCS) é uma ferramenta que analisa e verifica se o código PHP segue um determinado padrão de codificação. Ele é amplamente utilizado para garantir a consistência do código em projetos, especialmente em equipes, ajudando a evitar erros comuns e a manter a qualidade do código. O PHPCS suporta vários padrões de codificação, como PSR-1, PSR-2, PSR-12, entre outros.

## Instalação do PHP_CodeSniffer

### Instalando via Composer

- **Descrição:** 
  - A maneira mais comum de instalar o PHPCS é através do Composer, como uma dependência de desenvolvimento.

- **Comando:**
  ```bash
  composer require --dev squizlabs/php_codesniffer
  ```

#### Verificação da Instalação

- **Comando:**
  ```bash
  vendor/bin/phpcs --version
  ```

- **Resultado:** 
  - Isso deve exibir a versão do PHPCS instalada no seu projeto.

#### Instalação Global

- **Descrição:** 
  - Você também pode instalar o PHPCS globalmente em seu sistema para usá-lo em todos os projetos.

- **Comando:**
  ```bash
  composer global require squizlabs/php_codesniffer
  ```

- **Verificação:**
  ```bash
  phpcs --version
  ```

## Uso Básico do PHPCS

### Verificando o Código

- **Comando:**
  - Para verificar um arquivo ou um diretório específico, use o seguinte comando:
  
  ```bash
  vendor/bin/phpcs caminho/para/arquivo.php
  ```

- **Exemplo:**
  ```bash
  vendor/bin/phpcs src/MeuArquivo.php
  ```

### Verificando Todo o Projeto

- **Comando:**
  - Para verificar todo o projeto (ou diretório), você pode rodar o PHPCS na raiz do projeto:

  ```bash
  vendor/bin/phpcs src/
  ```

### Usando a Instalação Global

- **Comando Global:**
  ```bash
  phpcs caminho/para/arquivo.php
  ```

## Padrões de Codificação

### Definindo o Padrão de Codificação

- **Descrição:** 
  - O PHPCS suporta vários padrões de codificação, como PSR-1, PSR-2, PSR-12, entre outros. Você pode especificar o padrão que deseja aplicar durante a análise.

- **Comando:**
  ```bash
  vendor/bin/phpcs --standard=PSR12 src/
  ```

- **Principais Padrões Suportados:**
  - **PSR-1:** Um padrão básico de codificação para PHP.
  - **PSR-2:** Um guia de estilo estrito baseado no PSR-1.
  - **PSR-12:** Uma extensão do PSR-2 com mais detalhes para padrões de codificação.

- **Exemplo de Verificação com PSR-12:**
  ```bash
  vendor/bin/phpcs --standard=PSR12 src/
  ```

### Configurando o Padrão de Codificação por Padrão

- **Comando para Configuração Global:**
  ```bash
  vendor/bin/phpcs --config-set default_standard PSR12
  ```

- **Verificação do Padrão Configurado:**
  ```bash
  vendor/bin/phpcs --config-show
  ```

## Ignorando Arquivos ou Diretórios

### Ignorando Diretórios ou Arquivos

- **Descrição:** 
  - Você pode instruir o PHPCS a ignorar certos arquivos ou diretórios durante a verificação.

- **Comando:**
  ```bash
  vendor/bin/phpcs --ignore=vendor/*,tests/* src/
  ```

### Configuração via `phpcs.xml`

- **Descrição:** 
  - Você também pode criar um arquivo de configuração `phpcs.xml` no diretório raiz do projeto para definir os padrões, diretórios ignorados e outras configurações.

- **Exemplo de `phpcs.xml`:**
  ```xml
  <?xml version="1.0"?>
  <ruleset name="Meu Projeto">
      <description>Análise de padrão de codificação para Meu Projeto</description>
      <rule ref="PSR12"/>

      <exclude-pattern>*/vendor/*</exclude-pattern>
      <exclude-pattern>*/tests/*</exclude-pattern>

      <file>src/</file>
  </ruleset>
  ```

- **Uso:**
  - Após configurar o arquivo `phpcs.xml`, você pode rodar o PHPCS sem passar opções extras:
    ```bash
    vendor/bin/phpcs
    ```

## Corrigindo Problemas com PHP_CodeSniffer (PHPCBF)

### Introdução ao PHPCBF

- **Descrição:** 
  - O PHP_CodeSniffer também inclui uma ferramenta de correção automática chamada PHP Code Beautifier and Fixer (PHPCBF). Ela tenta corrigir automaticamente os problemas de formatação que o PHPCS identifica.

- **Comando para Corrigir:**
  ```bash
  vendor/bin/phpcbf src/
  ```

### Corrigindo Arquivo Específico

- **Comando:**
  ```bash
  vendor/bin/phpcbf src/MeuArquivo.php
  ```

- **Uso com Instalação Global:**
  ```bash
  phpcbf src/
  ```

