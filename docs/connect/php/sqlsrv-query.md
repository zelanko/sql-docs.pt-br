---
title: sqlsrv_query | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_query
apitype: NA
helpviewer_keywords:
- sqlsrv_query
- executing queries
- API Reference, sqlsrv_query
ms.assetid: 9fa7c4c8-4da8-4299-9893-f61815055aa3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19d7f4d6562f64061f01bf0ff7a73fcd03a4f63c
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606246"
---
# <a name="sqlsrvquery"></a>sqlsrv_query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Prepara e executa uma instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_query(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: o recurso de conexão associado à instrução preparada.  
  
*$tsql*: a expressão Transact-SQL que corresponde à instrução preparada.  
  
*$params* [OPCIONAL]: uma **matriz** de valores que correspondem a parâmetros em uma consulta parametrizada. Cada elemento da matriz pode ser um dos seguintes:
  
-   Um valor literal.  
  
-   Uma variável do PHP.  
  
-   Uma **matriz** com a seguinte estrutura:  
  
    ```  
    array($value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    A descrição de cada elemento da matriz está na tabela a seguir:  
  
    |Elemento|Descrição|  
    |-----------|---------------|  
    |*$value*|Um valor literal, uma variável do PHP ou uma variável do PHP por referência.|  
    |*$direction*[opcional]|Uma das seguintes constantes **SQLSRV_PARAM_\*** usadas para indicar a direção do parâmetro: **SQLSRV_PARAM_IN**, **SQLSRV_PARAM_OUT**, **SQLSRV_PARAM_INOUT**. O valor padrão é **SQLSRV_PARAM_IN**.<br /><br />Para obter mais informações sobre constantes do PHP, consulte [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$phpType*[opcional]|Uma constante **SQLSRV_PHPTYPE _\*** que especifica o tipo de dados do PHP do valor retornado.<br /><br />Para obter mais informações sobre constantes do PHP, consulte [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$sqlType*[opcional]|Uma constante **SQLSRV_SQLTYPE_\*** que especifica o tipo de dados do SQL Server do valor de entrada.<br /><br />Para obter mais informações sobre constantes do PHP, consulte [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
  
*$options* [OPCIONAL]: uma matriz associativa que define as propriedades da consulta. As chaves com suporte são as seguintes:  
  
|Chave|Valores com suporte|Descrição|  
|-------|--------------------|---------------|  
|QueryTimeout|Um valor inteiro positivo.|Define o tempo limite da consulta em segundos. Por padrão, o driver aguarda resultados indefinidamente.|  
|SendStreamParamsAtExec|**true** ou **false**<br /><br />O valor padrão é **true**.|Configura o driver para enviar todos os dados de fluxo na execução **true** ou para enviar dados de fluxo em partes (**false**). Por padrão, o valor é definido como **true**. Para obter mais informações, consulte [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md).|  
|Rolável|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|Para obter mais informações sobre esses valores, consulte [Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).|  
  
## <a name="return-value"></a>Valor retornado  
Um recurso de instrução. Se não for possível criar e/ou executar a instrução, **false** será retornado.  
  
## <a name="remarks"></a>Remarks  
A função **sqlsrv_query** é adequada para consultas únicas e deve ser a opção padrão para executar consultas, a menos que circunstâncias especiais se apliquem. Essa função fornece um método simplificado para executar uma consulta com uma quantidade mínima de código. A função **sqlsrv_query** realiza a preparação e a execução da instrução e pode ser usada para executar consultas parametrizadas.  
  
Para obter mais informações, consulte [How to: Retrieve Output Parameters Using the SQLSRV Driver](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).  
  
## <a name="example"></a>Exemplo  
No exemplo a seguir, uma única linha é inserida na tabela *Sales.SalesOrderDetail* do banco de dados AdventureWorks. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
> [!NOTE]  
> Embora o exemplo a seguir use uma instrução INSERT para demonstrar o uso de **sqlsrv_query** para a execução de uma instrução única, o conceito se aplica a qualquer instrução Transact-SQL.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "INSERT INTO Sales.SalesOrderDetail   
        (SalesOrderID,   
         OrderQty,   
         ProductID,   
         SpecialOfferID,   
         UnitPrice,   
         UnitPriceDiscount)  
        VALUES   
        (?, ?, ?, ?, ?, ?)";  
  
/* Set parameter values. */  
$params = array(75123, 5, 741, 1, 818.70, 0.00);  
  
/* Prepare and execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if ($stmt) {  
    echo "Row successfully inserted.\n";  
} else {  
    echo "Row insertion failed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir atualiza um campo na tabela *Sales.SalesOrderDetail* do banco de dados AdventureWorks. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array("Database"=>"AdventureWorks");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
    echo "Could not connect.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = (?)   
         WHERE SalesOrderDetailID = (?)";  
  
/* Assign literal parameter values. */  
$params = array(5, 10);  
  
/* Execute the query. */  
if (sqlsrv_query($conn, $tsql, $params)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Error in statement execution.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> É recomendável usar cadeias de caracteres como entradas ao associar os valores para um [coluna decimal ou numérica](https://docs.microsoft.com/sql/t-sql/data-types/decimal-and-numeric-transact-sql) para garantir a precisão e a precisão, como PHP limitou a precisão para [números de ponto flutuante](https://php.net/manual/en/language.types.float.php). O mesmo se aplica a colunas bigint, especialmente quando os valores estão fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

## <a name="example"></a>Exemplo  
Este exemplo de código mostra como associar um valor decimal como um parâmetro de entrada.  

```
<?php
$serverName = "(local)";
$connectionInfo = array("Database"=>"YourTestDB");  
$conn = sqlsrv_connect($serverName, $connectionInfo);  
if ($conn === false) {  
     echo "Could not connect.\n";  
     die(print_r(sqlsrv_errors(), true));  
}  

// Assume TestTable exists with a decimal field 
$input = "9223372036854.80000";
$params = array($input);
$stmt = sqlsrv_query($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="example"></a>Exemplo
Este exemplo de código mostra como criar uma tabela de [sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) tipos e buscar os dados inseridos.

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$options = array("Database"=>$dbName, "UID"=>$uid, "PWD"=>$pwd);
$conn = sqlsrv_connect($server, $options);
if($conn === false) {
    die(print_r(sqlsrv_errors(), true));
}

$tableName = 'testTable';
$query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
$stmt = sqlsrv_query($conn, $query);
if($stmt === false) {
    die(print_r(sqlsrv_errors(), true));
}
sqlsrv_free_stmt($stmt);

$query = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $query);

if(sqlsrv_fetch($stmt) === false) {
    die(print_r(sqlsrv_errors(), true));
}

$col1 = sqlsrv_get_field($stmt, 0);
echo "First field:  $col1 \n";

$col2 = sqlsrv_get_field($stmt, 1);
echo "Second field:  $col2 \n";

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

?>
```

A saída esperada seria:

```
First field:  1
Second field:  test_data
```

## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Como executar consultas parametrizadas](../../connect/php/how-to-perform-parameterized-queries.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  

[Como enviar dados como um fluxo](../../connect/php/how-to-send-data-as-a-stream.md)  

[Usando parâmetros direcionais](../../connect/php/using-directional-parameters.md)  

  
