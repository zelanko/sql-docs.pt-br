---
title: Atributos de declaração | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299639"
---
# <a name="statement-attributes"></a>Atributos de instrução
Os atributos de declaração são características da declaração. Por exemplo, se usar marcadores e que tipo de cursor usar com o conjunto de resultados da declaração são atributos de declaração.  
  
 Os atributos de declaração são definidos com **SQLSetStmtAttr** e suas configurações atuais recuperadas com **SQLGetStmtAttr**. Não há nenhuma exigência de que um aplicativo defina quaisquer atributos de declaração; todos os atributos de instrução têm padrões, alguns dos quais são específicos do driver.  
  
 Quando um atributo de declaração pode ser definido depende do próprio atributo. Os atributos de declaração SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_TYPE, SQL_ATTR_SIMULATE_CURSOR e SQL_ATTR_USE_BOOKMARKS devem ser definidos antes da execução da declaração. Os atributos de declaração SQL_ATTR_ASYNC_ENABLE e SQL_ATTR_NOSCAN podem ser definidos a qualquer momento, mas não são aplicados até que a declaração seja usada novamente. SQL_ATTR_MAX_LENGTH, SQL_ATTR_MAX_ROWS e SQL_ATTR_QUERY_TIMEOUT atributos de declaração podem ser definidos a qualquer momento, mas é específico do motorista se eles são aplicados antes que a instrução seja usada novamente. Os atributos de declaração restantes podem ser definidos a qualquer momento.  
  
> [!NOTE]  
>  A capacidade de definir atributos de declaração no nível de conexão, chamando **SQLSetConnectAttr,** foi preterida no ODBC 3. *x*. ODBC 3. *x* aplicativos nunca devem definir atributos de declaração no nível de conexão. ODBC 3. *x* drivers só precisam suportar essa funcionalidade se eles devem trabalhar com ODBC 2. *x* aplicações. Para obter mais informações, consulte [SQLSetConnectOption Mapping](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md) no apêndice G: Diretrizes do driver para compatibilidade retrógrada.  
>   
>  Uma exceção a isso são os atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de declaração e podem ser definidos tanto no nível de conexão quanto no nível de declaração.  
>   
>  Nenhum dos atributos de declaração introduzidos no ODBC 3. *x* (exceto SQL_ATTR_METADATA_ID) pode ser configurado no nível de conexão.  
  
 Para obter mais informações, consulte a descrição da função [SQLSetStmtAttr.](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)
