# Métodos e Parâmetros Estáticos em PHP

## Introdução

Em PHP, métodos e propriedades estáticas pertencem à própria classe, em vez de uma instância específica de uma classe. Isso significa que você pode acessá-los sem criar um objeto da classe. Métodos e propriedades estáticos são úteis para armazenar informações ou comportamentos que devem ser compartilhados entre todas as instâncias da classe ou que não dependem de uma instância específica.

## Propriedades Estáticas

### Definindo Propriedades Estáticas

- **Descrição:**
- Propriedades estáticas são declaradas com a palavra-chave `static`. Elas são compartilhadas por todas as instâncias da classe e são acessíveis diretamente pela classe, sem a necessidade de criar um objeto.

- **Sintaxe:**
```php
class Configuracao {
    public static $siteName = "Meu Site";

    public static function obterSiteName() {
        return self::$siteName;
    }
}
```

### Acessando Propriedades Estáticas

- **Descrição:**
- Propriedades estáticas podem ser acessadas usando `self::` dentro da classe ou `NomeDaClasse::` fora da classe.

- **Exemplo:**
```php
echo Configuracao::$siteName; // Output: Meu Site
```

- **Alterando Propriedades Estáticas:**
```php
Configuracao::$siteName = "Novo Nome do Site";
echo Configuracao::obterSiteName(); // Output: Novo Nome do Site
```

## Métodos Estáticos

### Definindo Métodos Estáticos

- **Descrição:**
- Métodos estáticos são definidos usando a palavra-chave `static`. Como propriedades estáticas, eles são acessíveis sem instanciar a classe.

- **Sintaxe:**
```php
class Utilidades {
    public static function saudacao($nome) {
        return "Olá, " . $nome;
    }
}
```

### Acessando Métodos Estáticos

- **Descrição:**
- Métodos estáticos podem ser chamados usando `NomeDaClasse::metodo()`.

- **Exemplo:**
```php
echo Utilidades::saudacao("João"); // Output: Olá, João
```

## Diferença entre `self::` e `static::`

- **`self::`**:
- Refere-se à classe onde o método está sendo definido, ignorando a classe que está chamando o método. Portanto, ele não respeita o comportamento de herança.

- **`static::`**:
- Introduzido no PHP 5.3, refere-se à classe que realmente faz a chamada do método, respeitando o comportamento de herança (conhecido como "Late Static Binding").

- **Exemplo Comparativo:**
```php
class Pai {
    public static function quemSouEu() {
        return self::class;
    }

    public static function quemSouEuStatic() {
        return static::class;
    }
}

class Filho extends Pai {}

echo Filho::quemSouEu();        // Output: Pai
echo Filho::quemSouEuStatic();  // Output: Filho
```
