---
title: Indicador de tipo de dados C | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b81acf6c60bd11e03a598e349e145dbf72e174b4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205285"
---
# <a name="bookmark-c-data-type"></a>Tipo de dados do indicador C
O indicador de tipo de dados C permite que um aplicativo recupere um indicador. Os tipos de indicador C são usados apenas para recuperar valores de indicador que podem ser variável em comprimento; eles não devem ser convertidos em outros tipos de dados. Um aplicativo recupera um indicador de coluna 0 do resultado definido com **SQLBulkOperations** (com uma operação de SQL_ADD), **SQLFetch**, **SQLFetchScroll**, ou **SQLGetData**. Para obter mais informações, consulte [indicadores](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 A tabela a seguir lista o valor de *CType* para o tipo de dados do indicador C, o tipo de dados ODBC C que implementa o tipo de dados do indicador C e a definição de dados do tipo do SQL. H.  
  
> [!NOTE]
>  O tipo de dados SQL_C_BOOKMARK foi preterido. 3 de ODBC *. x* aplicativos não devem usar SQL_C_BOOKMARK. 3 de ODBC *. x* drivers precisam suportar SQL_C_BOOKMARK somente se eles desejam trabalhar com ODBC 2. *x* aplicativos que usá-lo. O Gerenciador de Driver mapeia SQL_C_VARBOOKMARK para SQL_C_BOOKMARK quando o aplicativo funciona com um ODBC 2. *x* driver.  
  
|Identificador de tipo C|Typedef ODBC C|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Preterido)|INDICADOR|inteiro longo|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
