---
title: 'PDO:: Prepare | Microsoft Docs'
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8b16fdc-c748-49be-acf2-a6ac7432d16b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca5e1a4d0dd3f76b3fabefa6549eb644a894845a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745134"
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
Retorna um objeto PDOStatement em caso de êxito. Em caso de falha, retorna um objeto PDOException ou false, dependendo do valor de PDO::ATTR_ERRMODE.  
  
## <a name="remarks"></a>Remarks  
Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] não avaliam instruções preparadas até a execução.  
  
A tabela a seguir mostra os valores possíveis de *key_pair*.  
  
|Chave|Descrição|  
|-------|---------------|  
|PDO::ATTR_CURSOR|Especifica o comportamento do cursor. O padrão é PDO::CURSOR_FWDONLY. PDO::CURSOR_SCROLL é um cursor estático.<br /><br />Por exemplo, `array( PDO::ATTR_CURSOR => PDO::CURSOR_FWDONLY )`.<br /><br />Se você usar PDO::CURSOR_SCROLL, pode usar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE, descrito abaixo.<br /><br />Veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) para obter mais informações sobre conjuntos de resultados e cursores no driver PDO_SQLSRV.|  
|PDO::ATTR_EMULATE_PREPARES|Por padrão, esse atributo é false, que pode ser alterado por este `PDO::ATTR_EMULATE_PREPARES => true`. Ver [emular preparar](#emulate-prepare) para obter detalhes e exemplo.|
|PDO::SQLSRV_ATTR_ENCODING|PDO::SQLSRV_ENCODING_UTF8 (padrão)<br /><br />PDO::SQLSRV_ENCODING_SYSTEM<br /><br />PDO::SQLSRV_ENCODING_BINARY|  
|PDO::SQLSRV_ATTR_DIRECT_QUERY|Se for True, especifica a execução direta da consulta. False significa uma execução preparada da instrução. Para obter mais informações sobre PDO::SQLSRV_ATTR_DIRECT_QUERY, veja [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_ATTR_QUERY_TIMEOUT|Para obter mais informações, consulte [PDO::setAttribute](../../connect/php/pdo-setattribute.md).|  
  
Quando você usa PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, pode usar PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE. Por exemplo,  
  
```  
array(PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL, PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_DYNAMIC));  
```  
  
A tabela a seguir mostra os valores possíveis para PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE.  
  
|Valor|Descrição|  
|---------|---------------|  
|PDO::SQLSRV_CURSOR_BUFFERED|Cria um cursor estático (em buffer) do lado do cliente. Para obter mais informações sobre os cursores do lado do cliente, veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).|  
|PDO::SQLSRV_CURSOR_DYNAMIC|Cria um cursor dinâmico (sem buffer) do lado do servidor que permite acessar linhas em qualquer ordem e que refletirá as alterações no banco de dados.|  
|PDO::SQLSRV_CURSOR_KEYSET_DRIVEN|Cria um cursor de conjunto de chaves do lado do servidor. Um cursor de conjunto de chaves não atualiza a contagem de linhas se uma linha for excluída da tabela (uma linha excluída será retornada sem valores).|  
|PDO::SQLSRV_CURSOR_STATIC|Cria um cursor estático do lado do servidor, que permite acessar linhas em qualquer ordem, mas que não refletirá as alterações no banco de dados.<br /><br />PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL implica em PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE => PDO::SQLSRV_CURSOR_STATIC.|  
  
Você pode fechar um objeto PDOStatement definindo-o como null.  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra como usar o método PDO::prepare com marcadores de parâmetro e um cursor somente de avanço.  
  
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
  
$stmt = null  
?>  
```  

## <a name="example"></a>Exemplo  
Este exemplo mostra como usar o método PDO::prepare com um cursor do lado do cliente. Para obter uma amostra exibindo um cursor do lado do servidor, veja [Tipos de cursor &#40;Driver PDO_SQLSRV&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).  
  
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

O driver PDO_SQLSRV internamente substitui todos os espaços reservados com os parâmetros que são associados pelas [PDOStatement::bindParam()](../../connect/php/pdostatement-bindparam.md). Portanto, uma cadeia de caracteres de consulta SQL com nenhum espaço reservado é enviada ao servidor. Considere este exemplo,

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

Definindo `PDO::ATTR_EMULATE_PREPARES` para true pode ignorar algumas restrições no SQL Server. Por exemplo, SQL Server não dá suporte a parâmetros nomeados ou posicionais em algumas cláusulas de Transact-SQL. Além disso, o SQL Server tem um limite de 2100 parâmetros de associação.

> [!NOTE]
> Com emulate prepara-se definido como true, a segurança das consultas parametrizadas não estiver em vigor. Portanto, seu aplicativo deve garantir que os dados associados aos parâmetros não contenham código Transact-SQL mal-intencionado.

### <a name="encoding"></a>Codificação

Se o usuário deseja associar parâmetros com diferentes codificações (por exemplo, UTF-8 ou binária), usuário deve especificar claramente a codificação no script PHP.

O driver PDO_SQLSRV primeiro verifica a codificação especificada na `PDO::bindParam()` (por exemplo, `$statement->bindParam(:cus_name, "Cardinal", PDO::PARAM_STR, 10, PDO::SQLSRV_ENCODING_UTF8)`). 

Se não encontrado, o driver verificará se nenhuma codificação é definido em `PDO::prepare()` ou `PDOStatement::setAttribute()`. Caso contrário, o driver usará a codificação especificada na `PDO::__construct()` ou `PDO::setAttribute()`.

### <a name="limitations"></a>Limitações

Como você pode ver, a associação é feita internamente pelo driver. Uma consulta válida é enviada ao servidor para execução sem nenhum parâmetro. Em comparação com o caso comum, algumas limitações resultam quando o recurso de consulta com parâmetros não está em uso.

- Ele não funciona para os parâmetros que são associados como `PDO::PARAM_INPUT_OUTPUT`.
    - Quando o usuário especifica `PDO::PARAM_INPUT_OUTPUT` em `PDO::bindParam()`, uma exceção de PDO é lançada.
- Ele não funciona para os parâmetros que são associados como parâmetros de saída.
    - Quando o usuário cria uma instrução preparada com espaços reservados que servem para parâmetros de saída (ou seja, ter um sinal de igual imediatamente após um espaço reservado, como `SELECT ? = COUNT(*) FROM Table1`), uma exceção de PDO é lançada.
    - Quando uma instrução preparada invoca um procedimento armazenado com um espaço reservado como argumento para um parâmetro de saída, nenhuma exceção é gerada porque o driver não pode detectar o parâmetro de saída. No entanto, a variável que o usuário fornece para o parâmetro de saída permanecerá inalterada.
- Espaços reservados duplicados para um parâmetro codificado binário não funcionará

## <a name="see-also"></a>Consulte Também  
[Classe PDO](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
