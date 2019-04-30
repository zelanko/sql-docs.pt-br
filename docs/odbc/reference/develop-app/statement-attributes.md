---
title: Atributos de instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e669f02eeb76ba529c75851ce8bf6ff9a7831a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149107"
---
# <a name="statement-attributes"></a>Atributos de instrução
Atributos de instrução são características da instrução. Por exemplo, se usar indicadores e o que o tipo de cursor a ser usado com o resultado da instrução conjunto são atributos de instrução.  
  
 Atributos de instrução são definidos com **SQLSetStmtAttr** e suas configurações atuais são recuperadas com **SQLGetStmtAttr**. Não há nenhum requisito de que um aplicativo definir quaisquer atributos de instrução; todos os atributos de instrução têm padrões, alguns dos quais são específicos do driver.  
  
 Quando um atributo de instrução pode ser definido depende do próprio atributo. Os atributos de instrução SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS devem ser definidos antes que a instrução é executada. Os atributos de instrução SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN podem ser definidos a qualquer momento, mas não são aplicados até que a instrução é usada novamente. Atributos de instrução SQL_ATTR_MAX_LENGTH e SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT podem ser definidos a qualquer momento, mas é específica do driver elas são aplicadas antes que a instrução é usada novamente. Os atributos de instrução restantes podem ser definidos a qualquer momento.  
  
> [!NOTE]  
>  A capacidade de definir atributos de instrução no nível de conexão chamando **SQLSetConnectAttr** foi preterido no ODBC 3. *x*. ODBC 3. *x* aplicativos nunca devem definir atributos de instrução no nível de conexão. ODBC 3. *x* drivers precisam dar suporte apenas essa funcionalidade se eles devem funcionar com o ODBC 2. *x* aplicativos. Para obter mais informações, consulte [mapeamento SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores.  
>   
>  Uma exceção a isso é que os atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e podem ser definidos no nível de conexão ou no nível de instrução.  
>   
>  Nenhum dos atributos de instrução introduzidos no ODBC 3. *x* (exceto SQL_ATTR_METADATA_ID) podem ser definidas no nível de conexão.  
  
 Para obter mais informações, consulte o [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descrição da função.
