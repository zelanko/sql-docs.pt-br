---
title: (Drivers da Microsoft para PHP para SQL Server) do pool de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
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
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2a332153e4e2651079198dac5b4390c3b56d550d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>Pool de conexões (Drivers da Microsoft para PHP para SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Veja a seguir pontos importantes a serem observados sobre o pool de conexões no [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]:  
  
-   O [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] usa o pool de conexões do ODBC.  
  
-   Por padrão, o pooling de conexão é habilitada no Windows. No Linux e Mac OS X, as conexões são agrupados somente se o pool de conexão está habilitado para ODBC. Quando o pool de conexão está habilitado e você se conectar a um servidor, o driver tenta usar uma conexão em pool antes de criar um novo. Se uma conexão equivalente não for encontrada no pool, uma nova conexão será criada e adicionada a ele. O driver determina se as conexões são equivalentes com base em uma comparação de cadeias de conexão.  
  
-   Quando uma conexão do pool é usada, o estado da conexão é redefinido.  
  
-   O fechamento da conexão retorna a conexão ao pool.  
  
Para obter mais informações sobre o pool de conexão, consulte [Pooling de Conexão do Gerenciador de Driver](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="enablingdisabling-connection-pooling"></a>Pooling de conexão habilitando/desabilitando
### <a name="windows"></a>Windows
Você pode forçar o driver a criar uma nova conexão (em vez de procurar uma conexão equivalente no pool de conexão), definindo o valor da *ConnectionPooling* atributo na cadeia de conexão para **false**  (ou 0).  
  
Se o *ConnectionPooling* atributo for omitido da cadeia de conexão ou se ele é definido como **true** (ou 1), o driver cria uma nova conexão somente se não existir uma conexão equivalente do pool de conexão.  
  
Para obter mais informações sobre outros atributos de conexão, consulte [Connection Options](../../connect/php/connection-options.md).  
### <a name="linux-and-mac-os-x"></a>Linux e Mac OS X
*ConnectionPooling* atributo não pode ser usado para habilitar/desabilitar o pooling de conexão. 

Pooling de Conexão pode ser habilitado/desabilitado, editando o arquivo de configuração odbcinst.ini. O driver deve ser recarregado para que as alterações entrem em vigor.

Configuração `Pooling` para `Yes` e um positivo `CPTimeout`valor no odbcinst.ini habilita o pooling de conexão. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
Configuração `Pooling` para `No` no odbcinst.ini força o driver a criar uma nova conexão.
```
[ODBC]
Pooling=No
```
  
## <a name="see-also"></a>Consulte também  
[Como se conectar usando a Autenticação do Windows](../../connect/php/how-to-connect-using-windows-authentication.md)

[Como se conectar usando a Autenticação do SQL Server](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
