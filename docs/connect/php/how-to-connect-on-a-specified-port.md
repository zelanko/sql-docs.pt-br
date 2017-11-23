---
title: 'Como: conectar-se em uma porta especificada | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 88115d77c56cafed731aa2a9cf6c39afcd191618
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-connect-on-a-specified-port"></a>Como se conectar a uma porta especificada
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve como se conectar ao SQL Server em uma porta especificada com os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
### <a name="to-connect-on-a-specified-port"></a>Para se conectar em uma porta especificada  
  
1.  Verifique a porta na qual o servidor está configurado para aceitar conexões. Para obter informações sobre como configurar um servidor para aceitar conexões em uma porta especificada, consulte [como: configurar um servidor para escutar em uma porta de TCP específica (SQL Server Configuration Manager)](http://go.microsoft.com/fwlink/?LinkId=121865).  
  
2.  Adicione a porta desejada para o *$serverName* parâmetro o [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) função. Separe o nome do servidor e a porta com uma vírgula. Por exemplo, as seguintes linhas de código usam o driver SQLSRV para demonstrar como se conectar a um servidor chamado *myServer* na porta 1521:  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    As seguintes linhas de código usam o driver PDO_SQLSRV para demonstrar como se conectar a um servidor chamado *myServer* na porta 1521:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>Consulte também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)  
[Guia de programação para o driver SQL de PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Introdução ao driver SQL de PHP](../../connect/php/getting-started-with-the-php-sql-driver.md) 
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
[Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  

