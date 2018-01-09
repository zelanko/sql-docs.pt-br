---
title: "Atribuição de armazenamento | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-results
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- column-wise binding [ODBC]
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- SQLBindCol function
- storing data [ODBC]
- result sets [ODBC], storage
- SQL Server Native Client ODBC driver, data storage
- row-wise binding
- binding result sets [SQL Server Native Client]
- array binding
ms.assetid: 11c81955-5300-495f-925f-9256f2587b58
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b15ef1ebc3e6f947f361c52444b2587ff79d2fec
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="assigning-storage"></a>Atribuindo armazenamento
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Um aplicativo pode atribuir armazenamento para resultados antes ou depois de executar uma instrução SQL. Caso prepare ou execute a instrução SQL primeiro, um aplicativo pode consultar o conjunto de resultados antes de atribuir o armazenamento para resultados. Por exemplo, caso o conjunto de resultados seja desconhecido, o aplicativo deve recuperar o número de colunas antes de atribuir o armazenamento a eles.  
  
 Para associar o armazenamento para uma coluna de dados, um aplicativo chama [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)e passá-lo:  
  
-   O tipo de dados no qual os dados serão convertidos.  
  
-   O endereço de um buffer de saída para os dados.  
  
     O aplicativo deve alocar esse buffer e ser grande o bastante para manter os dados na forma em que são convertidos.  
  
-   O comprimento do buffer de saída.  
  
     Esse valor será ignorado se os dados retornados tiverem uma largura fixa em C como, por exemplo, um inteiro, número real ou estrutura de data.  
  
-   O endereço de um buffer de armazenamento no qual retornar o número de bytes de dados disponíveis.  
  
 Um aplicativo também pode associar colunas de conjunto de resultados a matrizes de variáveis de programa para oferecer suporte à busca das linhas de conjunto de resultados em blocos. Há dois tipos diferentes de associação de matriz:  
  
-   A associação que reconhece a coluna é concluída quando cada coluna é associada a sua própria matriz de variáveis.  
  
     A associação é especificada chamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com *atributo* definido como SQL_ATTR_ROW_BIND_TYPE e *ValuePtr* definido como SQL_BIND_BY_COLUMN. Todos as matrizes devem ter o mesmo número de elementos.  
  
-   A associação que reconhece a linha é concluída quando todos os parâmetros na instrução SQL são associados como uma unidade a uma matriz de estruturas que contêm as variáveis individuais dos parâmetros.  
  
     A associação é especificada chamando **SQLSetStmtAttr** com *atributo* definido como SQL_ATTR_ROW_BIND_TYPE e *ValuePtr* definido como o tamanho reter a estrutura de colunas do conjunto de variáveis que receberão o resultado.  
  
 O aplicativo também define SQL_ATTR_ROW_ARRAY_SIZE como o número de elementos nas matrizes da coluna ou da linha e define SQL_ATTR_ROW_STATUS_PTR e SQL_ATTR_ROWS_FETCHED_PTR.  
  
## <a name="see-also"></a>Consulte Também  
 [Resultados do processamento &#40; ODBC &#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
