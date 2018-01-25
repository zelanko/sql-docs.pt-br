---
title: SQLFetchScroll | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords: SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ece42f98419e884d5458959112a0089b0c441ae
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLFetchScroll** retorna um conjunto de linhas de dados para o aplicativo. O tamanho do conjunto de linhas é definido usando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a todas as instruções de busca definidas (por exemplo, SQL_FETCH_RELATIVE) com as seguintes limitações:  
  
-   Se um cursor de somente avanço for definido para a instrução, SQL_FETCH_NEXT será necessário e as tentativas de busca de qualquer outro modo resultarão em erro.  
  
-   SQL_FETCH_BOOKMARK só é suportado para cursores estáticos e controlados por conjunto de chaves.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>Suporte SQLFetchScroll para recursos avançados de data e hora  
 Valores de coluna de resultado dos tipos de data/hora são convertidos conforme descrito em [conversões de SQL para C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>Suporte SQLFetchScroll para UDTs CLR grandes  
 **SQLFetchScroll** dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLFetchScroll](http://go.microsoft.com/fwlink/?LinkId=59343)   
 [Detalhes de implementação de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
