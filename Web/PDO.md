# PDO (PHP Data Objects)

## Introdução

**PDO (PHP Data Objects)** é uma extensão do PHP que fornece uma interface leve e consistente para acessar bancos de dados. Ele suporta uma ampla gama de bancos de dados, como MySQL, PostgreSQL, SQLite, entre outros, e oferece uma maneira segura e eficiente de realizar operações de banco de dados usando prepared statements, que ajudam a prevenir injeção de SQL.

**Principais Benefícios do PDO:**
- **Suporte Multibanco:** Trabalha com vários sistemas de gerenciamento de banco de dados.
- **Segurança:** Oferece suporte a prepared statements, reduzindo o risco de injeção de SQL.
- **Interface Consistente:** Fornece uma API unificada, independentemente do banco de dados usado.
- **Modo de Erro Configurável:** Permite a personalização do tratamento de erros.

## Conectando ao Banco de Dados com PDO

### Configuração Básica

Para se conectar a um banco de dados usando PDO, você precisará do nome do banco de dados, nome de usuário, senha e host.

**Exemplo de Conexão com MySQL:**

```php
<?php
$host = '127.0.0.1';
$db = 'nome_do_banco';
$user = 'usuario';
$pass = 'senha';
$charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";

$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $pdo = new PDO($dsn, $user, $pass, $options);
    echo "Conexão bem-sucedida!";
} catch (\PDOException $e) {
    throw new \PDOException($e->getMessage(), (int)$e->getCode());
}
```

### Componentes da Conexão

- **DSN (Data Source Name):** 
  - String que especifica o driver e os detalhes da conexão.
  - Exemplo: `mysql:host=127.0.0.1;dbname=nome_do_banco;charset=utf8mb4`.
- **Atributos PDO:** 
  - Configurações que determinam como o PDO se comporta, como o modo de erro e o tipo de fetch.
  - `PDO::ATTR_ERRMODE`: Define o modo de erro para lançar exceções (`PDO::ERRMODE_EXCEPTION`).
  - `PDO::ATTR_DEFAULT_FETCH_MODE`: Define o modo de busca padrão (`PDO::FETCH_ASSOC` para arrays associativos).
  - `PDO::ATTR_EMULATE_PREPARES`: Desativa a emulação de prepared statements para usar a funcionalidade nativa do banco de dados.

## Executando Consultas com PDO

### Consultas Simples

**Descrição:**
- Você pode executar consultas simples diretamente com o método `query`.

**Exemplo:**
```php
$sql = 'SELECT * FROM usuarios';
$stmt = $pdo->query($sql);

while ($row = $stmt->fetch()) {
    echo $row['nome'] . "<br>";
}
```

### Prepared Statements

**Descrição:**
- Prepared statements são usados para consultas que precisam de parâmetros, oferecendo segurança contra injeção de SQL.

**Exemplo com `prepare()` e `execute()`:**
```php
$sql = 'SELECT * FROM usuarios WHERE id = :id';
$stmt = $pdo->prepare($sql);
$stmt->execute(['id' => $id]);

$usuario = $stmt->fetch();
echo $usuario['nome'];
```

### Inserção de Dados

**Descrição:**
- Para inserir dados no banco, você pode usar prepared statements com o comando `INSERT`.

**Exemplo:**
```php
$sql = 'INSERT INTO usuarios (nome, email) VALUES (:nome, :email)';
$stmt = $pdo->prepare($sql);
$stmt->execute(['nome' => 'João', 'email' => 'joao@example.com']);

echo "Novo usuário inserido com sucesso!";
```

### Atualização de Dados

**Descrição:**
- O comando `UPDATE` permite modificar registros existentes.

**Exemplo:**
```php
$sql = 'UPDATE usuarios SET email = :email WHERE id = :id';
$stmt = $pdo->prepare($sql);
$stmt->execute(['email' => 'novoemail@example.com', 'id' => $id]);

echo "Usuário atualizado com sucesso!";
```

### Exclusão de Dados

**Descrição:**
- O comando `DELETE` remove registros do banco de dados.

**Exemplo:**
```php
$sql = 'DELETE FROM usuarios WHERE id = :id';
$stmt = $pdo->prepare($sql);
$stmt->execute(['id' => $id]);

echo "Usuário excluído com sucesso!";
```

## Tratamento de Erros

### Modo de Erro

**Descrição:**
- O PDO permite configurar o modo de erro para lançar exceções, o que facilita a detecção e o tratamento de problemas.

**Exemplo:**
```php
$pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

### Captura de Exceções

**Descrição:**
- Ao configurar o modo de erro como exceção, você pode capturar erros usando `try...catch`.

**Exemplo:**
```php
try {
    $stmt = $pdo->query('SELECT * FROM tabela_inexistente');
} catch (PDOException $e) {
    echo "Erro: " . $e->getMessage();
}
```

## Fechando a Conexão

**Descrição:**
- A conexão com o banco de dados é fechada automaticamente quando o objeto PDO é destruído. Para fechar explicitamente a conexão, defina a variável PDO como `null`.

**Exemplo:**
```php
$pdo = null;
```

## Trabalhando com Transações

### Iniciando uma Transação

**Descrição:**
- Transações permitem agrupar várias operações de banco de dados em uma única unidade de trabalho. Se qualquer operação falhar, todas as mudanças podem ser revertidas.

**Exemplo:**
```php
try {
    $pdo->beginTransaction();

    $stmt1 = $pdo->prepare('INSERT INTO usuarios (nome, email) VALUES (?, ?)');
    $stmt1->execute(['Maria', 'maria@example.com']);

    $stmt2 = $pdo->prepare('UPDATE contas SET saldo = saldo - 100 WHERE id = ?');
    $stmt2->execute([1]);

    $pdo->commit();
} catch (Exception $e) {
    $pdo->rollBack();
    echo "Falha na transação: " . $e->getMessage();
}
```

### Revertendo uma Transação

**Descrição:**
- Se algo der errado durante a execução de uma transação, você pode reverter todas as operações usando `rollBack()`.

**Exemplo:**
```php
$pdo->rollBack();
```

## Fetch Modes

### Modos de Busca

**Descrição:**
- O PDO oferece vários modos de busca que determinam como os resultados da consulta são retornados.

**Modos Comuns:**
- **`PDO::FETCH_ASSOC`**: Retorna um array associativo.
- **`PDO::FETCH_NUM`**: Retorna um array indexado numericamente.
- **`PDO::FETCH_BOTH`**: Retorna um array com índices numéricos e associativos.
- **`PDO::FETCH_OBJ`**: Retorna um objeto anônimo.
- **`PDO::FETCH_CLASS`**: Mapeia os resultados em uma classe especificada.

**Exemplo:**
```php
$stmt = $pdo->query('SELECT * FROM usuarios');

// Como objeto
while ($row = $stmt->fetch(PDO::FETCH_OBJ)) {
    echo $row->nome . "<br>";
}

// Como array associativo
while ($row = $stmt->fetch(PDO::FETCH_ASSOC)) {
    echo $row['nome'] . "<br>";
}
```

## Injeção de SQL e Segurança

**Descrição:**
- PDO oferece proteção contra injeção de SQL ao usar prepared statements com parâmetros vinculados. Nunca use diretamente valores de entrada do usuário em consultas SQL sem sanitizá-los.

**Exemplo de Segurança:**
```php
$stmt = $pdo->prepare('SELECT * FROM usuarios WHERE email = :email');
$stmt->execute(['email' => $_POST['email']]);

$usuario = $stmt->fetch();
```

