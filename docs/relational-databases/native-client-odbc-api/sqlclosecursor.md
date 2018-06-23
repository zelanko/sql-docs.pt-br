---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 389236f4ede54ac618bac6d9d0fd0687c61a12e4
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700487"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLCloseCursor** substitui [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com um *opção* valor SQL_CLOSE. Após a recepção de **SQLCloseCursor**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client descarta linhas do conjunto de resultados pendentes. Observe que as associações de parâmetro e coluna da instrução (se houver) são mantidas inalteradas por **SQLCloseCursor**.  
  
## <a name="see-also"></a>Consulte também  
 [SQLCloseCursor](http://go.microsoft.com/fwlink/?LinkId=59331)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
