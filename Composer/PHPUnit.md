# PHPUnit


PHPUnit é o framework de testes unitários mais popular para PHP. Ele permite que desenvolvedores testem suas aplicações de maneira automatizada, garantindo que o código funcione como esperado. Testes unitários ajudam a identificar bugs precocemente, promovem código de melhor qualidade e facilitam a manutenção de projetos à medida que crescem.

## Instalação do PHPUnit

### Instalando via Composer

- **Descrição:** 
  - A maneira recomendada de instalar o PHPUnit é através do Composer, que gerencia dependências do projeto.

- **Comando:**
  ```bash
  composer require --dev phpunit/phpunit ^10
  ```

- **Verificação da Instalação:**
  - Após a instalação, você pode verificar se o PHPUnit foi instalado corretamente executando:
    ```bash
    vendor/bin/phpunit --version
    ```

### Instalando Globalmente

- **Descrição:** 
  - Se preferir, você pode instalar o PHPUnit globalmente em sua máquina.

- **Comando:**
  ```bash
  wget https://phar.phpunit.de/phpunit.phar
  chmod +x phpunit.phar
  sudo mv phpunit.phar /usr/local/bin/phpunit
  ```

- **Verificação da Instalação:**
  ```bash
  phpunit --version
  ```

## Estrutura Básica de um Teste Unitário

### Criando um Teste

- **Descrição:** 
  - Um teste unitário em PHPUnit é uma classe que estende `PHPUnit\Framework\TestCase` e contém métodos que verificam se o código funciona corretamente.

- **Exemplo Simples:**
  ```php
  use PHPUnit\Framework\TestCase;

  class ExemploTest extends TestCase
  {
      public function testSomaSimples()
      {
          $resultado = 2 + 2;
          $this->assertEquals(4, $resultado);
      }
  }
  ```

### Estrutura de Diretórios

- **Descrição:**
  - Por convenção, os testes são colocados em um diretório `tests` separado do código-fonte, geralmente no diretório raiz do projeto.

- **Exemplo de Estrutura de Diretórios:**
  ```
  /meu-projeto
  ├── /src
  │   └── Calculadora.php
  ├── /tests
  │   └── CalculadoraTest.php
  ├── composer.json
  └── phpunit.xml
  ```

## Executando Testes

### Usando PHPUnit via Composer

- **Comando:**
  ```bash
  vendor/bin/phpunit
  ```

### Usando PHPUnit Instalado Globalmente

- **Comando:**
  ```bash
  phpunit
  ```

- **Output:**
  - Se os testes passarem, você verá uma saída indicando sucesso. Caso contrário, o PHPUnit mostrará quais testes falharam e por quê.

## Asserções Comuns

### Tipos de Asserções

- **`assertEquals($expected, $actual)`**: Verifica se dois valores são iguais.
- **`assertTrue($condition)`**: Verifica se a condição é verdadeira.
- **`assertFalse($condition)`**: Verifica se a condição é falsa.
- **`assertNull($value)`**: Verifica se o valor é `null`.
- **`assertNotNull($value)`**: Verifica se o valor não é `null`.
- **`assertCount($expectedCount, $array)`**: Verifica se um array contém o número esperado de elementos.

- **Exemplos:**
  ```php
  public function testAssercoes()
  {
      $this->assertEquals(4, 2 + 2);
      $this->assertTrue(true);
      $this->assertFalse(false);
      $this->assertNull(null);
      $this->assertNotNull("algum valor");
      $this->assertCount(3, [1, 2, 3]);
  }
  ```

## Testes de Exceções

- **Descrição:** 
  - PHPUnit permite que você teste se uma exceção específica é lançada durante a execução de um método.

- **Exemplo:**
  ```php
  public function testExcecaoEsperada()
  {
      $this->expectException(InvalidArgumentException::class);

      // Código que deve lançar a exceção
      throw new InvalidArgumentException("Exceção esperada");
  }
  ```

## Configuração do PHPUnit

### Arquivo `phpunit.xml`

- **Descrição:** 
  - Um arquivo `phpunit.xml` na raiz do projeto pode ser usado para configurar o PHPUnit. Ele permite definir opções de configuração, como o diretório de testes, a lista de testes a serem ignorados, a cobertura de código, entre outros.

- **Exemplo Básico de `phpunit.xml`:**
  ```xml
  <phpunit bootstrap="vendor/autoload.php" colors="true">
      <testsuites>
          <testsuite name="Testes do Meu Projeto">
              <directory>./tests</directory>
          </testsuite>
      </testsuites>
  </phpunit>
  ```

- **Executando com `phpunit.xml`:**
  - Com o arquivo `phpunit.xml` configurado, basta rodar `vendor/bin/phpunit` ou `phpunit` (se instalado globalmente), e o PHPUnit seguirá as configurações definidas.

## Cobertura de Código

### Gerando Cobertura de Código

- **Descrição:** 
  - PHPUnit pode gerar relatórios de cobertura de código, que mostram quais partes do código foram executadas durante os testes.

- **Comando:**
  ```bash
  vendor/bin/phpunit --coverage-html cobertura/
  ```

- **Resultado:** 
  - Isso gerará um relatório em HTML na pasta `cobertura/`, que pode ser visualizado em um navegador.

## Mocking

### Uso de Mocks

- **Descrição:** 
  - Mocks são objetos simulados que imitam o comportamento de objetos reais. Eles são usados para testar componentes em isolamento.

- **Exemplo de Mock:**
  ```php
  public function testComMock()
  {
      $mock = $this->createMock(MinhaClasse::class);

      $mock->method('meuMetodo')
           ->willReturn('valor esperado');

      $this->assertEquals('valor esperado', $mock->meuMetodo());
  }
  ```