---
title: sqlsrv_prepare
description: Referência da API para a função sqlsrv_prepare no Driver SQLSRV da Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 04/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_prepare
apitype: NA
helpviewer_keywords:
- executing queries
- API Reference, sqlsrv_prepare
- sqlsrv_prepare
ms.assetid: 8c74c697-3296-4f5d-8fb9-e361f53f19a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 51f1bd58c872516ffdf79d3a957b7c4674b82cd8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726666"
---
# <a name="sqlsrv_prepare"></a>sqlsrv_prepare
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cria um recurso de instrução associado à conexão especificada. Essa função é útil para a execução de várias consultas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_prepare(resource $conn, string $tsql [, array $params [, array $options]])  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: o recurso de conexão associado à instrução preparada.  
  
*$tsql*: a expressão Transact-SQL que corresponde à instrução criada.  
  
*$params* [OPTIONAL]: uma **matriz** de valores que correspondem aos parâmetros em uma consulta parametrizada. Cada elemento da matriz pode ser um dos seguintes:
  
-   Um valor literal.  
  
-   Uma referência a uma variável do PHP.  
  
-   Uma **matriz** com a seguinte estrutura:  
  
    ```  
    array(&$value [, $direction [, $phpType [, $sqlType]]])  
    ```  
  
    > [!NOTE]  
    > Variáveis passadas como parâmetros de consulta devem ser passadas por referência em vez de por valor. Por exemplo, passe `&$myVariable` em vez de `$myVariable`. Um aviso do PHP será gerado quando uma consulta com parâmetros por valor for executada.  
  
    A tabela a seguir descreve os elementos dessa matriz:  
  
    |Elemento|Descrição|  
    |-----------|---------------|  
    |*&$value*|Um valor literal ou uma referência a uma variável do PHP.|  
    |*$direction*[OPCIONAL]|Uma dos seguintes constantes **SQLSRV_PARAM_\*** usadas para indicar a direção do parâmetro: **SQLSRV_PARAM_IN**, **SQLSRV_PARAM_OUT**, **SQLSRV_PARAM_INOUT**. O valor padrão é **SQLSRV_PARAM_IN**.<br /><br />Para obter mais informações sobre constantes do PHP, consulte [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).|  
    |*$phpType*[OPCIONAL]|Uma constante **SQLSRV_PHPTYPE _\*** que especifica o tipo de dados do PHP do valor retornado.|  
    |*$sqlType*[OPCIONAL]|Uma constante **SQLSRV_SQLTYPE_\*** que especifica o tipo de dados do SQL Server do valor de entrada.|  
  
*$options* [OPTIONAL]: Uma matriz associativa que define as <a name="properties">propriedades da consulta</a>. A tabela a seguir lista as chaves compatíveis e os valores correspondentes:

|Chave|Valores com suporte|Descrição|  
|-------|--------------------|---------------|  
|ClientBufferMaxKBSize|Um inteiro positivo|Configura o tamanho do buffer que contém o conjunto de resultados de um cursor do lado do cliente.<br /><br />O padrão é 10240 KB. Para saber mais, veja como [especificar um tipo de cursor e selecionar linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).|
|DecimalPlaces|Um inteiro entre 0 e 4 (inclusive)|Especifica as casas decimais ao formatar valores monetários buscados.<br /><br />Qualquer inteiro negativo ou um valor maior que 4 será ignorado.<br /><br />Esta opção funcionará somente quando o FormatDecimals for **true**.|
|FormatDecimals|**true** ou **false**<br /><br />O valor padrão é **false**.|Especifica quando é apropriado adicionar zeros iniciais em cadeias de caracteres decimais e habilita a opção `DecimalPlaces` para a formatação de tipos monetários.<br /><br />Para saber mais, confira [Formatação de cadeias de caracteres decimais e valores monetários (driver SQLSRV)](../../connect/php/formatting-decimals-sqlsrv-driver.md).|
|QueryTimeout|Um inteiro positivo|Define o tempo limite da consulta em segundos. Por padrão, o driver aguarda resultados indefinidamente.|  
|ReturnDatesAsStrings|**true** ou **false**<br /><br />O valor padrão é **false**.|Configura a instrução para recuperar os tipos de data e hora como cadeia de caracteres (**true**). Para saber mais, leia [Como recuperar um tipo de data e hora como cadeias de caracteres usando o driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).
|Rolável|SQLSRV_CURSOR_FORWARD<br /><br />SQLSRV_CURSOR_STATIC<br /><br />SQLSRV_CURSOR_DYNAMIC<br /><br />SQLSRV_CURSOR_KEYSET<br /><br />SQLSRV_CURSOR_CLIENT_BUFFERED|Para obter mais informações sobre esses valores, consulte [Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).|  
|SendStreamParamsAtExec|**true** ou **false**<br /><br />O valor padrão é **true**.|Configura o driver para enviar todos os dados de fluxo na execução **true** ou para enviar dados de fluxo em partes (**false**). Por padrão, o valor é definido como **true**. Para obter mais informações, consulte [sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md).|  
  
## <a name="return-value"></a>Valor retornado  
Um recurso de instrução. Se não for possível criar o recurso de instrução, **false** será retornado.  
  
## <a name="remarks"></a>Comentários  
Quando você prepara uma instrução que usa variáveis como parâmetros, as variáveis são associadas à instrução. Isso significa que, se você atualizar os valores das variáveis, da próxima vez que executar a instrução, ela será executada com valores de parâmetros atualizados.  
  
A combinação de **sqlsrv_prepare** e **sqlsrv_execute** separa a preparação e a execução da instrução em duas chamadas de função e pode ser usada para executar consultas parametrizadas. Essa função é ideal para executar uma instrução várias vezes com valores de parâmetros diferentes para cada execução.  
  
Para obter estratégias alternativas para gravar e ler grandes quantidades de informações, consulte [Batches of SQL Statements](../../odbc/reference/develop-app/batches-of-sql-statements.md) e [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
Para obter mais informações, confira [Como recuperar parâmetros de saída usando o driver SQLSRV](../../connect/php/how-to-retrieve-output-parameters-using-the-sqlsrv-driver.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir prepara e executa uma instrução. A instrução, quando executada (veja [sqlsrv_execute](../../connect/php/sqlsrv-execute.md)), atualiza um campo na tabela *Sales.SalesOrderDetail* do banco de dados AdventureWorks. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Set up Transact-SQL query. */  
$tsql = "UPDATE Sales.SalesOrderDetail   
         SET OrderQty = ?   
         WHERE SalesOrderDetailID = ?";  
  
/* Assign parameter values. */  
$param1 = 5;  
$param2 = 10;  
$params = array(&$param1, &$param2);  
  
/* Prepare the statement. */  
if ($stmt = sqlsrv_prepare($conn, $tsql, $params)) {
    echo "Statement prepared.\n";  
} else {  
    echo "Statement could not be prepared.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement. */  
if (sqlsrv_execute($stmt)) {  
    echo "Statement executed.\n";  
} else {  
    echo "Statement could not be executed.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir demonstra como preparar uma instrução e executá-la novamente com valores de parâmetros diferentes. O exemplo a seguir atualiza a coluna *OrderQty* da tabela *Sales.SalesOrderDetail* no banco de dados AdventureWorks. Depois que as atualizações forem concluídas, o banco de dados será consultado para verificar se as atualizações foram bem-sucedidas. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Define the parameterized query. */  
$tsql = "UPDATE Sales.SalesOrderDetail  
         SET OrderQty = ?  
         WHERE SalesOrderDetailID = ?";  
  
/* Initialize parameters and prepare the statement. Variables $qty  
and $id are bound to the statement, $stmt1. */  
$qty = 0; $id = 0;  
$stmt1 = sqlsrv_prepare($conn, $tsql, array(&$qty, &$id));  
if ($stmt1) {  
    echo "Statement 1 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Set up the SalesOrderDetailID and OrderQty information. This array  
maps the order ID to order quantity in key=>value pairs. */  
$orders = array(1=>10, 2=>20, 3=>30);  
  
/* Execute the statement for each order. */  
foreach ($orders as $id => $qty) {  
    // Because $id and $qty are bound to $stmt1, their updated  
    // values are used with each execution of the statement.   
    if (sqlsrv_execute($stmt1) === false) {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
echo "Orders updated.\n";  
  
/* Free $stmt1 resources.  This allows $id and $qty to be bound to a different statement.*/  
sqlsrv_free_stmt($stmt1);  
  
/* Now verify that the results were successfully written by selecting   
the newly inserted rows. */  
$tsql = "SELECT OrderQty   
         FROM Sales.SalesOrderDetail   
         WHERE SalesOrderDetailID = ?";  
  
/* Prepare the statement. Variable $id is bound to $stmt2. */  
$stmt2 = sqlsrv_prepare($conn, $tsql, array(&$id));  
if ($stmt2) {  
    echo "Statement 2 prepared.\n";  
} else {  
    echo "Error in statement preparation.\n";  
    die(print_r(sqlsrv_errors(), true));  
}  
  
/* Execute the statement for each order. */  
foreach (array_keys($orders) as $id)  
{  
    /* Because $id is bound to $stmt2, its updated value   
    is used with each execution of the statement. */  
    if (sqlsrv_execute($stmt2)) {  
        sqlsrv_fetch($stmt2);  
        $quantity = sqlsrv_get_field($stmt2, 0);  
        echo "Order $id is for $quantity units.\n";  
    } else {  
        echo "Error in statement execution.\n";  
        die(print_r(sqlsrv_errors(), true));  
    }  
}  
  
/* Free $stmt2 and connection resources. */  
sqlsrv_free_stmt($stmt2);  
sqlsrv_close($conn);  
?>  
```  
  
> [!NOTE]
> É recomendável usar cadeias de caracteres como entradas ao associar valores a uma [coluna decimal ou numérica](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) a fim de garantir a precisão e a exatidão, pois o PHP tem uma precisão limitada para [números de ponto flutuante](https://php.net/manual/en/language.types.float.php). O mesmo se aplica a colunas bigint, principalmente quando os valores estão fora do intervalo de um [inteiro](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md).

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
$stmt = sqlsrv_prepare($conn, "INSERT INTO TestTable (DecimalCol) VALUES (?)", $params);
sqlsrv_execute($stmt);

sqlsrv_free_stmt($stmt);  
sqlsrv_close($conn);  

?>
```

## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Como: Executar consultas parametrizadas](../../connect/php/how-to-perform-parameterized-queries.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)

[Como: Enviar dados como um fluxo](../../connect/php/how-to-send-data-as-a-stream.md)

[Usando parâmetros direcionais](../../connect/php/using-directional-parameters.md)

[Recuperando dados](../../connect/php/retrieving-data.md)

[Atualizando dados &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)