---
title: sqlsrv_fetch_object | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- sqlsrv_fetch_object
apitype: NA
helpviewer_keywords:
- sqlsrv_fetch_object
- API Reference, sqlsrv_fetch_object
- retrieving data, as an object
ms.assetid: 4ce2df2c-083a-4a4d-a1e2-e866e63707d5
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87477c1d30607d71e49729f73105905a2f64767a
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="sqlsrvfetchobject"></a>sqlsrv_fetch_object
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera a próxima linha de dados como um objeto do PHP.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sqlsrv_fetch_object( resource $stmt [, string $className [, array $ctorParams[, row[, ]offset]]])  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$stmt*: um recurso de instrução correspondente a uma instrução executada.  
  
*$className* [opcional]: uma cadeia de caracteres especificando o nome da classe para criar uma instância. Se um valor para o parâmetro *$className* não for especificado, uma instância do PHP **stdClass** será criada.  
  
*$ctorParams* [opcional]: uma matriz que contém valores passados para o construtor da classe especificada com o *$className* parâmetro. Se o construtor da classe especificada aceitar valores de parâmetro, o parâmetro *$ctorParams* deverá ser usado ao chamar **sqlsrv_fetch_object**.  
  
*linha* [opcional]: um dos valores a seguir, especificando a linha a ser acessada em um conjunto de resultados que usa um cursor rolável. (Se *linha* for especificado, *$className* e *$ctorParams* deve ser especificado explicitamente, mesmo que você especifique null para *$className*e *$ctorParams*.)  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Para obter mais informações sobre esses valores, consulte [Especificando um tipo de cursor e selecionando linhas](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
*deslocamento* [opcional]: usado com SQLSRV_SCROLL_ABSOLUTE e SQLSRV_SCROLL_RELATIVE para especificar a linha a ser recuperada. O primeiro registro no conjunto de resultados é 0.  
  
## <a name="return-value"></a>Valor de retorno  
Um objeto do PHP com propriedades que correspondem aos nomes de campo do conjunto de resultados. Os valores de propriedade são preenchidos com os valores de campo correspondentes do conjunto de resultados. Se a classe especificada com o parâmetro *$className* opcional não existir ou se não houver nenhum conjunto de resultados ativo associado à instrução especificada, **false** será retornado. Se não houver mais linhas para recuperar, **null** será retornado.  
  
O tipo de dados de um valor no objeto retornado será o tipo de dados do PHP padrão. Para obter informações sobre tipos de dados padrão do PHP, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md).  
  
## <a name="remarks"></a>Remarks  
Se um nome de classe for especificado com o parâmetro *$className* opcional, será criada uma instância de um objeto desse tipo de classe. Se a classe tiver propriedades cujos nomes correspondam aos nomes de campo do conjunto de resultados, os valores correspondentes do conjunto de resultados serão aplicados às propriedades. Se um nome de campo do conjunto de resultados não corresponder a uma propriedade de classe, uma propriedade com o nome de campo do conjunto de resultados será adicionada ao objeto, e o valor do conjunto de resultados será aplicado à propriedade.  
  
As seguintes regras se aplicam ao especificar uma classe com o parâmetro *$className* :  
  
-   A correspondência diferencia maiúsculas e minúsculas. Por exemplo, o nome da propriedade CustomerId não corresponde ao nome de campo CustomerID. Nesse caso, uma propriedade CustomerID seria adicionada ao objeto, e o valor do campo CustomerID seria fornecido à propriedade CustomerID.  
  
-   A correspondência ocorre independentemente dos modificadores de acesso. Por exemplo, se a classe especificada tiver uma propriedade privada cujo nome corresponder a um nome de campo do conjunto de resultados, o valor do campo do conjunto de resultados será aplicado à propriedade.  
  
-   Tipos de dados de propriedade de classe são ignorados. Se o campo "CustomerID" no conjunto de resultados for uma cadeia de caracteres, mas a propriedade "CustomerID" da classe for um inteiro, o valor da cadeia de caracteres do conjunto de resultados será gravado na propriedade "CustomerID".  
  
-   Se a classe especificada não existir, a função retornará **false** e adicionará um erro à coleção de erros. Para obter mais informações sobre a recuperação de informações de erro, consulte [sqlsrv_errors](../../connect/php/sqlsrv-errors.md).  
  
Se um campo sem nome for retornado, **sqlsrv_fetch_object** descartará o valor do campo e emitirá um aviso. Por exemplo, considere esta instrução Transact-SQL que insere um valor em uma tabela de banco de dados e recupera a chave primária gerada pelo servidor:  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
Se os resultados retornados por essa consulta forem recuperados com **sqlsrv_fetch_object**, o valor retornado por `SELECT SCOPE_IDENTITY()` será descartado, e um aviso será emitido. Para evitar isso, você pode especificar um nome para o campo retornado na instrução Transact-SQL. Veja a seguir uma maneira de especificar um nome de coluna no Transact-SQL:  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera cada linha de um conjunto de resultados como um objeto do PHP. O exemplo supõe que o SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
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
  
/* Set up and execute the query. */  
$tsql = "SELECT FirstName, LastName  
         FROM Person.Contact  
         WHERE LastName='Alan'";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in query preparation/execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve each row as a PHP object and display the results.*/  
while( $obj = sqlsrv_fetch_object( $stmt))  
{  
      echo $obj->LastName.", ".$obj->FirstName."\n";  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera cada linha de um conjunto de resultados como uma instância da classe *Product* definida no script. O exemplo recupera informações de produtos de *Purchasing. PurchaseOrderDetail* e *Production. Product* tabelas do banco de dados AdventureWorks para produtos que tenham uma data de vencimento ( *DueDate*) e uma quantidade em estoque (*StockQty*) menor que um valor especificado. O exemplo destaca algumas das regras que se aplicam ao especificar uma classe em uma chamada para **sqlsrv_fetch_object**:  
  
-   A variável *$product* é uma instância da classe *Product* , pois "Product" foi especificado com o parâmetro *$className* e a classe *Product* existe.  
  
-   A propriedade *Name* é adicionada à instância *$product* porque a propriedade *name* existente não corresponde.  
  
-   A propriedade *Color* é adicionada à instância *$product* porque não há uma propriedade correspondente.  
  
-   A propriedade privada *UnitPrice* é preenchida com o valor do campo *UnitPrice* .  
  
O exemplo supõe que SQL Server e o [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída será gravada no console quando o exemplo for executado da linha de comando.  
  
```  
<?php  
/* Define the Product class. */  
class Product  
{  
     /* Constructor */  
     public function Product($ID)  
     {  
          $this->objID = $ID;  
     }  
     public $objID;  
     public $name;  
     public $StockedQty;  
     public $SafetyStockLevel;  
     private $UnitPrice;  
     function getPrice()  
     {  
          return $this->UnitPrice;  
     }  
}  
  
/* Connect to the local server using Windows Authentication, and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Define the query. */  
$tsql = "SELECT Name,  
                SafetyStockLevel,  
                StockedQty,  
                UnitPrice,  
                Color  
         FROM Purchasing.PurchaseOrderDetail AS pdo  
         JOIN Production.Product AS p  
         ON pdo.ProductID = p.ProductID  
         WHERE pdo.StockedQty < ?  
         AND pdo.DueDate= ?";  
  
/* Set the parameter values. */  
$params = array(3, '2002-01-29');  
  
/* Execute the query. */  
$stmt = sqlsrv_query( $conn, $tsql, $params);  
if ( $stmt )  
{  
     echo "Statement executed.\n";  
}   
else   
{  
     echo "Error in statement execution.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Iterate through the result set, printing a row of data upon each  
 iteration. Note the following:  
     1) $product is an instance of the Product class.  
     2) The $ctorParams parameter is required in the call to  
        sqlsrv_fetch_object, because the Product class constructor is  
        explicity defined and requires parameter values.  
     3) The "Name" property is added to the $product instance because  
        the existing "name" property does not match.  
     4) The "Color" property is added to the $product instance  
        because there is no matching property.  
     5) The private property "UnitPrice" is populated with the value  
        of the "UnitPrice" field.*/  
$i=0; //Used as the $objID in the Product class constructor.  
while( $product = sqlsrv_fetch_object( $stmt, "Product", array($i)))  
{  
     echo "Object ID: ".$product->objID."\n";  
     echo "Product Name: ".$product->Name."\n";  
     echo "Stocked Qty: ".$product->StockedQty."\n";  
     echo "Safety Stock Level: ".$product->SafetyStockLevel."\n";  
     echo "Product Color: ".$product->Color."\n";  
     echo "Unit Price: ".$product->getPrice()."\n";  
     echo "-----------------\n";  
     $i++;  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
A variável **sqlsrv_fetch_object** sempre retorna dados de acordo com os [Default PHP Data Types](../../connect/php/default-php-data-types.md). Para obter informações sobre como especificar o tipo de dados do PHP, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
Se um campo sem nome for retornado, **sqlsrv_fetch_object** descartará o valor do campo e emitirá um aviso. Por exemplo, considere esta instrução Transact-SQL que insere um valor em uma tabela de banco de dados e recupera a chave primária gerada pelo servidor:  
  
<pre>INSERT INTO Production.ProductPhoto (LargePhoto) VALUES (?);  
SELECT SCOPE_IDENTITY()</pre>  
  
Se os resultados retornados por essa consulta forem recuperados com **sqlsrv_fetch_object**, o valor retornado por `SELECT SCOPE_IDENTITY()` será descartado, e um aviso será emitido. Para evitar isso, você pode especificar um nome para o campo retornado na instrução Transact-SQL. Veja a seguir uma maneira de especificar um nome de coluna no Transact-SQL:  
  
`SELECT SCOPE_IDENTITY() AS PictureID`  
  
## <a name="see-also"></a>Consulte também  
[Recuperando dados](../../connect/php/retrieving-data.md)  

[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
