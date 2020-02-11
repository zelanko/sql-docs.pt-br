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
ms.openlocfilehash: c74f1a79ef79b682bc2900d671e07bbe34c4dbf5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107270"
---
# <a name="statement-attributes"></a>Atributos de instrução
Atributos de instrução são características da instrução. Por exemplo, se é para usar indicadores e que tipo de cursor usar com o conjunto de resultados da instrução são atributos de instrução.  
  
 Os atributos de instrução são definidos com **SQLSetStmtAttr** e suas configurações atuais recuperadas com **SQLGetStmtAttr**. Não há nenhum requisito de que um aplicativo defina atributos de instrução; todos os atributos de instrução têm padrões, alguns dos quais são específicos do driver.  
  
 Quando um atributo de instrução pode ser definido depende do próprio atributo. Os atributos de instrução SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS devem ser definidos antes de a instrução ser executada. Os atributos de instrução SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN podem ser definidos a qualquer momento, mas não são aplicados até que a instrução seja usada novamente. Os atributos de instrução SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS e SQL_ATTR_QUERY_TIMEOUT podem ser definidos a qualquer momento, mas são específicos do driver, sejam eles aplicados antes que a instrução seja usada novamente. Os atributos de instrução restantes podem ser definidos a qualquer momento.  
  
> [!NOTE]  
>  A capacidade de definir atributos de instrução no nível de conexão chamando **SQLSetConnectAttr** foi preterida no ODBC 3. *x*. ODBC 3. os aplicativos *x* nunca devem definir atributos de instrução no nível de conexão. ODBC 3. os drivers *x* precisam apenas de suporte a essa funcionalidade se eles devem funcionar com o ODBC 2. aplicativos *x* . Para obter mais informações, consulte [mapeamento de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no apêndice G: diretrizes de driver para compatibilidade com versões anteriores.  
>   
>  Uma exceção é o SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE atributos, que são atributos de conexão e atributos de instrução e podem ser definidos no nível de conexão ou no nível de instrução.  
>   
>  Nenhum dos atributos de instrução introduzidos no ODBC 3. *x* (exceto para SQL_ATTR_METADATA_ID) pode ser definido no nível de conexão.  
  
 Para obter mais informações, consulte a descrição da função [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) .
