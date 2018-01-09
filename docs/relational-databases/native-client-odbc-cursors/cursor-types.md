---
title: Tipos de cursor | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5cff663d1f61790ba3c0afa7dc3059e38389702
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="cursor-types"></a>Tipos de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC define quatro tipos de cursor suportados pelo Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client. Esses cursores variam em sua capacidade de detectar alterações para o conjunto de resultados e nos recursos consomem, como memória em espaço em **tempdb**. Um cursor pode detectar alterações nas linhas apenas quando ele tenta buscar essas linhas novamente; não há como a fonte de dados notificar o cursor dessas alterações nas linhas que estão sendo buscadas atualmente. A capacidade de um cursor de detectar alterações que não foram feitas pelo cursor também é influenciada pelo nível de isolamento da transação.  
  
 Estes são os quatro tipos de cursor ODBC suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Cursores de somente avanço não suportam o recurso de rolagem; eles suportam apenas a busca de linhas em série do início ao fim do cursor.  
  
-   Cursores estáticos são incorporados no **tempdb** quando o cursor é aberto. Eles sempre exibem o conjunto de resultados da forma como ele estava quando o cursor foi aberto. Eles nunca refletem alterações aos dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores estáticos são sempre somente leitura. Como um cursor de servidor estático é criado como uma tabela de trabalho em **tempdb**, o tamanho do conjunto de resultados de cursor não pode exceder o tamanho de linha máximo permitido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Os cursores controlados por conjunto de chaves têm a associação (membership) e a ordem das linhas fixas no conjunto de resultados quando o cursor é aberto. As alterações nas colunas não chave são visíveis pelo cursor.  
  
-   Os cursores dinâmicos são o oposto dos cursores estáticos. Eles refletem todas as alterações feitas nas linhas de seu conjunto de resultados. Os valores de dados, a ordem e a associação das linhas do conjunto de resultados podem ser alterados em cada busca.  
  
## <a name="see-also"></a>Consulte Também  
 [Usando cursores &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
