---
title: Simultaneidade de cursor (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: da4b99f4ea20ce7c8540f45a4324321413b18183
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117199"
---
# <a name="cursor-concurrency-odbc"></a>Simultaneidade do cursor (ODBC)
  As operações de cursor, assim como os tipos de cursor, são afetadas pelas opções de simultaneidade definidas pelo aplicativo. Opções de simultaneidade são definidas usando a opção SQL_ATTR_CONCURRENCY de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). Os tipos de simultaneidade são:  
  
-   Somente leitura (SQL_CONCUR_READONLY)  
  
-   Valores (SQL_CONCUR_VALUES)  
  
-   Versão de linha (SQL_CONCUR_ROWVER)  
  
-   Bloqueio (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do cursor](cursor-properties.md)  
  
  