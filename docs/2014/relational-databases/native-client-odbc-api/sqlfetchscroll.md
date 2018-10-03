---
title: SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ee2297f01ef2cc0a4dc94beca66939bf6ae9030
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145646"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll** retorna um conjunto de linhas de dados para o aplicativo. O tamanho do conjunto de linhas é definido usando [SQLSetStmtAttr](sqlsetstmtattr.md). O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte a todas as instruções de busca definidas (por exemplo, SQL_FETCH_RELATIVE) com as seguintes limitações:  
  
-   Se um cursor de somente avanço for definido para a instrução, SQL_FETCH_NEXT será necessário e as tentativas de busca de qualquer outro modo resultarão em erro.  
  
-   SQL_FETCH_BOOKMARK só é suportado para cursores estáticos e controlados por conjunto de chaves.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>Suporte SQLFetchScroll para recursos avançados de data e hora  
 Os valores de coluna de resultado dos tipos de data/hora são convertidos conforme descrito em [conversões de SQL para C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Para obter mais informações, consulte [aprimoramentos de data e hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>Suporte SQLFetchScroll para UDTs CLR grandes  
 **SQLFetchScroll** dá suporte a UDTs (tipos definidos pelo usuário) CLR grandes. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLFetchScroll](http://go.microsoft.com/fwlink/?LinkId=59343)   
 [Detalhes da implementação da API do ODBC](odbc-api-implementation-details.md)  
  
  
