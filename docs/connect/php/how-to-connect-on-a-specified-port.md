---
title: 'Como fazer: Conectar em uma porta especificada | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af055a73904bb8feec92fb2afe93df064a09ab23
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015055"
---
# <a name="how-to-connect-on-a-specified-port"></a>Como fazer: Conectar em uma porta especificada
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico descreve como se conectar ao SQL Server em uma porta especificada com os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
### <a name="to-connect-on-a-specified-port"></a>Para se conectar em uma porta especificada  
  
1.  Verifique a porta na qual o servidor está configurado para aceitar conexões. Para obter informações sobre como configurar um servidor para aceitar conexões em uma porta especificada, confira [Como configurar um servidor para escuta em uma porta TCP específica (SQL Server Configuration Manager)](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Adicione a porta desejada ao parâmetro *$serverName* da função [sqlsrv_connect](../../connect/php/sqlsrv-connect.md). Separe o nome do servidor e a porta com uma vírgula. Por exemplo, as seguintes linhas de código usam o driver SQLSRV para demonstrar como se conectar a um servidor chamado *myServer* na porta 1521:  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    As linhas de código a seguir usam o driver PDO_SQLSRV para demonstrar como se conectar a um servidor chamado *myServer* na porta 1521:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Conectando-se ao servidor](../../connect/php/connecting-to-the-server.md)

[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Introdução aos Drivers da Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV Driver Reference](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
