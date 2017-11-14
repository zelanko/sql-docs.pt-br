---
title: "Atributos de instrução | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d50c660ed3b405a7ae9fec6b9c66a9b395605025
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="statement-attributes"></a>Atributos de instrução
Atributos de instrução são características da instrução. Por exemplo, se usar indicadores e o tipo de definição do cursor a ser usado com os resultados da instrução são atributos de instrução.  
  
 Atributos de instrução são definidos com **SQLSetStmtAttr** e suas configurações atuais são recuperadas com **SQLGetStmtAttr**. Não há nenhum requisito de que um aplicativo defina os atributos de instrução; todos os atributos de instrução têm padrões, alguns dos quais são específicos do driver.  
  
 Quando um atributo de instrução pode ser definido depende do próprio atributo. Os atributos de instrução SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS devem ser definidos antes da instrução é executada. Os atributos de instrução SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN podem ser definidos a qualquer momento, mas não são aplicados até que a instrução é usada novamente. É possível definir atributos de instrução SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT a qualquer momento, mas é específica do driver se elas são aplicadas antes que a instrução é usada novamente. Os demais atributos de instrução podem ser definidos a qualquer momento.  
  
> [!NOTE]  
>  A capacidade de definir atributos de instrução no nível de conexão chamando **SQLSetConnectAttr** foi preterido no ODBC 3. *x*. ODBC 3. *x* aplicativos nunca devem definir atributos de instrução no nível de conexão. ODBC 3. *x* drivers necessitam suporte para essa funcionalidade somente se eles devem funcionar com ODBC 2. *x* aplicativos. Para obter mais informações, consulte [SQLSetConnectOption mapeamento](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
>   
>  Uma exceção a isso é os atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e podem ser definidos no nível de conexão ou no nível de instrução.  
>   
>  Nenhum dos atributos de instrução introduzidos no ODBC 3. *x* (exceto SQL_ATTR_METADATA_ID) podem ser definidas no nível de conexão.  
  
 Para obter mais informações, consulte o [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descrição da função.

