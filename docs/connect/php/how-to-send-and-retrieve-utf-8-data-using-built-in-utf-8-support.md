---
title: 'Como: enviar e recuperar dados UTF-8 usando o suporte interno a UTF-8 | Microsoft Docs'
ms.custom: ''
ms.date: 03/23/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- retrieving data, UTF-8 encoded data
- converting data types
- updating data
ms.assetid: 366c57cf-352f-4202-8074-6ddce44880d1
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bfb2e5a7bd7bef5d34d60e6e5435295b342bcca5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support"></a>Como enviar e recuperar dados UTF-8 usando o suporte interno a UTF-8
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Se você estiver usando o driver PDO_SQLSRV, pode especificar a codificação com o atributo PDO::SQLSRV_ATTR_ENCODING. Para obter mais informações, consulte [Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
O restante deste tópico aborda a codificação com o driver SQLSRV.  
  
Para recuperar ou enviar dados codificados em UTF-8 para o servidor:  
  
1.  Verifique se a coluna de origem ou de destino é do tipo **nchar** ou **nvarchar**.  
  
2.  Especifique o tipo de PHP como `SQLSRV_PHPTYPE_STRING('UTF-8')` na matriz de parâmetros. Ou especifique `"CharacterSet" => "UTF-8"` como uma opção de conexão.  
  
    Quando você especifica um conjunto de caracteres como parte das opções de conexão, o driver pressupõe que as outras cadeias de caracteres da opção de conexão usem esse mesmo conjunto de caracteres. Também pressupõe-se que o nome do servidor e as cadeias de caracteres de consulta usem o mesmo conjunto de caracteres.  
  
Você pode passar UTF-8 ou SQLSRV_ENC_CHAR para **CharacterSet**, mas não é possível passar SQLSRV_ENC_BINARY. A codificação padrão é SQLSRV_ENC_CHAR.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir demonstra como enviar e recuperar dados codificados em UTF-8 especificando o conjunto de caracteres UTF-8 ao fazer a conexão. O exemplo atualiza a coluna Comments da tabela Production.ProductReview para uma ID de análise especificada. O exemplo também recupera e exibe os dados recém-atualizados. Observe que a coluna Comments é do tipo **nvarchar (3850).** Observe também que antes de dados são enviados para o servidor, ele é convertido em UTF-8 codificação usando o PHP **utf8_encode** função. Isso é feito apenas para fins de demonstração. Em um cenário de aplicativo real, você começaria com dados codificados UTF-8.  
  
O exemplo supõe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) banco de dados são instalados no computador local. Toda a saída será gravada no navegador quando o exemplo é executado a partir do navegador.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", "CharacterSet" => "UTF-8");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing 1, 2, 3, 4.  Testing.");  
$params1 = array(  
                  array( $comments, null ),  
                  array( $reviewID, null )  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field( $stmt2, 0 );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
Para obter informações sobre como armazenar dados Unicode, consulte [trabalhar com dados Unicode](https://msdn.microsoft.com/library/ms175180.aspx).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir é semelhante ao primeiro exemplo, mas em vez de especificar o conjunto de caracteres UTF-8 na conexão, este exemplo mostra como especificar o conjunto de caracteres UTF-8 na coluna.  
  
```  
<?php  
  
// Connect to the local server using Windows Authentication and  
// specify the AdventureWorks database as the database in use.   
//   
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
  
if ( $conn === false ) {  
   echo "Could not connect.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Set up the Transact-SQL query.  
//   
$tsql1 = "UPDATE Production.ProductReview  
          SET Comments = ?  
          WHERE ProductReviewID = ?";  
  
// Set the parameter values and put them in an array. Note that  
// $comments is converted to UTF-8 encoding with the PHP function  
// utf8_encode to simulate an application that uses UTF-8 encoded data.   
//   
$reviewID = 3;  
$comments = utf8_encode("testing");  
$params1 = array(  
                  array($comments,  
                        SQLSRV_PARAM_IN,  
                        SQLSRV_PHPTYPE_STRING('UTF-8')  
                  ),  
                  array($reviewID)  
                );  
  
// Execute the query.  
//   
$stmt1 = sqlsrv_query($conn, $tsql1, $params1);  
  
if ( $stmt1 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
else {  
   echo "The update was successfully executed.<br>";  
}  
  
// Retrieve the newly updated data.  
//   
$tsql2 = "SELECT Comments   
          FROM Production.ProductReview   
          WHERE ProductReviewID = ?";  
  
// Set up the parameter array.  
//   
$params2 = array($reviewID);  
  
// Execute the query.  
//   
$stmt2 = sqlsrv_query($conn, $tsql2, $params2);  
if ( $stmt2 === false ) {  
   echo "Error in statement execution.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Retrieve and display the data.   
//   
if ( sqlsrv_fetch($stmt2) ) {  
   echo "Comments: ";  
   $data = sqlsrv_get_field($stmt2,   
                            0,   
                            SQLSRV_PHPTYPE_STRING('UTF-8')  
                           );  
   echo $data."<br>";  
}  
else {  
   echo "Error in fetching data.<br>";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
// Free statement and connection resources.  
//   
sqlsrv_free_stmt( $stmt1 );  
sqlsrv_free_stmt( $stmt2 );  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Recuperando dados](../../connect/php/retrieving-data.md)

[Trabalhando com dados de ASCII em não-Windows](../../connect/php/how-to-send-and-retrieve-ascii-data-in-linux-mac.md)

[Atualizando dados &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[Referência da API do driver JDBC](../../connect/php/sqlsrv-driver-api-reference.md)

[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Aplicativo de exemplo &#40;driver SQLSRV&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
  
