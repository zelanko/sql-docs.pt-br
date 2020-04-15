---
title: Tipo de dados C do marcador C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 566f1065d30a47b2db234ba1f11f877725189fb7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292286"
---
# <a name="bookmark-c-data-type"></a>Tipo de dados do indicador C
O tipo de dados do marcador C permite que um aplicativo recupere um marcador. Os tipos c do marcador são usados apenas para recuperar valores de marcadores que podem ser variáveis no comprimento; eles não devem ser convertidos para outros tipos de dados. Um aplicativo recupera um marcador da coluna 0 do conjunto de resultados com **SQLBulkOperations** (com uma operação de SQL_ADD), **SQLFetch,** **SQLFetchScroll**ou **SQLGetData**. Para obter mais informações, consulte [Marcadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 A tabela a seguir lista o valor de *CType* para o tipo de dados do marcador C, o tipo de dados ODBC C que implementa o tipo de dados do marcador C e a definição deste tipo de dados do SQL. H.  
  
> [!NOTE]
>  O SQL_C_BOOKMARK tipo de dados foi preterido. Os aplicativos ODBC *3.x* não devem usar SQL_C_BOOKMARK. Os drivers ODBC *3.x* precisam suportar SQL_C_BOOKMARK somente se quiserem trabalhar com aplicativos ODBC *2.x* que o usam. O Driver Manager mapeia SQL_C_VARBOOKMARK para SQL_C_BOOKMARK quando um aplicativo funciona com um driver ODBC *2.x.*  
  
|Identificador de tipo C|Tipo ODBC C|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Preterido)|Indicador|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
