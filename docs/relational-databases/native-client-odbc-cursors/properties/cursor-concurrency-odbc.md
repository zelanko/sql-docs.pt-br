---
description: Simultaneidade do cursor (ODBC)
title: Simultaneidade do cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 343eaeceeb12e71f0df9b4a2791120007effac46
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473717"
---
# <a name="cursor-concurrency-odbc"></a>Simultaneidade do cursor (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  As operações de cursor, assim como os tipos de cursor, são afetadas pelas opções de simultaneidade definidas pelo aplicativo. As opções de simultaneidade são definidas usando a opção SQL_ATTR_CONCURRENCY de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Os tipos de simultaneidade são:  
  
-   Somente leitura (SQL_CONCUR_READONLY)  
  
-   Valores (SQL_CONCUR_VALUES)  
  
-   Versão de linha (SQL_CONCUR_ROWVER)  
  
-   Bloqueio (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
