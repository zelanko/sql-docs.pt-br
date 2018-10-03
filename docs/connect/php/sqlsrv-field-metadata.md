---
title: sqlsrv_field_metadata | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c030a6a3d2ba5caad755abfd92a5cf1adb01cc25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748504"
---
# <a name="sqlsrvfieldmetadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera metadados para os campos de uma instrução preparada. Para obter informações sobre como preparar uma instrução, consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Observe que **sqlsrv_field_metadata** pode ser chamado em qualquer instrução preparada, antes ou após a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: um recurso de instrução para o qual os metadados de campo são pesquisados.  
  
## <a name="return-value"></a>Valor retornado  
Uma **matriz** de matrizes ou **false**. A matriz consiste em uma matriz para cada campo no conjunto de resultados. Cada submatriz tem chaves, conforme descrito na tabela a seguir. Se ocorrer um erro na recuperação de metadados do campo, será retornado **false** .  
  
|Chave|Descrição|  
|-------|---------------|  
|Nome|Nome da coluna correspondente ao campo.|  
|Tipo|Valor numérico que corresponde a um tipo SQL.|  
|Tamanho|Número de caracteres de campos do tipo character (char(n), varchar(n), nchar(n), nvarchar(n), XML). Número de bytes para campos do tipo binary (binary(n), varbinary(n), UDT). **NULL** para outros tipos de dados do SQL Server.|  
|Precisão|A precisão dos tipos de precisão variável (real, numeric, decimal, datetime2, datetimeoffset e time). **NULL** para outros tipos de dados do SQL Server.|  
|Escala|A escala dos tipos de escala variável (numeric, decimal, datetime2, datetimeoffset e time). **NULL** para outros tipos de dados do SQL Server.|  
|Anulável|Um valor enumerado que indica se a coluna é anulável (**SQLSRV_NULLABLE_YES**), não anulável (**SQLSRV_NULLABLE_NO**) ou se não se sabe se a coluna é anulável (**SQLSRV_NULLABLE_UNKNOWN**).|  
  
A tabela a seguir fornece mais informações sobre as chaves para cada submatriz (consulte a documentação do SQL Server para obter mais informações sobre esses tipos):  
  
|Tipos de dados do SQL Server 2008|Tipo|Precisão mínima/máxima|Escala mínima/máxima|Tamanho|  
|-----------------------------|--------|----------------------|------------------|--------|  
|BIGINT|SQL_BIGINT (-5)|||8|  
|BINARY|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|Data|SQL_TYPE_DATE (91)|10/10|0/0||  
|DATETIME|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|Decimal|SQL_DECIMAL (3)|1/38|0/valor da precisão||  
|FLOAT|SQL_FLOAT (6)|4/8|||  
|image|SQL_LONGVARBINARY (-4)|||2 GB|  
|INT|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|NCHAR|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|NUMERIC|SQL_NUMERIC (2)|1/38|0/valor da precisão||  
|NVARCHAR|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|REAL|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|SMALLINT|SQL_SMALLINT (5)|||2 bytes|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|text|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8 bytes|  
|tinyint|SQL_TINYINT (-6)|||1 byte|  
|udt|SQL_SS_UDT (-151)|||variável|  
|UNIQUEIDENTIFIER|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|xml|SQL_SS_XML (-152)|||0|  
  
(1) Zero (0) indica que o tamanho máximo é permitido.  
  
A chave Nullable pode ser yes ou no.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria um recurso de instrução. Em seguida, recupera e exibe os metadados de campo. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Prepare the statement. */  
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";  
$stmt = sqlsrv_prepare( $conn, $tsql);  
  
/* Get and display field metadata. */  
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata)  
{  
      foreach( $fieldMetadata as $name => $value)  
      {  
           echo "$name: $value\n";  
      }  
      echo "\n";  
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement  
resource, pre- or post-execution. */  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  
