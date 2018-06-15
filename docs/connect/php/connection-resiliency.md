---
title: Resiliência de Conexão ociosa
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.openlocfilehash: 250e4e6334a31d760c8fcb3e1e571ec1a726d020
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307255"
---
# <a name="idle-connection-resiliency"></a>Resiliência de Conexão ociosa
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[Resiliência de Conexão](https://msdn.microsoft.com/library/dn632678.aspx) é o princípio de que uma conexão ociosa quebrada possa ser restabelecido, de acordo com determinadas restrições. Se uma conexão para o Microsoft SQL Server falhar, a resiliência de conexão permite que o cliente tentará automaticamente restabelecer a conexão. Resiliência de Conexão é uma propriedade da fonte de dados; somente SQL Server 2014 e versões posterior e banco de dados SQL do Azure oferecem suporte a resiliência de conexão.

Resiliência de Conexão é implementada com duas conexão palavras-chave que podem ser adicionadas em cadeias de caracteres de conexão: **ConnectRetryCount** e **ConnectRetryInterval**.

|Palavra-chave|Valores|Padrão|Description|
|-|-|-|-|
|**ConnectRetryCount**| Número inteiro entre 0 e 255 (inclusive)|1|O número máximo de tentativas de restabelecer uma conexão interrompida antes de desistir. Por padrão, um único tenta restabelecer uma conexão quando quebrado. Um valor de 0 significa que nenhum reconexão será tentada.|
|**ConnectRetryInterval**| Número inteiro entre 1 e 60 (inclusivo)|1| O tempo, em segundos, entre as tentativas de restabelecer uma conexão. O aplicativo tentará reconectar-se imediatamente ao detectar uma conexão interrompida e, em seguida, aguardará **ConnectRetryInterval** segundos antes de tentar novamente. Esta palavra-chave será ignorado se **ConnectRetryCount** é igual a 0.

Se o produto de **ConnectRetryCount** multiplicado por **ConnectRetryInterval** é maior do que **LoginTimeout**, em seguida, o cliente deixará de tentar se conectar de uma vez  **LoginTimeout** for atingido; caso contrário, ele continuará a tentar se reconectar até **ConnectRetryCount** for atingido.

#### <a name="remarks"></a>Remarks

Resiliência de Conexão se aplica quando a conexão estiver ociosa. Falhas que ocorrem durante a execução de uma transação, por exemplo, não vai disparar tentativas de reconexão – eles falharão, pois caso contrário, deve ser esperado. As seguintes situações, conhecidas como estados de sessão não recuperável, não vai disparar tentativas de reconexão:

* Tabelas temporárias
* Cursores globais e locais
* Bloqueios de nível de transação de contexto e a sessão de transação
* Bloqueios de aplicativo
* EXECUTE AS / REVERTER o contexto de segurança
* Identificadores de automação OLE
* Identificadores XML preparados
* Sinalizadores de rastreamento

## <a name="example"></a>Exemplo

O código a seguir se conecta a um banco de dados e executa uma consulta. A conexão for interrompida, eliminando a sessão e uma nova consulta é tentada usando a conexão interrompida. Este exemplo usa o [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) banco de dados de exemplo.

Neste exemplo, podemos especificar um cursor em buffer antes de dividir a conexão. Se não especificamos um cursor em buffer, a conexão não será restabelecida porque seria um cursor do lado do servidor ativo e, portanto, a conexão não seria ocioso quando quebrado. No entanto, nesse caso, podemos chamar sqlsrv_free_stmt() antes de dividir a conexão para liberação de cursor e a conexão deve ser restabelecida com êxito.

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
Saída esperada:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>Consulte também
[Resiliência de conexão no driver ODBC do Windows](https://docs.microsoft.com/en-us/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)
