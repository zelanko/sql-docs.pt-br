---
title: "Recuperar informações de conjunto de resultados (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d02d5d45b4b06a5c8e3e0ce016a6c5930d3c00fb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="processing-results---retrieve-result-set-information"></a>Processando resultados - recuperar informações do conjunto de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-get-information-about-a-result-set"></a>Para obter informações sobre um conjunto de resultados  
  
1.  Chamar [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obter o número de colunas no conjunto de resultados.  
  
2.  Para cada coluna no conjunto de resultados:  
  
    -   Chamar [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) para obter informações sobre a coluna de resultados.  
  
     Ou  
  
    -   Chamar [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) para obter informações específicas do descritor sobre a coluna de resultado.  
  
## <a name="see-also"></a>Consulte Também  
[Processar resultados &#40; ODBC &#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinar as características de um conjunto de resultados &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
