---
title: Atribuindo armazenamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 322c6b7f9ae296ca59186af8a5eb865d28ff41de
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775910"
---
# <a name="assigning-storage"></a>Atribuindo armazenamento
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Um aplicativo pode atribuir armazenamento para resultados antes ou depois de executar uma instrução SQL. Caso prepare ou execute a instrução SQL primeiro, um aplicativo pode consultar o conjunto de resultados antes de atribuir o armazenamento para resultados. Por exemplo, caso o conjunto de resultados seja desconhecido, o aplicativo deve recuperar o número de colunas antes de atribuir o armazenamento a eles.  
  
 Para associar o armazenamento de uma coluna de dados, um aplicativo chama [SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)e o passa:  
  
-   O tipo de dados no qual os dados serão convertidos.  
  
-   O endereço de um buffer de saída para os dados.  
  
     O aplicativo deve alocar esse buffer e ser grande o bastante para manter os dados na forma em que são convertidos.  
  
-   O comprimento do buffer de saída.  
  
     Esse valor será ignorado se os dados retornados tiverem uma largura fixa em C como, por exemplo, um inteiro, número real ou estrutura de data.  
  
-   O endereço de um buffer de armazenamento no qual retornar o número de bytes de dados disponíveis.  
  
 Um aplicativo também pode associar colunas de conjunto de resultados a matrizes de variáveis de programa para oferecer suporte à busca das linhas de conjunto de resultados em blocos. Há dois tipos diferentes de associação de matriz:  
  
-   A associação que reconhece a coluna é concluída quando cada coluna é associada a sua própria matriz de variáveis.  
  
     A associação de coluna é especificada chamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com o *atributo* definido como SQL_ATTR_ROW_BIND_TYPE e *ValuePtr* definido como SQL_BIND_BY_COLUMN. Todos as matrizes devem ter o mesmo número de elementos.  
  
-   A associação que reconhece a linha é concluída quando todos os parâmetros na instrução SQL são associados como uma unidade a uma matriz de estruturas que contêm as variáveis individuais dos parâmetros.  
  
     A associação de linha é especificada chamando **SQLSetStmtAttr** com o *atributo* definido como SQL_ATTR_ROW_BIND_TYPE e *ValuePtr* definido como o tamanho da estrutura que contém as variáveis que receberão as colunas do conjunto de resultados.  
  
 O aplicativo também define SQL_ATTR_ROW_ARRAY_SIZE como o número de elementos nas matrizes da coluna ou da linha e define SQL_ATTR_ROW_STATUS_PTR e SQL_ATTR_ROWS_FETCHED_PTR.  
  
## <a name="see-also"></a>Consulte Também  
 [Processando resultados &#40;&#41;ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
