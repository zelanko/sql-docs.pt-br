---
title: sqlsrv_get_field | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_field
apitype: NA
helpviewer_keywords:
- sqlsrv_get_field
- API Reference, sqlsrv_get_field
- retrieving data, as a single field
ms.assetid: fa17cc56-fb38-433b-a40d-65642f04dc23
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a5f94566cf965cfe135a17eed216cf8ee4b42b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618674"
---
# <a name="sqlsrvgetfield"></a>sqlsrv_get_field
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera dados do campo especificado da linha atual. Os dados de campo devem ser acessados em sequência. Por exemplo, dados do primeiro campo não podem ser acessados depois que o segundo campo de dados tiver sido acessado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sqlsrv_get_field( resource $stmt, int $fieldIndex [, int $getAsType])  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: um recurso de instrução correspondente a uma instrução executada.  
  
*$fieldIndex*: o índice do campo a ser recuperado. Os índices começam em zero.  
  
*$getAsType* [OPCIONAL]: uma constante **SQLSRV** (**SQLSRVPHPTYPE_&#x2a;**) que determina o tipo de dados do PHP para os dados retornados. Para obter informações sobre os tipos de dados compatíveis, consulte [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md). Se nenhum tipo de retorno for especificado, será retornado um tipo do PHP padrão. Para obter informações sobre tipos do PHP padrão, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md). Para obter informações sobre especificação de tipos de dados do PHP padrão, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="return-value"></a>Valor retornado  
Os dados do campo. Você pode especificar o tipo de dados  do PHP dos dados retornados usando o parâmetro *$getAsType* . Se nenhum tipo de dados de retorno for especificado, será retornado um tipo de dados do PHP padrão. Para obter informações sobre tipos do PHP padrão, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md). Para obter informações sobre especificação de tipos de dados do PHP padrão, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="remarks"></a>Remarks  
A combinação de **sqlsrv_fetch** e **sqlsrv_get_field** fornece acesso somente de encaminhamento aos dados.  
  
A combinação de **sqlsrv_fetch**/**sqlsrv_get_field** carrega apenas um campo de um conjunto de resultados de linha na memória do script e permite a especificação do tipo de retorno do PHP. (Para obter informações sobre como retornar o tipo de dados do PHP, veja [Como especificar tipos de dados do PHP](../../connect/php/how-to-specify-php-data-types.md).) Essa combinação de funções também permite que os dados sejam recuperados como um fluxo. (Para obter informações sobre como recuperar dados como um fluxo, veja [Recuperando dados como um fluxo usando o driver SQLSRV](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md).)  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera uma linha de dados que contém uma revisão do produto e o nome do revisor. Para recuperar dados do conjunto de resultados, **sqlsrv_get_field** é usado. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set up and execute the query. Note that both ReviewerName and  
Comments are of the SQL Server nvarchar type. */  
$tsql = "SELECT ReviewerName, Comments   
         FROM Production.ProductReview  
         WHERE ProductReviewID=1";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in statement preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Make the first row of the result set available for reading. */  
if( sqlsrv_fetch( $stmt ) === false )  
{  
     echo "Error in retrieving row.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Note: Fields must be accessed in order.  
Get the first field of the row. Note that no return type is  
specified. Data will be returned as a string, the default for  
a field of type nvarchar.*/  
$name = sqlsrv_get_field( $stmt, 0);  
echo "$name: ";  
  
/*Get the second field of the row as a stream.  
Because the default return type for a nvarchar field is a  
string, the return type must be specified as a stream. */  
$stream = sqlsrv_get_field( $stmt, 1,   
                            SQLSRV_PHPTYPE_STREAM( SQLSRV_ENC_CHAR));  
while( !feof( $stream))  
{   
    $str = fread( $stream, 10000);  
    echo $str;  
}  
  
/* Free the statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Recuperando dados](../../connect/php/retrieving-data.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
