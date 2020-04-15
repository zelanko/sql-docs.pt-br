---
title: Recuperar informações do conjunto de resultados (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1c65841db0fdfd386891cfbd03bdee483ce25f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300366"
---
# <a name="processing-results---retrieve-result-set-information"></a>Resultados do processamento – Recuperar informações do conjunto de resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-get-information-about-a-result-set"></a>Para obter informações sobre um conjunto de resultados  
  
1.  Ligue para [sqlnumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obter o número de colunas no conjunto de resultados.  
  
2.  Para cada coluna no conjunto de resultados:  
  
    -   Ligue para [o SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) para obter informações sobre a coluna de resultados.  
  
     Ou  
  
    -   Ligue para [sqlcolattribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) para obter informações específicas sobre a coluna de resultados.  
  
## <a name="see-also"></a>Consulte Também  
[Resultados do processo &#40;&#41;da ODBC](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinando as características de um conjunto de resultados &#40;o&#41;da ODBC](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
