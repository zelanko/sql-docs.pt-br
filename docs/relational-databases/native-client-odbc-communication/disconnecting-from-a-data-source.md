---
title: Desconectando de uma fonte de dados | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9be70e47fa37db9caad77cccdd2930e126b49c16
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="disconnecting-from-a-data-source"></a>Desconectando uma fonte de dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Quando um aplicativo tiver terminado de usar uma fonte de dados, ele chama **SQLDisconnect**. **SQLDisconnect** libera todas as instruções que são alocadas a conexão e desconecta o driver da fonte de dados. Após a desconexão, o aplicativo pode chamar [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar o identificador de conexão. Antes de sair, um aplicativo também chama **SQLFreeHandle** para liberar o identificador de ambiente.  
  
 Depois de desconectar, um aplicativo pode reutilizar o identificador de conexão alocado para se conectar a uma outra fonte de dados ou para reconectar-se à mesma fonte de dados. A decisão de permanecer conectado em vez de desconectar e reconectar posteriormente exige que o criador do aplicativo considere os custos relativos de cada opção. Conectar-se a uma fonte de dados e permanecer conectado podem ser relativamente caro, dependendo do meio de conexão. Ao fazer uma compensação, o aplicativo deve também fazer suposições sobre a probabilidade e o tempo das operações adicionais na mesma fonte de dados. Talvez o aplicativo também precise usar mais de uma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Comunicação com o SQL Server &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
