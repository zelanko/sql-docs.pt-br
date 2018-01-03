---
title: "Referência de Interface (IDA) do provedor de serviço ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d902f5202d0f669fa6aa9272a871b3c855acd20a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Referência de Interface (IDA) do provedor de serviço ODBC
Tradicionalmente, o ODBC definidos uma interface de programação de aplicativo (API). As funções na API do podem ser chamadas por aplicativos e eles devem ser implementados dentro do Gerenciador de Driver e o driver.  
  
 Com a adição do recurso de pooling de conexão com reconhecimento de driver, ODBC apresenta a interface de provedor de serviço (IDA). As funções a ida são usadas para comunicação entre o Gerenciador de Driver e o driver. Funções de ida são implementadas pelo driver; o Gerenciador de Driver não expõe funções ida para aplicativos. Aplicativos não devem chamar essas funções diretamente.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
 Esta seção contém os tópicos a seguir  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Desenvolvimento de reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool de conexões do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
