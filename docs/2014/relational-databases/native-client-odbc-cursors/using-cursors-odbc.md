---
title: Usando cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
caps.latest.revision: 35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee00b752236032b7123eb557e82bed12de8ecb00
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37416345"
---
# <a name="using-cursors-odbc"></a>Usando cursores (ODBC)
  ODBC dá suporte a um modelo de cursor que permite:  
  
-   Vários tipos de cursor.  
  
-   Recursos de rolagem e posicionamento dentro de um cursor.  
  
-   Várias opções de simultaneidade.  
  
-   Atualizações posicionadas.  
  
 Os aplicativos ODBC raramente declaram e abrem cursores ou usam qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionada com cursor. O ODBC abre automaticamente um cursor para cada conjunto de resultados retornado de uma instrução SQL. As características dos cursores são controladas por atributos de instrução definidos com [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) antes do SQL de instrução é executada. As funções API ODBC para o processamento de conjuntos de resultados dão suporte à gama completa de funcionalidades de cursor, como buscar, rolar e posicionar atualizações.  
  
 Esta é uma comparação de como scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e aplicativos ODBC funcionam com cursores.  
  
|Ação|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|Definir o comportamento do cursor|Especifique por meio de parâmetros DECLARE CURSOR|Definir atributos de cursor usando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)|  
|Abrir um cursor|DECLARE CURSOR aberto *cursor_name*|**SQLExecDirect** ou **SQLExecute**|  
|Buscar linhas|FETCH|**SQLFetch** ou [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)|  
|Atualização posicionada|Cláusula WHERE CURRENT OF em UPDATE ou DELETE|**SQLSetPos**|  
|Fechar um cursor|Fechar *cursor_name* DEALLOCATE|[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)|  
  
 Os cursores de servidor implementados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte à funcionalidade de modelo do cursor ODBC. O driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa cursores de servidor para dar suporte à funcionalidade da API ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Como os cursores são implementados](implementation/how-cursors-are-implemented.md)  
  
-   [Tipos de cursor](cursor-types.md)  
  
-   [Comportamentos de cursor](cursor-behaviors.md)  
  
-   [Propriedades do cursor](properties/cursor-properties.md)  
  
-   [Detalhes de programação de cursor &#40;ODBC&#41;](programming/cursor-programming-details-odbc.md)  
  
-   [Rolagem e busca de linhas](../native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [Atualizações posicionadas &#40;ODBC&#41;](positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/close-transact-sql)   
 [Cursores](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/deallocate-transact-sql)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [FETCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/fetch-transact-sql)   
 [OPEN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/open-transact-sql)  
  
  
