---
title: Nível de isolamento da transação de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fef68bfdb62527f7b631b8d7433e095eba4d1c88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207145"
---
# <a name="cursor-transaction-isolation-level"></a>Nível de isolamento da transação de cursor
  O comportamento de bloqueio completo de cursores se baseia em uma interação entre atributos de simultaneidade e o nível de isolamento da transação definidos pelo cliente. Clientes ODBC definem a transação usando o [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION ou SQL_COPT_SS_TXN_ISOLATION. O comportamento de bloqueio de um ambiente de cursor específico é determinado pela combinação dos comportamentos de bloqueio das opções de nível de isolamento da transação e de simultaneidade.  
  
 Os seguintes níveis de isolamento de transação de cursor são suportados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client:  
  
-   Leitura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Leitura não confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Leitura repetível (SQL_TXN_REPEATABLE_READ)  
  
-   Serializável (SQL_TXN_SERIALIZABLE)  
  
-   Instantâneo (SQL_TXN_SS_SNAPSHOT)  
  
 Observe que a API ODBC Especifica níveis de isolamento de transação adicionais, mas eles não são suportados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do cursor](cursor-properties.md)  
  
  
