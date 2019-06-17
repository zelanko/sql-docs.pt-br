---
title: Referência de Interface (SPI) do provedor de serviço ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e3d83f0aa27641c9dde164f51319a0e78d456ba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653244"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Referência da SPI (Interface do Provedor de Serviços) do ODBC
Tradicionalmente, o ODBC definidos uma interface de programação de aplicativo (API). As funções na API podem ser chamadas por aplicativos e eles devem ser implementados dentro do Gerenciador de Driver e o driver.  
  
 Com a adição do recurso de pooling de conexão de reconhecimento de driver, ODBC apresenta a interface de provedor de serviço (SPI). As funções no SPI são usadas para comunicação entre o Gerenciador de Driver e o driver. Funções SPI são implementadas pelo driver; o Gerenciador de Driver não expõe funções SPI aos aplicativos. Aplicativos não devem chamar essas funções diretamente.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
 Esta seção contém os tópicos a seguir  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool de conexões do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
