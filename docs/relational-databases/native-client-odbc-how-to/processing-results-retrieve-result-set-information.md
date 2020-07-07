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
ms.openlocfilehash: f00fe6310c339d7ec24736c5f659d3b7b7d84ce8
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006572"
---
# <a name="processing-results---retrieve-result-set-information"></a>Resultados do processamento – Recuperar informações do conjunto de resultados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-get-information-about-a-result-set"></a>Para obter informações sobre um conjunto de resultados  
  
1.  Chame [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obter o número de colunas no conjunto de resultados.  
  
2.  Para cada coluna no conjunto de resultados:  
  
    -   Chame [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) para obter informações sobre a coluna de resultado.  
  
     Ou  
  
    -   Chame [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) para obter informações de descritor específicas sobre a coluna de resultado.  
  
## <a name="see-also"></a>Consulte Também  
[Resultados do processo &#40;&#41;ODBC](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinando as características de um conjunto de resultados &#40;&#41;ODBC](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
