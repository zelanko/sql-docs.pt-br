---
title: Como desabilitar MARS (vários conjuntos de resultados ativos) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple active result sets, disabling
- MARS, disabling
ms.assetid: 1912ad05-d0a4-40ff-8888-0d85bb36a807
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a438c1d077de0559a950458755a68ac08a1de089
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796119"
---
# <a name="how-to-disable-multiple-active-resultsets-mars"></a>Como desabilitar vários conjuntos de resultados ativos (MARS)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Se você precisa se conectar a uma fonte de dados do SQL Server que não permite vários conjuntos de dados ativos (MARS), pode usar a opção de conexão MultipleActiveResultSets para desabilitar ou habilitar o MARS.  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-disable-mars-support"></a>Para desabilitar o suporte de MARS  
  
-   Use a seguinte opção de conexão:  
  
    ```  
    'MultipleActiveResultSets'=>false  
    ```  
  
    Se o aplicativo tentar executar uma consulta em uma conexão que tem um conjunto de resultados ativo aberto, a segunda tentativa de consulta retornará as informações de erro a seguir:  
  
    A conexão não pode processar esta operação porque há uma instrução com resultados pendentes.  Para disponibilizar a conexão para outras consultas, busque todos os resultados ou então cancele ou libere a instrução. Para obter mais informações sobre a opção de conexão MultipleActiveResultSets, consulte [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir mostra como desabilitar o suporte de MARS usando o driver SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "MyServer";  
$connectionInfo = array( "Database"=>"AdventureWorks", 'MultipleActiveResultSets'=> false);  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
   echo "Could not connect.\n";  
   die( print_r( sqlsrv_errors(), true));  
}  
  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir mostra como desabilitar o suporte para MARS usando o driver PDO_SQLSRV dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
```  
<?php  
// Connect to the local server using Windows Authentication and AdventureWorks database  
$serverName = "(local)";   
$database = "AdventureWorks";  
  
try {  
   $conn = new PDO(" sqlsrv:server=$serverName ; Database=$database ; MultipleActiveResultSets=false ", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );   
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
$conn = null;   
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)  
  
