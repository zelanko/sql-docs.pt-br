---
title: Recuperar informações do conjunto de resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3017f74b12eb18624f8a34e8a1289da18b70c93a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712694"
---
# <a name="retrieve-result-set-information-odbc"></a>Recuperar informações do conjunto de resultados (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>Para obter informações sobre um conjunto de resultados  
  
1.  Chame [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) para obter o número de colunas no conjunto de resultados.  
  
2.  Para cada coluna no conjunto de resultados:  
  
    -   Chame [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) para obter informações sobre a coluna de resultado.  
  
     Ou  
  
    -   Chame [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) para obter informações de descritor específicas sobre a coluna de resultado.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre o processamento de resultados &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [Determinando as características de um conjunto de resultados &#40;&#41;ODBC](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
