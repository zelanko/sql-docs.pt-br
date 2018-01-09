---
title: "Comunicação com o SQL Server (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 957ffb336a018128b6cb5de24ba70ac60509de47
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicando-se com o SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Para um aplicativo ODBC para se comunicar com uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele deve alocar o ambiente e conexão manipula e conecte-se à fonte de dados. Depois que uma conexão é estabelecida, o aplicativo pode enviar consultas ao servidor e processar quaisquer conjuntos de resultados. Quando o aplicativo conclui o uso da fonte de dados, ele se desconecta da fonte de dados e libera o identificador de conexão. Depois de liberar todos os identificadores de conexão, o aplicativo libera o identificador de ambiente.  
  
 Um aplicativo pode se conectar a qualquer número de fontes de dados. O aplicativo pode usar uma combinação de drivers e fontes de dados, o mesmo driver e uma combinação de fontes de dados ou inclusive o mesmo driver e várias conexões com a mesma fonte de dados.  
  
 Você pode baixar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC amostras do [Downloads do SQL Server](http://go.microsoft.com/fwlink/?LinkId=62796) página no MSDN.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Alocando um identificador de ambiente](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [Alocando um identificador de conexão](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [Fontes de dados ODBC do SQL Server Native Client](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [Conexão com uma fonte de dados &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [Desconectando uma fonte de dados](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do SQL Server &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
