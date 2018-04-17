---
title: Indicador de tipo de dados C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43a9c02694e121eb653d70693587d5728931f747
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="bookmark-c-data-type"></a>Tipo de dados de indicador C
O tipo de dados C de indicador permite que um aplicativo recupere um indicador. Os tipos de indicador C são usados somente para recuperar valores de indicador que podem ser variável em comprimento; eles não devem ser convertidos em outros tipos de dados. Um aplicativo recupera um indicador de coluna 0 do resultado definido com **SQLBulkOperations** (com uma operação de SQL_ADD), **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData**. Para obter mais informações, consulte [indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 A tabela a seguir lista o valor de *CType* para o tipo de dados de indicador C, o tipo de dados ODBC C que implementa o tipo de dados do indicador C e a definição de dados de tipo de SQL. H.  
  
> [!NOTE]  
>  O tipo de dados SQL_C_BOOKMARK foi preterido. ODBC 3*. x* aplicativos não devem usar SQL_C_BOOKMARK. ODBC 3*. x* drivers precisam oferecer suporte a SQL_C_BOOKMARK apenas se desejar trabalhar com ODBC 2. *x* aplicativos que o utilizam. O Gerenciador de Driver SQL_C_VARBOOKMARK é mapeado para SQL_C_BOOKMARK quando um aplicativo funciona com um ODBC 2. *x* driver.  
  
|Identificador de tipo C|Typedef ODBC C|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Preterido)|INDICADOR|int longo não assinado|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
