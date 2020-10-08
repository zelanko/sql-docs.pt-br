---
title: PDOStatement::getColumnMeta
description: Referência de API para a função PDOStatement::getColumnMeta no Driver do Microsoft PDO_SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 58b6882fe4f0fce4ddf948121cb6ad35e5828fd7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726737"
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera metadados para uma coluna.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$conn*: (inteiro) o número da coluna, com base em zero, cujos metadados você deseja recuperar.  
  
## <a name="return-value"></a>Valor de retorno  
Uma matriz associativa (chave e valor) que contém os metadados da coluna. Consulte a seção de comentários para obter uma descrição dos campos na matriz.  
  
## <a name="remarks"></a>Comentários  
A tabela a seguir descreve os campos na matriz retornada por getColumnMeta.  
  
|NOME|VALUES|  
|--------|----------|  
|native_type|Especifica o tipo do PHP para a coluna. Sempre cadeia de caracteres.|  
|driver:decl_type|Especifica o tipo do SQL usado para representar o valor da coluna no banco de dados. Se a coluna no conjunto de resultados é o resultado de uma função, esse valor não é retornado por PDOStatement::getColumnMeta.|  
|sinalizadores|Especifica os sinalizadores definidos para essa coluna. Sempre 0.|  
|name|Especifica o nome da coluna no banco de dados.|  
|table|Especifica o nome da tabela que contém a coluna no banco de dados. Sempre em branco.|  
|len|Especifica o comprimento da coluna.|  
|precisão|Especifica a precisão numérica dessa coluna.|  
|pdo_type|Especifica o tipo desta coluna, conforme representado pelas constantes PDO::PARAM_ *. Sempre PDO::PARAM_STR (2).|  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="sensitivity-data-classification-metadata"></a>Metadados de classificação de dados de confidencialidade

A partir da versão 5.8.0, um novo atributo de instrução `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` está disponível para os usuários acessarem os [metadados de classificação de dados de confidencialidade](../../relational-databases/security/sql-data-discovery-and-classification.md?tabs=t-sql&view=sql-server-ver15#subheading-4) no Microsoft SQL Server 2019 usando o `PDOStatement::getColumnMeta`, que requer o Microsoft ODBC Driver 17.4.2 ou posterior.

Observe que o atributo `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` é `false` por padrão, porém, quando definido como `true`, o campo de matriz mencionado anteriormente, `flags`, será preenchido com os metadados de classificação de dados de confidencialidade, se existirem. 

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

Para acessar os metadados, use `PDOStatement::getColumnMeta` depois de definir `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` como true, como mostrado no seguinte trecho:

```
$options = array(PDO::SQLSRV_ATTR_DATA_CLASSIFICATION => true);
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = $conn->prepare($tsql, $options);
$stmt->execute();
$numCol = $stmt->columnCount();

for ($i = 0; $i < $numCol; $i++) {
    $metadata = $stmt->getColumnMeta($i);
    $jstr = json_encode($metadata);
    echo $jstr . PHP_EOL;
}
```

A saída de metadados para todas as colunas é:

```
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"int identity","native_type":"string","table":"","pdo_type":2,"name":"PatientId","len":10,"precision":0}
{"flags":{"Data Classification":[{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""}}]},"sqlsrv:decl_type":"char","native_type":"string","table":"","pdo_type":2,"name":"SSN","len":11,"precision":0}
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"FirstName","len":50,"precision":0}
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"LastName","len":50,"precision":0}
{"flags":{"Data Classification":[{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""}}]},"sqlsrv:decl_type":"date","native_type":"string","table":"","pdo_type":2,"name":"BirthDate","len":10,"precision":0}
```

Se modificarmos o trecho acima definindo `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` como `false` (o caso padrão), o campo `flags` sempre será `0` como antes, desta forma:

```
{"flags":0,"sqlsrv:decl_type":"int identity","native_type":"string","table":"","pdo_type":2,"name":"PatientId","len":10,"precision":0}
{"flags":0,"sqlsrv:decl_type":"char","native_type":"string","table":"","pdo_type":2,"name":"SSN","len":11,"precision":0}
{"flags":0,"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"FirstName","len":50,"precision":0}
{"flags":0,"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"LastName","len":50,"precision":0}
{"flags":0,"sqlsrv:decl_type":"date","native_type":"string","table":"","pdo_type":2,"name":"BirthDate","len":10,"precision":0}
```

      
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
