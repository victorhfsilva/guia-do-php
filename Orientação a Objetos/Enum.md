# Enums em PHP

## Introdução

Enums (ou enumerações) foram introduzidos no PHP 8.1 como uma forma de definir um conjunto fixo de valores possíveis para uma variável. Eles são úteis quando você tem um grupo limitado e pré-definido de opções e deseja garantir que uma variável só possa assumir um desses valores. Enums melhoram a segurança e a legibilidade do código, tornando mais fácil trabalhar com conjuntos finitos de valores.

## Definindo um Enum

### Enum Básico

- **Descrição:** 
- Um enum é definido usando a palavra-chave `enum`. Ele pode conter um conjunto de casos (`cases`), cada um representando um valor único.

- **Sintaxe:**
```php
enum StatusPedido {
    case PENDENTE;
    case PROCESSANDO;
    case CONCLUIDO;
    case CANCELADO;
}
```

- **Exemplo de Uso:**
```php
$status = StatusPedido::PENDENTE;

if ($status === StatusPedido::PENDENTE) {
    echo "O pedido está pendente.";
}
```

### Enum com Valores

- **Descrição:** 
- Enums podem ter valores associados a cada caso. Em PHP, esses valores podem ser de tipos `string` ou `int`.

- **Sintaxe:**
```php
enum StatusPedido: string {
    case PENDENTE = 'pendente';
    case PROCESSANDO = 'processando';
    case CONCLUIDO = 'concluido';
    case CANCELADO = 'cancelado';
}
```

- **Exemplo de Uso:**
```php
$status = StatusPedido::CONCLUIDO;

echo $status->value; // Output: concluido
```

## Métodos em Enums

### Métodos Internos

- **Descrição:** 
- Você pode definir métodos dentro de um enum para adicionar comportamento personalizado. Isso é útil para manipular ou transformar os valores do enum.

- **Exemplo:**
```php
enum StatusPedido: string {
    case PENDENTE = 'pendente';
    case PROCESSANDO = 'processando';
    case CONCLUIDO = 'concluido';
    case CANCELADO = 'cancelado';

    public function descricao(): string {
        return match($this) {
            self::PENDENTE => 'O pedido ainda está pendente.',
            self::PROCESSANDO => 'O pedido está sendo processado.',
            self::CONCLUIDO => 'O pedido foi concluído.',
            self::CANCELADO => 'O pedido foi cancelado.',
        };
    }
}

$status = StatusPedido::PROCESSANDO;
echo $status->descricao(); // Output: O pedido está sendo processado.
```

### Métodos Estáticos

- **Descrição:** 
- Enums também podem ter métodos estáticos, permitindo a criação de métodos auxiliares para o enum.

- **Exemplo:**
```php
enum StatusPedido: string {
    case PENDENTE = 'pendente';
    case PROCESSANDO = 'processando';
    case CONCLUIDO = 'concluido';
    case CANCELADO = 'cancelado';

    public static function todosStatus(): array {
        return array_map(fn($case) => $case->value, self::cases());
    }
}

$status = StatusPedido::todosStatus();
print_r($status);
// Output: Array ( [0] => pendente [1] => processando [2] => concluido [3] => cancelado )
```

#### 4. Comparação de Enums

- **Descrição:** 
- Você pode comparar valores de enums usando o operador de identidade (`===`). Isso garante que tanto o tipo quanto o valor sejam iguais.

- **Exemplo:**
```php
$status = StatusPedido::PENDENTE;

if ($status === StatusPedido::PENDENTE) {
    echo "O pedido ainda está pendente.";
}
```
