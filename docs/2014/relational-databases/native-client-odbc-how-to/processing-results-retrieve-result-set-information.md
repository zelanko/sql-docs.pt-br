---
title: Recuperar informações de conjunto de resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a814a65419026dfb6e7901f2b49db2096c5da423
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409636"
---
# <a name="retrieve-result-set-information-odbc"></a>Recuperar informações do conjunto de resultados (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>Para obter informações sobre um conjunto de resultados  
  
1.  Chame [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) para obter o número de colunas no conjunto de resultados.  
  
2.  Para cada coluna no conjunto de resultados:  
  
    -   Chame [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) para obter informações sobre a coluna de resultados.  
  
     Ou  
  
    -   Chame [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) para obter informações específicas do descritor sobre a coluna de resultado.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos explicativos de resultados de processamento &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [Determinando as características de um conjunto de resultados &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
