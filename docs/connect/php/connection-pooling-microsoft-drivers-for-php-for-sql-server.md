---
title: Pool de conexões (Drivers da Microsoft para PHP para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 714a3436cc79f3568e14c5e2609e16fd408f288e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80900982"
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>Pool de conexões (Drivers da Microsoft para PHP para SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Veja a seguir pontos importantes a serem observados sobre o pool de conexões no [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]:  
  
-   O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] usa o pool de conexões do ODBC.  
  
-   Por padrão, o pool de conexões está habilitado no Windows. No Linux e no macOS, as conexões serão agrupadas somente se o pool de conexões estiver habilitado para ODBC (confira [Como habilitar/desabilitar o pool de conexões](#enablingdisabling-connection-pooling)). Quando o pool de conexões estiver habilitado e você se conectar a um servidor, o driver tentará usar uma conexão em pool antes de criar uma. Se uma conexão equivalente não for encontrada no pool, uma nova conexão será criada e adicionada a ele. O driver determina se as conexões são equivalentes com base em uma comparação de cadeias de conexão.  
  
-   Quando uma conexão do pool é usada, o estado da conexão é redefinido.  
  
-   O fechamento da conexão retorna a conexão ao pool.  
  
Confira mais informações sobre o pool de conexão em [Pool de conexões do Gerenciador de Driver](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="enablingdisabling-connection-pooling"></a>Como habilitar/desabilitar o pool de conexões
### <a name="windows"></a>Windows
Você pode forçar o driver a criar uma nova conexão (em vez de procurar uma conexão equivalente no pool de conexões), definindo o valor do atributo *ConnectionPooling* na cadeia de conexão como **false** (ou 0).  
  
Se o atributo *ConnectionPooling* for omitido da cadeia de conexão ou se for definido como **true** (ou 1), o driver criará uma nova conexão somente se não existir uma conexão equivalente no pool.  
  
Para obter mais informações sobre outros atributos de conexão, consulte [Connection Options](../../connect/php/connection-options.md).  
### <a name="linux-and-macos"></a>Linux e macOS
O atributo *ConnectionPooling* não pode ser usado para habilitar/desabilitar o pool de conexões. 

O pool de conexões pode ser habilitado/desabilitado pela edição do arquivo de configuração odbcinst.ini. O driver deve ser recarregado para que as alterações entrem em vigor.

A configuração de `Pooling` como `Yes` e de um valor `CPTimeout` positivo no arquivo odbcinst.ini habilita o pool de conexões. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
  
Resumidamente, o arquivo odbcinst.ini deve ser semelhante a este exemplo:

```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
Description=Microsoft ODBC Driver 13 for SQL Server
Driver=/opt/microsoft/msodbcsql/lib64/libmsodbcsql-13.1.so.3.0
UsageCount=1
CPTimeout=120
```

Configurar `Pooling` como `No` no arquivo odbcinst.ini força o driver a criar uma conexão.
```
[ODBC]
Pooling=No
```

## <a name="remarks"></a>Comentários
- No Linux ou no macOS, todas as conexões serão agrupadas se o pool estiver habilitado no arquivo odbcinst.ini. Isso significa que a opção de conexão ConnectionPooling não tem nenhum efeito. Para desabilitar o pool, defina Pooling=No no arquivo odbcinst.ini e recarregue os drivers.
  - unixODBC <= 2.3.4 (Linux e macOS) pode não retornar informações de diagnóstico apropriadas, como mensagens de erro, avisos e mensagens informativas
  - por esse motivo, os drivers SQLSRV e PDO_SQLSRV podem não conseguir buscar corretamente dados longos (por exemplo, XML, binários) como cadeias de caracteres. Como uma solução alternativa, os dados longos podem ser obtidos como fluxos. Veja o exemplo abaixo para SQLSRV.

```
<?php
$connectionInfo = array("Database"=>"test", "UID"=>"username", "PWD"=>"password");

$conn1 = sqlsrv_connect("servername", $connectionInfo);

$longSample = str_repeat("a", 8500);
$xml1 = 
'<ParentXMLTag>
  <ChildTag01>'.$longSample.'</ChildTag01>
</ParentXMLTag>';

// Create table and insert xml string into it
sqlsrv_query($conn1, "CREATE TABLE xml_table (field xml)");
sqlsrv_query($conn1, "INSERT into xml_table values ('$xml1')");

// retrieve the inserted xml
$column1 = getColumn($conn1);

// return the connection to the pool
sqlsrv_close($conn1);

// This connection is from the pool
$conn2 = sqlsrv_connect("servername", $connectionInfo);
$column2 = getColumn($conn2);

sqlsrv_query($conn2, "DROP TABLE xml_table");
sqlsrv_close($conn2);

function getColumn($conn)
{
    $tsql = "SELECT * from xml_table";
    $stmt = sqlsrv_query($conn, $tsql);
    sqlsrv_fetch($stmt);
    // This might fail in Linux and macOS
    // $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STRING(SQLSRV_ENC_CHAR));
    // The workaround is to fetch it as a stream
    $column = sqlsrv_get_field($stmt, 0, SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_CHAR));
    sqlsrv_free_stmt($stmt);
    return ($column);
}
?>
```


## <a name="see-also"></a>Consulte Também  
[Como se conectar usando a Autenticação do Windows](../../connect/php/how-to-connect-using-windows-authentication.md)

[Como se conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
