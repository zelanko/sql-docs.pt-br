---
title: Usando cursors (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: be512713462a9518856de2a16db749490ea24366
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306267"
---
# <a name="using-cursors-odbc"></a>Usando cursores (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC dá suporte a um modelo de cursor que permite:  
  
-   Vários tipos de cursor.  
  
-   Recursos de rolagem e posicionamento dentro de um cursor.  
  
-   Várias opções de simultaneidade.  
  
-   Atualizações posicionadas.  
  
 Os aplicativos ODBC raramente declaram e abrem cursores ou usam qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionada com cursor. O ODBC abre automaticamente um cursor para cada conjunto de resultados retornado de uma instrução SQL. As características dos cursores são controladas por atributos de declaração definidos com [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) antes da execução da declaração SQL. As funções API ODBC para o processamento de conjuntos de resultados dão suporte à gama completa de funcionalidades de cursor, como buscar, rolar e posicionar atualizações.  
  
 Esta é uma comparação de como scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] e aplicativos ODBC funcionam com cursores.  
  
|Ação|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBCODBC|  
|------------|------------------------|----------|  
|Definir o comportamento do cursor|Especifique por meio de parâmetros DECLARE CURSOR|Defina atributos do cursor usando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)|  
|Abrir um cursor|DECLARE CURSOR OPEN *cursor_name*|**SQLExecDirect** ou **SQLExecute**|  
|Buscar linhas|FETCH|**SQLFetch** ou [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|Atualização posicionada|Cláusula WHERE CURRENT OF em UPDATE ou DELETE|**SQLSetPos**|  
|Fechar um cursor|FECHAR *CURSOR_NAME* DESLOCEU|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 Os cursores de servidor implementados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte à funcionalidade de modelo do cursor ODBC. O driver do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client usa cursores de servidor para dar suporte à funcionalidade da API ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Como os cursores são implementados](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [Tipos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [Comportamentos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [Propriedades do cursor](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [Detalhes da programação do cursor &#40;&#41;da ODBC](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [Rolando e buscando linhas](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [Atualizações posicionadas &#40;o&#41;da ODBC](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cliente nativo do servidor SQL &#40;&#41;ODBC](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [FECHAR &#40;&#41;Transact-SQL](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARAR CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;&#41;Transact-SQL](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
