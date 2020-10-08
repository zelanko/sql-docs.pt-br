---
description: sqlsrv_field_metadata
title: sqlsrv_field_metadata | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5629096fb59bbb081aa535e8e3436a4cb06130d8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726711"
---
# <a name="sqlsrv_field_metadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera metadados para os campos de uma instrução preparada. Para obter informações sobre como preparar uma instrução, consulte [sqlsrv_query](../../connect/php/sqlsrv-query.md) ou [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md). Observe que **sqlsrv_field_metadata** pode ser chamado em qualquer instrução preparada, antes ou após a execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: um recurso de instrução para o qual os metadados de campo são pesquisados.  
  
## <a name="return-value"></a>Valor de retorno  
Uma **matriz** de matrizes ou **false**. A matriz consiste em uma matriz para cada campo no conjunto de resultados. Cada submatriz tem chaves, conforme descrito na tabela a seguir. Se ocorrer um erro na recuperação de metadados do campo, será retornado **false** .  
  
|Chave|Descrição|  
|-------|---------------|  
|Nome|Nome da coluna correspondente ao campo.|  
|Type|Valor numérico que corresponde a um tipo SQL.|  
|Tamanho|Número de caracteres de campos do tipo character (char(n), varchar(n), nchar(n), nvarchar(n), XML). Número de bytes para campos do tipo binary (binary(n), varbinary(n), UDT). **NULL** para outros tipos de dados do SQL Server.|  
|Precisão|A precisão dos tipos de precisão variável (real, numeric, decimal, datetime2, datetimeoffset e time). **NULL** para outros tipos de dados do SQL Server.|  
|Escala|A escala dos tipos de escala variável (numeric, decimal, datetime2, datetimeoffset e time). **NULL** para outros tipos de dados do SQL Server.|  
|Nullable|Um valor enumerado que indica se a coluna é anulável (**SQLSRV_NULLABLE_YES**), não anulável (**SQLSRV_NULLABLE_NO**) ou se não se sabe se a coluna é anulável (**SQLSRV_NULLABLE_UNKNOWN**).|  
  
A tabela a seguir fornece mais informações sobre as chaves para cada submatriz (consulte a documentação do SQL Server para obter mais informações sobre esses tipos):  
  
|Tipos de dados do SQL Server 2008|Type|Precisão mínima/máxima|Escala mínima/máxima|Tamanho|  
|-----------------------------|--------|----------------------|------------------|--------|  
|BIGINT|SQL_BIGINT (-5)|||8|  
|binary|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT (-7)||||  
|char|SQL_CHAR (1)|||0 < *n* < 8000 <sup>1</sup>|  
|Data|SQL_TYPE_DATE (91)|10/10|0/0||  
|DATETIME|SQL_TYPE_TIMESTAMP (93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP (93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET (-155)|26/34|0/7||  
|decimal|SQL_DECIMAL (3)|1/38|0/valor da precisão||  
|FLOAT|SQL_FLOAT (6)|4/8|||  
|image|SQL_LONGVARBINARY (-4)|||2 GB|  
|INT|SQL_INTEGER (4)||||  
|money|SQL_DECIMAL (3)|19/19|4/4||  
|NCHAR|SQL_WCHAR (-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR (-10)|||1 GB|  
|numeric|SQL_NUMERIC (2)|1/38|0/valor da precisão||  
|NVARCHAR|SQL_WVARCHAR (-9)|||0 < *n* < 4000 <sup>1</sup>|  
|real|SQL_REAL (7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP (93)|16/16|0/0||  
|SMALLINT|SQL_SMALLINT (5)|||2 bytes|  
|Smallmoney|SQL_DECIMAL (3)|10/10|4/4||  
|sql_variant|SQL_SS_VARIANT (-150)|||variável|  
|texto|SQL_LONGVARCHAR (-1)|||2 GB|  
|time|SQL_SS_TIME2 (-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8 bytes|  
|TINYINT|SQL_TINYINT (-6)|||1 byte|  
|udt|SQL_SS_UDT (-151)|||variável|  
|UNIQUEIDENTIFIER|SQL_GUID (-11)|||16|  
|varbinary|SQL_VARBINARY (-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR (12)|||0 < *n* < 8000 <sup>1</sup>|  
|Xml|SQL_SS_XML (-152)|||0|  
  
(1) Zero (0) indica que o tamanho máximo é permitido.  
  
A chave Nullable pode ser yes ou no.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria um recurso de instrução. Em seguida, recupera e exibe os metadados de campo. O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) estejam instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```
<?php
/* Connect to the local server using Windows Authentication and
specify the AdventureWorks database as the database in use. */
$serverName = "(local)";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect.\n";
    die( print_r( sqlsrv_errors(), true));
}

/* Prepare the statement. */
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";
$stmt = sqlsrv_prepare( $conn, $tsql);
  
/* Get and display field metadata. */
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata) {
    foreach( $fieldMetadata as $name => $value) {
        echo "$name: $value\n";
    }  
    echo "\n";
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement
resource, pre- or post-execution. */
  
/* Free statement and connection resources. */
sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="sensitivity-data-classification-metadata"></a>Metadados de classificação de dados de confidencialidade

Uma nova opção `DataClassification` foi introduzida na versão 5.8.0 para os usuários acessarem os [metadados de classificação de dados de confidencialidade](../../relational-databases/security/sql-data-discovery-and-classification.md?tabs=t-sql&view=sql-server-ver15#subheading-4) no Microsoft SQL Server 2019 usando o `sqlsrv_field_metadata`, que requer o Microsoft ODBC Driver 17.4.2 ou posterior.

Por padrão, a opção `DataClassification` é `false`, porém, quando definido como `true`, a matriz mencionada anteriormente como `sqlsrv_field_metadata` será preenchida com os metadados de classificação de dados de confidencialidade, se existirem. 

Pegue a tabela de Pacientes, por exemplo:

```
CREATE TABLE Patients 
      [PatientId] int identity,
      [SSN] char(11),
      [FirstName] nvarchar(50),
      [LastName] nvarchar(50),
      [BirthDate] date)
```

Podemos classificar as colunas SSN e BirthDate, como mostrado abaixo:

```
ADD SENSITIVITY CLASSIFICATION TO [Patients].SSN WITH (LABEL = 'Highly Confidential - secure privacy', INFORMATION_TYPE = 'Credentials')
ADD SENSITIVITY CLASSIFICATION TO [Patients].BirthDate WITH (LABEL = 'Confidential Personal Data', INFORMATION_TYPE = 'Birthdays')
```

Para acessar os metadados, invoque `sqlsrv_field_metadata`, como mostrado no trecho abaixo:

```
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = sqlsrv_prepare($conn, $tsql, array(), array('DataClassification' => true));
if (sqlsrv_execute($stmt)) {
    $fieldmeta = sqlsrv_field_metadata($stmt);

    foreach ($fieldmeta as $f) {
        if (count($f['Data Classification']) > 0) {
            echo $f['Name'] . ": \n";
            print_r($f['Data Classification']); 
        }
    }
}
```

A saída será:

```
SSN: 
Array
(
    [0] => Array
        (
            [Label] => Array
                (
                    [name] => Highly Confidential - secure privacy
                    [id] => 
                )

            [Information Type] => Array
                (
                    [name] => Credentials
                    [id] => 
                )

        )

)
BirthDate: 
Array
(
    [0] => Array
        (
            [Label] => Array
                (
                    [name] => Confidential Personal Data
                    [id] => 
                )

            [Information Type] => Array
                (
                    [name] => Birthdays
                    [id] => 
                )

        )

)
```

Se estiver usando `sqlsrv_query` em vez de `sqlsrv_prepare`, o trecho acima poderá ser modificado, desta forma:

```
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $tsql, array(), array('DataClassification' => true));
$fieldmeta = sqlsrv_field_metadata($stmt);

foreach ($fieldmeta as $f) {
    $jstr = json_encode($f);
    echo $jstr . PHP_EOL;
}
```

Como você pode ver na representação JSON abaixo, os metadados de classificação de dados são exibidos se associados às colunas:

```
{"Name":"PatientId","Type":4,"Size":null,"Precision":10,"Scale":null,"Nullable":0,"Data Classification":[]}
{"Name":"SSN","Type":1,"Size":11,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""}}]}
{"Name":"FirstName","Type":-9,"Size":50,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[]}
{"Name":"LastName","Type":-9,"Size":50,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[]}
{"Name":"BirthDate","Type":91,"Size":null,"Precision":10,"Scale":0,"Nullable":1,"Data Classification":[{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""}}]}
```

## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  

[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
