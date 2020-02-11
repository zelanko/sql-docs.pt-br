---
title: Tipo de dados de indicador C | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86488da93470a61a54638e9c60e6e1795a9da4dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125749"
---
# <a name="bookmark-c-data-type"></a>Tipo de dados do indicador C
O tipo de dados Bookmark C permite que um aplicativo recupere um indicador. Os tipos de indicador C são usados somente para recuperar valores de indicadores que podem ser variáveis de comprimento; Eles não devem ser convertidos em outros tipos de dados. Um aplicativo recupera um indicador da coluna 0 do conjunto de resultados com **SQLBulkOperations** (com uma operação de SQL_ADD), **SQLFetch**, **SQLFetchScroll**ou **SQLGetData**. Para obter mais informações, consulte [indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 A tabela a seguir lista o valor de *CType* para o tipo de dados Bookmark c, o tipo de dados ODBC C que implementa o tipo de dados Bookmark c e a definição desse tipo de dados do SQL. T.  
  
> [!NOTE]
>  O tipo de dados SQL_C_BOOKMARK foi preterido. Os aplicativos ODBC *3. x* não devem usar SQL_C_BOOKMARK. Os drivers ODBC *3. x* precisam dar suporte a SQL_C_BOOKMARK somente se quiserem trabalhar com aplicativos ODBC *2. x* que o utilizam. O Gerenciador de driver mapeia SQL_C_VARBOOKMARK para SQL_C_BOOKMARK quando um aplicativo funciona com um driver ODBC *2. x* .  
  
|Identificador de tipo C|Typedef C ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Preterido)|Indicador|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
