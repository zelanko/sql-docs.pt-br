---
title: sqlsrv_connect | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
caps.latest.revision: 67
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e9491e2b0721f7c7a2ca6b5ed37c52135a4c760
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvconnect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cria um recurso de conexão e abre uma conexão. Por padrão, a conexão será tentada usando a Autenticação do Windows.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$serverName*: uma cadeia de caracteres especificando o nome do servidor com o qual uma conexão está sendo estabelecida. Um nome de instância (por exemplo, "meuServidor\NomedaInstância") ou número de porta (por exemplo, "meuServidor, 1521") pode ser incluído como parte da cadeia de caracteres. Para obter uma descrição completa das opções disponíveis para esse parâmetro, consulte a palavra-chave Servidor na seção Palavras-chave da cadeia de conexão do driver ODBC de [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](http://go.microsoft.com/fwlink/?LinkId=105504).  
  
A partir da versão 3.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], você também pode especificar uma instância LocalDB com `"(localdb)\instancename"`. Para obter mais informações, consulte [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).  
  
A partir da versão 3.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], também é possível especificar um nome de rede virtual para se conectar a um grupo de disponibilidade AlwaysOn. Para obter mais informações sobre o suporte do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], consulte [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(Driver do PHP para o suporte do SQL Server para alta disponibilidade e recuperação de desastre).  
  
*$connectionInfo* [opcional]: uma associação **matriz** que contém atributos de conexão (por exemplo, **matriz**("Database" = > "AdventureWorks")). Consulte [Connection Options](../../connect/php/connection-options.md) para obter uma lista das chaves com suporte para a matriz.  
  
## <a name="return-value"></a>Valor de retorno  
Um recurso de conexão PHP. Se uma conexão não puder ser criada e aberta com êxito, **false** será retornado.  
  
## <a name="remarks"></a>Comentários  
Se os valores das chaves *UID* e *PWD* não forem especificadas no parâmetro *$connectionInfo* opcional, a conexão será tentada usando a Autenticação do Windows. Para obter mais informações sobre como se conectar ao servidor, consulte [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) e [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria e abre uma conexão usando a Autenticação do Windows. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](http://www.codeplex.com/SqlServerSamples) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*  
Connect to the local server using Windows Authentication and specify  
the AdventureWorks database as the database in use. To connect using  
SQL Server Authentication, set values for the "UID" and "PWD"  
 attributes in the $connectionInfo parameter. For example:  
$connectionInfo = array("UID" => $uid, "PWD" => $pwd, "Database"=>"AdventureWorks");  
*/  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if( $conn )  
{  
     echo "Connection established.\n";  
}  
else  
{  
     echo "Connection could not be established.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)  
[Connecting to the Server](../../connect/php/connecting-to-the-server.md)  
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  

