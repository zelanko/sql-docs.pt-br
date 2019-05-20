---
title: PDO::prepare | Microsoft Docs
ms.custom: ''
ms.date: 04/25/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7eac30ff1391ba5c56099cf7c59fa89b1368f115
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105875"
---
# <a name="pdoprepare"></a>PDO::prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara uma instrução para execução.

## <a name="syntax"></a>Sintaxe

```
PDOStatement PDO::prepare ( $statement [, array(key_pair)] )
```

#### <a name="parameters"></a>Parâmetros
$*statement*: uma cadeia de caracteres contendo a instrução SQL.

*key_pair*: uma matriz contendo um nome e valor de atributo. Para obter mais informações, consulte a seção Comentários.

## <a name="return-value"></a>Valor retornado
Retorna um objeto PDOStatement em caso de êxito. Em caso de falha, retorna um objeto PDOException ou false, dependendo do valor de `PDO::ATTR_ERRMODE`.

## <a name="remarks"></a>Remarks
Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] não avaliam instruções preparadas até a execução.

A tabela a seguir mostra os valores possíveis de *key_pair*.

|Chave|Descrição|
|-------|---------------|
|PDO::ATTR_CURSOR|Especifica o comportamento do cursor. O padrão é `PDO::CURSOR_FWDONLY`, um cursor de avanço que não é de rolagem. `PDO::CURSOR_SCROLL` é um cursor de rolagem.<br /><br />Por exemplo, `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`.<br /><br />Quando definido como `PDO::CURSOR_SCROLL`, você pode usar `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` para definir o tipo de cursor de rolagem, que está descrito abaixo.<br /><br />Veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) para obter mais informações sobre conjuntos de resultados e cursores no driver PDO_SQLSRV.|
|PDO::ATTR_EMULATE_PREPARES|Por padrão, esse atributo é false, e pode ser alterado usando o seguinte: `PDO::ATTR_EMULATE_PREPARES => true`. Confira [Emulate Prepare](#emulate-prepare) para saber mais e ver exemplos.|
|PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE|Especifica o tipo de cursor de rolagem. Válido somente quando `PDO::ATTR_CURSOR` está definido como `PDO::CURSOR_SCROLL`. Veja abaixo os valores que esse atributo pode usar.|
|PDO::SQLSRV_ATTR_DECIMAL_PLACES|Especifica o número de casas decimais ao formatar valores monetários buscados. Essa opção só funciona quando `PDO::SQLSRV_ATTR_FORMAT_DECIMALS` é true. Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_DIRECT_QUERY|Se for True, especifica a execução direta da consulta. False significa uma execução preparada da instrução. Para saber mais sobre `PDO::SQLSRV_ATTR_DIRECT_QUERY`, confira [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (padrão)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|
|PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE|Especifica quando recuperar tipos de data e hora como objetos de [DateTime PHP](http://php.net/manual/en/class.datetime.php). Para saber mais, confira [Como recuperar tipos de data e hora como objetos DateTime PHP usando o driver PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE|Lida com buscas numéricas de colunas com tipos SQL numéricos. Para obter mais informações, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|
|PDO::SQLSRV_ATTR_FORMAT_DECIMALS|Especifica quando é apropriado adicionar zeros à esquerda em cadeias de caracteres decimais. Se definida, essa opção habilita a opção `PDO::SQLSRV_ATTR_DECIMAL_PLACES` para formatação de tipos de moeda. Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver PDO_SQLSRV) ](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).| 
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Para obter mais informações, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|

Ao usar `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL`, use `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE` para especificar o tipo de cursor. Por exemplo, passe a matriz a seguir para PDO::Prepare para definir um cursor dinâmico:
```
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));
```
A tabela a seguir mostra os valores possíveis para `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE`. Para saber mais sobre os cursores de rolagem, confira [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).

|Valor|Descrição|
|---------|---------------|
|PDO::SQLSRV_CURSOR_BUFFERED|Cria um cursor estático do lado do cliente (em buffer), que armazena em buffer o conjunto de resultados na memória do computador do cliente.|
|PDO::SQLSRV_CURSOR_DYNAMIC|Cria um cursor dinâmico (sem buffer) do lado do servidor que permite acessar linhas em qualquer ordem e que refletirá as alterações no banco de dados.|
|PDO::SQLSRV_CURSOR_KEYSET|Cria um cursor de conjunto de chaves do lado do servidor. Um cursor de conjunto de chaves não atualiza a contagem de linhas se uma linha for excluída da tabela (uma linha excluída será retornada sem valores).|
|PDO::SQLSRV_CURSOR_STATIC|Cria um cursor estático do lado do servidor, que permite acessar linhas em qualquer ordem, mas que não refletirá as alterações no banco de dados.<br /><br />`PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` implica `PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC`.|

Você pode fechar um objeto PDOStatement chamando `unset`:
```
unset($stmt);
```

## <a name="example"></a>Exemplo
Este exemplo mostra como usar o método PDO::prepare com marcadores de parâmetro e um cursor de somente avanço.

```
<?php
$database = "Test";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$col1 = 'a';
$col2 = 'b';

$query = "insert into Table1(col1, col2) values(?, ?)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( $col1, $col2 ) );
print $stmt->rowCount();
echo "\n";

$query = "insert into Table1(col1, col2) values(:col1, :col2)";
$stmt = $conn->prepare( $query, array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY, PDO::SQLSRV_ATTR_QUERY_TIMEOUT => 1  ) );
$stmt->execute( array( ':col1' => $col1, ':col2' => $col2 ) );
print $stmt->rowCount();

unset($stmt);
?>
```

## <a name="example"></a>Exemplo
Este exemplo mostra como usar PDO::Prepare com um cursor estático do lado do servidor. Para ver um exemplo que mostra um cursor do lado do cliente, confira [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).

```
<?php
$database = "AdventureWorks";
$server = "(local)";
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");

$query = "select * from Person.ContactType";
$stmt = $conn->prepare( $query, array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL));
$stmt->execute();

echo "\n";

while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){
   print "$row[Name]\n";
}
echo "\n..\n";

$row = $stmt->fetch( PDO::FETCH_BOTH, PDO::FETCH_ORI_FIRST );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_ASSOC, PDO::FETCH_ORI_REL, 1 );
print "$row[Name]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT );
print "$row[1]\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_PRIOR );
print "$row[1]..\n";

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_ABS, 0 );
print_r($row);

$row = $stmt->fetch( PDO::FETCH_NUM, PDO::FETCH_ORI_LAST );
print_r($row);
?>
```

<a name="emulate-prepare" />

## <a name="example"></a>Exemplo

Este exemplo mostra como usar o método PDO::prepare com `PDO::ATTR_EMULATE_PREPARES` definido como true.

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$database = "tempdb";
$conn = new PDO("sqlsrv:server = $serverName; Database = $database", $username, $password);

$pdo_options = array();
$pdo_options[PDO::ATTR_EMULATE_PREPARES] = true;
$pdo_options[PDO::SQLSRV_ATTR_ENCODING] = PDO::SQLSRV_ENCODING_UTF8;

$stmt = $conn->prepare("CREATE TABLE TEST([id] [int] IDENTITY(1,1) NOT NULL,
                                          [name] nvarchar(max))",
                                          $pdo_options);
$stmt->execute();

$prefix = '가각';
$name = '가각ácasa';
$name2 = '가각sample2';

$stmt = $conn->prepare("INSERT INTO TEST(name) VALUES(:p0)", $pdo_options);
$stmt->execute(['p0' => $name]);
unset($stmt);

$stmt = $conn->prepare("SELECT * FROM TEST WHERE NAME LIKE :p0", $pdo_options);
$stmt->execute(['p0' => "$prefix%"]);
foreach ($stmt as $row) {
    echo "\n" . 'FOUND: ' . $row['name'];
}

unset($stmt);
unset($conn);
?>
```

O driver PDO_SQLSRV substitui internamente todos os espaços reservados pelos parâmetros que são limitados por [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md). Portanto, uma cadeia de caracteres de consulta SQL sem espaços reservados é enviada ao servidor. Considere este exemplo:

```
$statement = $PDO->prepare("INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)");
$statement->bindParam(:cus_name, "Cardinal");
$statement->bindParam(:con_name, "Tom B. Erichsen");
$statement->execute();
```

Com `PDO::ATTR_EMULATE_PREPARES` definido como false (o caso padrão), os dados enviados para o banco de dados são:

```
"INSERT into Customers (CustomerName, ContactName) VALUES (:cus_name, :con_name)"
Information on :cus_name parameter
Information on :con_name parameter
```

O servidor executará a consulta usando seu recurso de consulta parametrizada para parâmetros de associação. Por outro lado, com `PDO::ATTR_EMULATE_PREPARES` definido como true, a consulta enviada ao servidor é essencialmente:

```
"INSERT into Customers (CustomerName, ContactName) VALUES ('Cardinal', 'Tom B. Erichsen')"
```

Definir `PDO::ATTR_EMULATE_PREPARES` como true pode ignorar algumas restrições no SQL Server. Por exemplo, o SQL Server não oferece suporte a parâmetros nomeados ou posicionais em algumas cláusulas de Transact-SQL. Além disso, o SQL Server tem um limite de 2.100 parâmetros de associação.

> [!NOTE]
> Com emulate prepare definido como true, a segurança das consultas parametrizadas não é aplicada. Portanto, seu aplicativo deve garantir que os dados associados aos parâmetros não contenham código Transact-SQL mal-intencionado.

### <a name="encoding"></a>Codificação

Se o usuário deseja associar parâmetros com diferentes codificações (por exemplo, UTF-8 ou binária), ele deve especificar claramente a codificação no script PHP.

O driver PDO_SQLSRV primeiro verifica a codificação especificada em `PDO::bindParam()` (por exemplo, `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`).

Se não encontrado, o driver verifica se alguma codificação está definida em `PDO::prepare()` ou `PDOStatement::setAttribute()`. Caso contrário, o driver usa a codificação especificada em `PDO::__construct()` ou `PDO::setAttribute()`.

### <a name="limitations"></a>Limitações

Como você pode ver, a associação é feita internamente pelo driver. Uma consulta válida é enviada ao servidor para execução sem nenhum parâmetro. Em comparação com o caso regular, algumas limitações resultam quando o recurso de consulta parametrizada não está em uso.

- Ele não funciona para os parâmetros que são associados como `PDO::PARAM_INPUT_OUTPUT`.
    - Quando o usuário especifica `PDO::PARAM_INPUT_OUTPUT` em `PDO::bindParam()`, ocorre uma exceção de PDO.
- Não funciona para os parâmetros que são associados como parâmetros de saída.
    - Quando o usuário cria uma instrução preparada com espaços reservados que servem para parâmetros de saída (ou seja, ter um sinal de igual imediatamente após um espaço reservado, como `SELECT ? = COUNT(*) FROM Table1`), ocorre uma exceção de PDO.
    - Quando uma instrução preparada invoca um procedimento armazenado com um espaço reservado como argumento para um parâmetro de saída, nenhuma exceção é gerada porque o driver não pode detectar o parâmetro de saída. No entanto, a variável que o usuário fornece para o parâmetro de saída permanece inalterada.
- Espaços reservados duplicados para um parâmetro codificado binário não funcionarão

## <a name="see-also"></a>Consulte Também
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)

