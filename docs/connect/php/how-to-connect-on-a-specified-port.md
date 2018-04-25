---
title: 'Como: conectar-se em uma porta especificada | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b17dd2bb8df3f7274cb8eea36faf3ee5f320f983
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-connect-on-a-specified-port"></a>Como se conectar a uma porta especificada
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve como se conectar ao SQL Server em uma porta especificada com os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
### <a name="to-connect-on-a-specified-port"></a>Para se conectar em uma porta especificada  
  
1.  Verifique a porta na qual o servidor está configurado para aceitar conexões. Para obter informações sobre como configurar um servidor para aceitar conexões em uma porta especificada, consulte [How to: Configure a Server to Listen on a Specific TCP Port ](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)SQL Server Configuration Manager (Como configurar um servidor para escuta em uma porta TCP específica (SQL Server Configuration Manager)).  
  
2.  Adicione a porta desejada ao parâmetro *$serverName* da função [sqlsrv](../../connect/php/sqlsrv-connect.md)connect. Separe o nome do servidor e a porta com uma vírgula. Por exemplo, as seguintes linhas de código usam o driver SQLSRV para demonstrar como se conectar a um servidor chamado *myServer* na porta 1521:  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    As linhas de código a seguir usam o driver PDO*SQLSRV para demonstrar como se conectar a um servidor chamado* myServer na porta 1521:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)

[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Guia de Introdução com os Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV Driver Reference](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
