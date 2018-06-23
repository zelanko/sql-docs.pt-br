---
title: Usar cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1458eca20de9624d9a501e7303d4430aaf5a29e0
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35699037"
---
# <a name="using-cursors-odbc"></a>Usando cursores (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC dá suporte a um modelo de cursor que permite:  
  
-   Vários tipos de cursor.  
  
-   Recursos de rolagem e posicionamento dentro de um cursor.  
  
-   Várias opções de simultaneidade.  
  
-   Atualizações posicionadas.  
  
 Os aplicativos ODBC raramente declaram e abrem cursores ou usam qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionada com cursor. O ODBC abre automaticamente um cursor para cada conjunto de resultados retornado de uma instrução SQL. As características dos cursores são controladas por atributos de instrução definidos com [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) antes do comando SQL a instrução é executada. As funções API ODBC para o processamento de conjuntos de resultados dão suporte à gama completa de funcionalidades de cursor, como buscar, rolar e posicionar atualizações.  
  
 Esta é uma comparação de como scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e aplicativos ODBC funcionam com cursores.  
  
|Ação|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|Definir o comportamento do cursor|Especifique por meio de parâmetros DECLARE CURSOR|Definir atributos de cursor usando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)|  
|Abrir um cursor|DECLARE CURSOR aberto *cursor_name*|**SQLExecDirect** ou **SQLExecute**|  
|Buscar linhas|FETCH|**SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|Atualização posicionada|Cláusula WHERE CURRENT OF em UPDATE ou DELETE|**SQLSetPos**|  
|Fechar um cursor|Fechar *cursor_name* DEALLOCATE|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 Os cursores de servidor implementados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte à funcionalidade de modelo do cursor ODBC. O driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa cursores de servidor para dar suporte à funcionalidade da API ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Como os cursores são implementados](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [Tipos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [Comportamentos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [Propriedades do cursor](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [Detalhes da programação de cursor &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [Rolagem e busca de linhas](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [Atualizações posicionadas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
