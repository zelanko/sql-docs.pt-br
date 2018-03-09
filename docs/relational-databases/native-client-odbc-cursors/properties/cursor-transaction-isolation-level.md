---
title: "Nível de isolamento de transação do cursor | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88831b0ef8d0ecf1ecb5a0a8fee3d2918af2c2c8
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="cursor-transaction-isolation-level"></a>Nível de isolamento da transação de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O comportamento de bloqueio completo de cursores se baseia em uma interação entre atributos de simultaneidade e o nível de isolamento da transação definidos pelo cliente. Clientes ODBC definem a transação usando o [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION ou SQL_COPT_SS_TXN_ISOLATION. O comportamento de bloqueio de um ambiente de cursor específico é determinado pela combinação dos comportamentos de bloqueio das opções de nível de isolamento da transação e de simultaneidade.  
  
 Os seguintes níveis de isolamento de transação de cursor com suporte a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client:  
  
-   Leitura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Leitura não confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Leitura repetível (SQL_TXN_REPEATABLE_READ)  
  
-   Serializável (SQL_TXN_SERIALIZABLE)  
  
-   Instantâneo (SQL_TXN_SS_SNAPSHOT)  
  
 Observe que a API ODBC Especifica níveis de isolamento de transação adicionais, mas eles não são suportados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
