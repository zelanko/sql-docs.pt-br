---
title: Simultaneidade do cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: rothja
ms.author: jroth
ms.openlocfilehash: c47f24152978fedf8f2c3d49ec3b721969712814
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020585"
---
# <a name="cursor-concurrency-odbc"></a>Simultaneidade do cursor (ODBC)
  As operações de cursor, assim como os tipos de cursor, são afetadas pelas opções de simultaneidade definidas pelo aplicativo. As opções de simultaneidade são definidas usando a opção SQL_ATTR_CONCURRENCY de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). Os tipos de simultaneidade são:  
  
-   Somente leitura (SQL_CONCUR_READONLY)  
  
-   Valores (SQL_CONCUR_VALUES)  
  
-   Versão de linha (SQL_CONCUR_ROWVER)  
  
-   Bloqueio (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades do cursor](cursor-properties.md)  
  
  
