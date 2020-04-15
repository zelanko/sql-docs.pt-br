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
ms.openlocfilehash: 067abcfc8aa5bfd781e6656e3ced9f9e1e573e5f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297866"
---
# <a name="assigning-storage"></a>Atribuindo armazenamento
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um aplicativo pode atribuir armazenamento para resultados antes ou depois de executar uma instrução SQL. Caso prepare ou execute a instrução SQL primeiro, um aplicativo pode consultar o conjunto de resultados antes de atribuir o armazenamento para resultados. Por exemplo, caso o conjunto de resultados seja desconhecido, o aplicativo deve recuperar o número de colunas antes de atribuir o armazenamento a eles.  
  
 Para associar o armazenamento a uma coluna de dados, um aplicativo chama [o SQLBindCol](../../relational-databases/native-client-odbc-api/sqlbindcol.md)e passa-o:  
  
-   O tipo de dados no qual os dados serão convertidos.  
  
-   O endereço de um buffer de saída para os dados.  
  
     O aplicativo deve alocar esse buffer e ser grande o bastante para manter os dados na forma em que são convertidos.  
  
-   O comprimento do buffer de saída.  
  
     Esse valor será ignorado se os dados retornados tiverem uma largura fixa em C como, por exemplo, um inteiro, número real ou estrutura de data.  
  
-   O endereço de um buffer de armazenamento no qual retornar o número de bytes de dados disponíveis.  
  
 Um aplicativo também pode associar colunas de conjunto de resultados a matrizes de variáveis de programa para oferecer suporte à busca das linhas de conjunto de resultados em blocos. Há dois tipos diferentes de associação de matriz:  
  
-   A associação que reconhece a coluna é concluída quando cada coluna é associada a sua própria matriz de variáveis.  
  
     A vinculação em termos de coluna é especificada chamando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) com *Atributo* definido como SQL_ATTR_ROW_BIND_TYPE e *ValuePtr* definido como SQL_BIND_BY_COLUMN. Todos as matrizes devem ter o mesmo número de elementos.  
  
-   A associação que reconhece a linha é concluída quando todos os parâmetros na instrução SQL são associados como uma unidade a uma matriz de estruturas que contêm as variáveis individuais dos parâmetros.  
  
     A vinculação em termos de linha é especificada chamando **SQLSetStmtAttr** com *Atributo* definido para SQL_ATTR_ROW_BIND_TYPE e *ValuePtr* definido para o tamanho da estrutura que mantém as variáveis que receberão as colunas do conjunto de resultados.  
  
 O aplicativo também define SQL_ATTR_ROW_ARRAY_SIZE como o número de elementos nas matrizes da coluna ou da linha e define SQL_ATTR_ROW_STATUS_PTR e SQL_ATTR_ROWS_FETCHED_PTR.  
  
## <a name="see-also"></a>Consulte Também  
 [Resultados de processamento &#40;&#41;Da ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
  
