# Phan

## Introdução

**Phan** é um analisador estático para PHP que ajuda a identificar possíveis erros e problemas no código sem a necessidade de executá-lo. Ele é especialmente útil para detectar bugs, problemas de tipagem e inconsistências que podem passar despercebidos em um código PHP dinâmico. Phan é altamente configurável e suporta análise de código tanto para versões mais antigas quanto para as mais recentes do PHP.

## Instalação do Phan

### Requisitos

Antes de instalar o Phan, certifique-se de que você tem o PHP 7.1 ou superior instalado, pois o Phan depende de recursos introduzidos nessas versões. Além disso, você precisará do Composer para gerenciar a instalação.

### Instalação via Composer

**Passos:**

1. **Adicione o Phan como dependência de desenvolvimento ao seu projeto:**
   ```bash
   composer require --dev phan/phan
   ```

2. **Verifique a instalação:**
   ```bash
   vendor/bin/phan --version
   ```

**Resultado:**
- A execução do comando acima deve retornar a versão do Phan, confirmando a instalação correta.

## Configuração Básica do Phan

Após instalar o Phan, você precisa configurar a análise do seu projeto. Isso é feito através de um arquivo de configuração `phan.php` ou `phan_config.php`.

### Gerando um Arquivo de Configuração Padrão

**Comando:**
```bash
vendor/bin/phan --init
```

**Resultado:**
- Este comando gera um arquivo `phan.php` na raiz do projeto, que contém a configuração padrão.

### Estrutura Básica do `phan.php`

**Exemplo:**
```php
return [
    'target_php_version' => '8.0', // Defina a versão do PHP do projeto
    'directory_list' => [
        'src/', // Diretório onde o código será analisado
        'vendor/guzzlehttp/guzzle' // Inclua pacotes do vendor se necessário
    ],
    'exclude_analysis_directory_list' => [
        'vendor/' // Exclua a análise do diretório vendor
    ],
    'file_list' => [], // Arquivos individuais a serem analisados
    'plugins' => [
        'AlwaysReturnPlugin', 
        'DuplicateArrayKeyPlugin',
        'PregRegexCheckerPlugin',
    ],
];
```

**Opções Comuns:**
- **`target_php_version`**: Especifica a versão do PHP para a qual o código está sendo escrito.
- **`directory_list`**: Diretórios que devem ser analisados pelo Phan.
- **`exclude_analysis_directory_list`**: Diretórios a serem excluídos da análise.
- **`file_list`**: Lista de arquivos específicos a serem analisados (opcional).
- **`plugins`**: Lista de plugins que adicionam verificações adicionais.

## Executando o Phan

### Análise Básica

**Comando:**
```bash
vendor/bin/phan
```

**Resultado:**
- O Phan analisará o código nos diretórios especificados e exibirá uma lista de possíveis problemas, como erros de tipagem, funções não definidas, problemas de retorno e muito mais.

### Analisando Arquivos Específicos

**Comando:**
```bash
vendor/bin/phan src/MeuArquivo.php
```

**Resultado:**
- O Phan realizará a análise apenas no arquivo ou diretórios especificados.
