---
title: Referência de Interface do Provedor de Serviços ODBC (SPI) | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298904"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Referência da SPI (Interface do Provedor de Serviços) do ODBC
Tradicionalmente, a ODBC definiu uma interface de programação de aplicativos (API). As funções na API podem ser chamadas por aplicativos e devem ser implementadas tanto dentro do Driver Manager quanto do driver.  
  
 Com a adição do recurso de poolde conexão com reconhecimento de driver, a ODBC introduz a interface do provedor de serviços (SPI). As funções no SPI são usadas para comunicação entre o Driver Manager e o driver. As funções de SPI são implementadas pelo driver; o Driver Manager não expõe funções SPI a aplicativos. Os aplicativos não devem chamar essas funções diretamente.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [Sqlgetpoolid](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLpoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [Conexão SQLRate](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SqlSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Desenvolvendo a conscientização do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool de conexões do Gerenciador de Driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
