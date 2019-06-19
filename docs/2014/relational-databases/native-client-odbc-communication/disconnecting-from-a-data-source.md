---
title: Desconectando de uma fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ccc784d0d8759c559e705cbbb65861040f6e8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205681"
---
# <a name="disconnecting-from-a-data-source"></a>Desconectando uma fonte de dados
  Quando um aplicativo tiver terminado de usar uma fonte de dados, ele chama **SQLDisconnect**. **SQLDisconnect** libera todas as instruções que são alocadas a conexão e desconecta o driver da fonte de dados. Após a desconexão, o aplicativo pode chamar [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) para liberar o identificador de conexão. Antes de sair, um aplicativo também chama **SQLFreeHandle** para liberar o identificador de ambiente.  
  
 Depois de desconectar, um aplicativo pode reutilizar o identificador de conexão alocado para se conectar a uma outra fonte de dados ou para reconectar-se à mesma fonte de dados. A decisão de permanecer conectado em vez de desconectar e reconectar posteriormente exige que o criador do aplicativo considere os custos relativos de cada opção. Conectar-se a uma fonte de dados e permanecer conectado podem ser relativamente caro, dependendo do meio de conexão. Ao fazer uma compensação, o aplicativo deve também fazer suposições sobre a probabilidade e o tempo das operações adicionais na mesma fonte de dados. Talvez o aplicativo também precise usar mais de uma conexão.  
  
## <a name="see-also"></a>Consulte também  
 [Comunicando-se com o SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
