---
title: sqlsrv_connect | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_connect
apitype: NA
helpviewer_keywords:
- connecting to the server
- API Reference, sqlsrv_connect
- connection pooling support
- sqlsrv_connect
ms.assetid: 37836b49-258e-45ce-9549-b8bd85d6952d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1804d84913a97c114dddf3ae3cbb6e401f4fa949
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80902734"
---
# <a name="sqlsrv_connect"></a>sqlsrv_connect
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Cria um recurso de conexão e abre uma conexão. Por padrão, a conexão será tentada usando a Autenticação do Windows.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_connect( string $serverName [, array $connectionInfo])  
```  
  
#### <a name="parameters"></a>parâmetros  
*$serverName*: uma cadeia de caracteres especificando o nome do servidor com o qual uma conexão está sendo estabelecida. Um nome de instância (por exemplo, "meuServidor\NomedaInstância") ou número de porta (por exemplo, "meuServidor, 1521") pode ser incluído como parte da cadeia de caracteres. Para obter uma descrição completa das opções disponíveis para esse parâmetro, confira a palavra-chave Servidor na seção Palavras-chave da cadeia de conexão do Driver ODBC de [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
A partir da versão 3.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], você também pode especificar uma instância LocalDB com `"(localdb)\instancename"`. Para obter mais informações, confira [Suporte para LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md).  
  
A partir da versão 3.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], também é possível especificar um nome de rede virtual para se conectar a um grupo de disponibilidade AlwaysOn. Para obter mais informações sobre o suporte do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] para [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], confira [Suporte para alta disponibilidade, recuperação de desastre](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).  
  
*$connectionInfo* [OPCIONAL]: uma **matriz** associativa que contém atributos de conexão (por exemplo, **matriz**("Database" => "AdventureWorks")). Consulte [Connection Options](../../connect/php/connection-options.md) para obter uma lista das chaves com suporte para a matriz.  
  
## <a name="return-value"></a>Valor retornado  
Um recurso de conexão PHP. Se uma conexão não puder ser criada e aberta com êxito, **false** será retornado.  
  
## <a name="remarks"></a>Comentários  
Se os valores das chaves *UID* e *PWD* não forem especificadas no parâmetro *$connectionInfo* opcional, a conexão será tentada usando a Autenticação do Windows. Para obter mais informações sobre como se conectar ao servidor, consulte [How to: Connect Using Windows Authentication](../../connect/php/how-to-connect-using-windows-authentication.md) e [How to: Connect Using SQL Server Authentication](../../connect/php/how-to-connect-using-sql-server-authentication.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria e abre uma conexão usando a Autenticação do Windows. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://www.codeplex.com/SqlServerSamples) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
