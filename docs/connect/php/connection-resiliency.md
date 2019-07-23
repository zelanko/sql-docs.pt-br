---
title: Resiliência da Conexão Ociosa
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265175"
---
# <a name="idle-connection-resiliency"></a>Resiliência da Conexão Ociosa
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

A [resiliência da conexão](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) é o princípio de que uma conexão ociosa desfeita pode ser restabelecida, dentro de determinadas restrições. Se uma conexão com o Microsoft SQL Server falhar, a resiliência de conexão permitirá que o cliente tente restabelecer a conexão automaticamente. A resiliência da conexão é uma propriedade da fonte de dados; somente SQL Server 2014 e posterior e o banco de dados SQL do Azure dão suporte à resiliência de conexão.

A resiliência de conexão é implementada com duas palavras-chave de conexão que podem ser adicionadas às cadeias de conexão: **ConnectRetryCount** e **ConnectRetryInterval**.

|Palavra-chave|Valores|Padrão|Descrição|
|-|-|-|-|
|**ConnectRetryCount**| Um inteiro entre 0 e 255 (inclusive)|1|O número máximo de tentativas de restabelecer uma conexão interrompida antes de desistir. Por padrão, uma única tentativa é feita para restabelecer uma conexão quando quebrada. Um valor de 0 significa que nenhuma nova conexão será tentada.|
|**ConnectRetryInterval**| Um inteiro entre 1 e 60 (inclusive)|1| O tempo, em segundos, entre as tentativas de restabelecer uma conexão. O aplicativo tentará se reconectar imediatamente após a detecção de uma conexão interrompida e, em seguida, aguardará **ConnectRetryInterval** segundos antes de tentar novamente. Essa palavra-chave será ignorada se **ConnectRetryCount** for igual a 0.

Se o produto de **ConnectRetryCount** multiplicado por **ConnectRetryInterval** for maior que **LoginTimeout**, o cliente deixará de tentar se conectar quando o **LoginTimeout** for atingido; caso contrário, ele continuará a tentar se reconectar até que **ConnectRetryCount** seja atingido.

#### <a name="remarks"></a>Remarks

A resiliência da conexão se aplica quando a conexão está ociosa. As falhas que ocorrem durante a execução de uma transação, por exemplo, não dispararão tentativas de reconexão-elas falharão, como seria esperado. As seguintes situações, conhecidas como Estados de sessão não recuperáveis, não disparam tentativas de reconexão:

* Tabelas temporárias
* Cursores globais e locais
* Bloqueios de transação de nível de sessão e de contexto de transação
* Bloqueios de aplicativo
* EXECUTAR como/reverter contexto de segurança
* Identificadores de automação OLE
* Identificadores XML preparados
* Sinalizadores de rastreamento

## <a name="example"></a>Exemplo

O código a seguir se conecta a um banco de dados e executa uma consulta. A conexão é interrompida finalizando a sessão e uma nova consulta é tentada usando a conexão interrompida. Este exemplo usa o banco de dados [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) de exemplo.

Neste exemplo, especificamos um cursor em buffer antes de dividir a conexão. Se não especificarmos um cursor em buffer, a conexão não seria restabelecida porque haveria um cursor ativo no lado do servidor e, portanto, a conexão não estaria ociosa quando interrompida. No entanto, nesse caso, poderíamos chamar sqlsrv_free_stmt () antes de dividir a conexão para esvaziar o cursor e a conexão seria restabelecida com êxito.

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

## <a name="see-also"></a>Consulte Também
[Resiliência de conexão no driver ODBC do Windows](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
