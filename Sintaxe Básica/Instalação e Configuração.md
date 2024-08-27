# Configuração e Instalação do PHP

## Introdução

O PHP é uma linguagem de programação popular usada principalmente para desenvolvimento web. Este guia detalha os passos necessários para instalar e configurar o PHP no seu sistema.

## Pré-requisitos
Antes de começar a instalação do PHP, verifique os seguintes pré-requisitos:

- **Servidor Web:** Apache ou Nginx são os mais comuns.
- **Acesso ao Terminal:** Para executar comandos.
- **Sistema Operacional:** Este guia cobre os sistemas operacionais Windows, macOS e Linux.

## Instalando o PHP no Windows

1. **Download do PHP:**
   - Acesse o site oficial do PHP: [https://www.php.net/downloads.php](https://www.php.net/downloads.php)
   - Baixe a versão mais recente do PHP que seja compatível com seu sistema (normalmente a versão "Thread Safe" para Windows).

2. **Extrair os Arquivos:**
   - Extraia o arquivo baixado para uma pasta de fácil acesso, por exemplo, `C:\php`.

3. **Configurar as Variáveis de Ambiente:**
   - Abra o **Painel de Controle > Sistema > Configurações Avançadas do Sistema > Variáveis de Ambiente**.
   - Adicione o caminho da pasta PHP (ex: `C:\php`) na variável `Path` do sistema.

4. **Configurar o PHP:**
   - Navegue até a pasta onde você extraiu o PHP (`C:\php`).
   - Renomeie o arquivo `php.ini-development` para `php.ini`.
   - Abra o arquivo `php.ini` com um editor de texto (ex: Notepad++).
   - Ative as extensões necessárias removendo o ponto e vírgula (;) antes da linha correspondente, por exemplo:
     ```ini
     extension=curl
     extension=gd
     extension=mbstring
     extension=mysqli
     extension=pdo_mysql
     ```

5. **Testar a Instalação:**
   - Abra o terminal e digite `php -v`. Isso deve mostrar a versão do PHP instalada.
   - Para testar com o servidor Apache, certifique-se de que o Apache esteja instalado e adicione as seguintes linhas no arquivo `httpd.conf`:
     ```apache
     LoadModule php_module "c:/php/php7apache2_4.dll"
     AddHandler application/x-httpd-php .php
     ```
   - Reinicie o servidor Apache e crie um arquivo `info.php` com o conteúdo:
     ```php
     <?php
     phpinfo();
     ?>
     ```
   - Acesse `http://localhost/info.php` no navegador. Se a página de informações do PHP aparecer, a instalação foi bem-sucedida.

## Instalando o PHP no Linux (Ubuntu/Debian)

1. **Atualizar o Sistema:**
   - Abra o Terminal e execute:
     ```bash
     sudo apt update
     sudo apt upgrade
     ```

2. **Instalar o PHP:**
   - Para instalar o PHP e as extensões comuns:
     ```bash
     sudo apt install php libapache2-mod-php php-mysql php-cli php-curl php-gd php-mbstring
     ```

3. **Configurar o PHP:**
   - O arquivo de configuração principal do PHP está localizado em `/etc/php/7.x/apache2/php.ini` (o `7.x` depende da versão instalada).
   - Edite o arquivo para ajustar as configurações de acordo com suas necessidades.

4. **Testar a Instalação:**
   - Verifique a versão do PHP:
     ```bash
     php -v
     ```
   - Reinicie o Apache para aplicar as mudanças:
     ```bash
     sudo systemctl restart apache2
     ```
   - Crie o arquivo `info.php` no diretório `/var/www/html/` e acesse `http://localhost/info.php`.

## Configurações Adicionais

- **Alterar o Fuso Horário:**
  - No arquivo `php.ini`, procure por `date.timezone` e defina o fuso horário:
    ```ini
    date.timezone = "America/Sao_Paulo"
    ```

- **Limite de Memória:**
  - No `php.ini`, você pode alterar o limite de memória:
    ```ini
    memory_limit = 256M
    ```

- **Tamanho Máximo de Upload:**
  - Ajuste o tamanho máximo de upload no `php.ini`:
    ```ini
    upload_max_filesize = 50M
    post_max_size = 50M
    ```