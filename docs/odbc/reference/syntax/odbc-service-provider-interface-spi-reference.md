---
title: Referência de SPI (interface do provedor de serviços ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9739abd13bf2c4bed1b1b3a31c18c683594705a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298904"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Referência da SPI (Interface do Provedor de Serviços) do ODBC
Tradicionalmente, o ODBC definiu uma API (interface de programação de aplicativo). As funções na API podem ser chamadas por aplicativos e devem ser implementadas dentro do Gerenciador de driver e do driver.  
  
 Com a adição do recurso de pooling de conexão com reconhecimento de driver, o ODBC apresenta a SPI (Service Provider interface). As funções no SPI são usadas para comunicação entre o Gerenciador de driver e o driver. As funções SPI são implementadas pelo driver; o Gerenciador de driver não expõe funções SPI para aplicativos. Os aplicativos não devem chamar essas funções diretamente.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool de conexões do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
