---
title: Usando cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 190efb4a3c5343eab9f8654009a4a7b3c6d2a6f2
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705537"
---
# <a name="using-cursors-odbc"></a>Usando cursores (ODBC)
  ODBC dá suporte a um modelo de cursor que permite:  
  
-   Vários tipos de cursor.  
  
-   Recursos de rolagem e posicionamento dentro de um cursor.  
  
-   Várias opções de simultaneidade.  
  
-   Atualizações posicionadas.  
  
 Os aplicativos ODBC raramente declaram e abrem cursores ou usam qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionada com cursor. O ODBC abre automaticamente um cursor para cada conjunto de resultados retornado de uma instrução SQL. As características dos cursores são controladas pelos atributos de instrução definidos com [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) antes da execução da instrução SQL. As funções API ODBC para o processamento de conjuntos de resultados dão suporte à gama completa de funcionalidades de cursor, como buscar, rolar e posicionar atualizações.  
  
 Esta é uma comparação de como scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e aplicativos ODBC funcionam com cursores.  
  
|Ação|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBCODBC|  
|------------|------------------------|----------|  
|Definir o comportamento do cursor|Especifique por meio de parâmetros DECLARE CURSOR|Definir atributos de cursor usando [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)|  
|Abrir um cursor|DECLARAR CURSOR aberto *cursor_name*|**SQLExecDirect** ou **SQLExecute**|  
|Buscar linhas|FETCH|**SQLFetch** ou [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)|  
|Atualização posicionada|Cláusula WHERE CURRENT OF em UPDATE ou DELETE|**SQLSetPos**|  
|Fechar um cursor|FECHAR *cursor_name* desalocar|[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)|  
  
 Os cursores de servidor implementados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte à funcionalidade de modelo do cursor ODBC. O driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa cursores de servidor para dar suporte à funcionalidade da API ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Como os cursores são implementados](implementation/how-cursors-are-implemented.md)  
  
-   [Tipos de cursor](cursor-types.md)  
  
-   [Comportamentos de cursor](cursor-behaviors.md)  
  
-   [Propriedades do cursor](properties/cursor-properties.md)  
  
-   [Detalhes de programação do cursor &#40;&#41;ODBC](programming/cursor-programming-details-odbc.md)  
  
-   [Rolando e buscando linhas](../native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [Atualizações posicionadas &#40;&#41;ODBC](positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [FECHAR &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/close-transact-sql)   
 [Cursores](../../relational-databases/cursors.md)   
 [Desalocar &#40;&#41;de Transact-SQL](/sql/t-sql/language-elements/deallocate-transact-sql)   
 [DECLARAR CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [BUSCAR &#40;&#41;de Transact-SQL](/sql/t-sql/language-elements/fetch-transact-sql)   
 [OPEN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/open-transact-sql)  
  
  
