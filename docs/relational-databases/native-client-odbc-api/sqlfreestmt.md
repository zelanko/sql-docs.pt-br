---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 11/23/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 2e83bc03d42f3b3ed1fde43bdc43c441c3304be8
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537466"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Em geral   
      **SQLFreeStmt** não é recomendado no ODBC 3.0 e posterior. No entanto se o aplicativo precisa reutilizar a instrução ainda use **SQLFreeStmt** com o **SQL_RESET_PARAMS** e **SQL_UNBIND** opções). Você também pode usar [SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md), [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md), [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md), [SQLSetDescField](../../relational-databases/native-client-odbc-api/sqlsetdescfield.md), e [ SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para substituir ou duplicam a função do **SQLFreeStmt** e devem ser usadas em vez disso.  
  
 Em geral, é mais eficiente reutilizar as instruções que to soltá-los e alocar novos. No entanto em algumas situações, como a reutilização de instruções, SQLFreeStmt ainda deve ser usado.  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLFreeStmt](http://go.microsoft.com/fwlink/?LinkId=59346)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
