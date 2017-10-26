---
title: "Como: recuperar dados binários como um fluxo usando o Driver SQLSRV | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retrieving data, as a binary stream
- streaming data
ms.assetid: cd8d6382-abe6-48ee-9d10-4e6c52c0cb9a
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9cfd6c030465016673acc6c81706e88979078629
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-retrieve-binary-data-as-a-stream-using-the-sqlsrv-driver"></a>Como recuperar dados binários como um fluxo usando o driver SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recuperação de dados como um fluxo só está disponível no driver SQLSRV do [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]e não está disponível no driver PDO_SQLSRV.  
  
Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] aproveitam os fluxos do PHP para recuperar grandes quantidades de dados binários do servidor. Este tópico demonstra como recuperar dados binários como um fluxo.  
  
O uso de fluxos para recuperar dados binários, como imagens, evita o uso de grandes quantidades de memória de script, recuperando partes de dados em vez de carregar o objeto inteiro na memória de script.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir recupera dados binários (neste caso, uma imagem) da tabela *Production.ProductPhoto* do banco de dados AdventureWorks. A imagem é recuperada como um fluxo e exibida no navegador.  
  
A recuperação de dados de imagem como um fluxo é efetuada usando [sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md) e [sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md) com o tipo de retorno especificado como um fluxo binário. O tipo de retorno é especificado usando a constante **SQLSRV_PHPTYPE_STREAM**. Para obter informações sobre **sqlsrv** constantes, consulte [constantes &#40; Drivers da Microsoft para PHP para SQL Server &#41; ](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md).  
  
O exemplo supõe que o SQL Server e o banco de dados [AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=67739) estejam instalados no computador local. Toda a saída é gravada no navegador quando o exemplo é executado a partir do navegador.  
  
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
  
/* Set up the Transact-SQL query. */  
$tsql = "SELECT LargePhoto   
         FROM Production.ProductPhoto   
         WHERE ProductPhotoID = ?";  
  
/* Set the parameter values and put them in an array. */  
$productPhotoID = 70;  
$params = array( $productPhotoID);  
  
/* Execute the query. */  
$stmt = sqlsrv_query($conn, $tsql, $params);  
if( $stmt === false )  
{  
     echo "Error in statement execution.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the data.  
The return data is retrieved as a binary stream. */  
if ( sqlsrv_fetch( $stmt ) )  
{  
   $image = sqlsrv_get_field( $stmt, 0,   
                      SQLSRV_PHPTYPE_STREAM(SQLSRV_ENC_BINARY));  
   header("Content-Type: image/jpg");  
   fpassthru($image);  
}  
else  
{  
     echo "Error in retrieving data.</br>";  
     die(print_r( sqlsrv_errors(), true));  
}  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
A especificação do tipo de retorno no exemplo demonstra como especificar o tipo de retorno do PHP como um fluxo binário. Tecnicamente, ele não é necessário no exemplo porque o *LargePhoto* campo tem varbinary (max) de tipo do SQL Server e, portanto, é retornado como um fluxo binário por padrão. Para obter informações sobre os tipos de dados padrão do PHP, consulte [Default PHP Data Types](../../connect/php/default-php-data-types.md). Para obter informações sobre como especificar tipos de retorno do PHP, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
## <a name="see-also"></a>Consulte também  
[Recuperando dados](../../connect/php/retrieving-data.md)  
[Recuperando dados como um fluxo usando o driver SQLSRV](../../connect/php/retrieving-data-as-a-stream-using-the-sqlsrv-driver.md)  
[Sobre exemplos de código na documentação](../../connect/php/about-code-examples-in-the-documentation.md)  
  

