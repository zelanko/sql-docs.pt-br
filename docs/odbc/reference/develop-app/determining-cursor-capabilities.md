---
title: Determinando recursos do cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 984ad8302f2e1695c8df84a64a18042f4cc9e364
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305877"
---
# <a name="determining-cursor-capabilities"></a>Determinar os recursos de cursor
As quatro opções a seguir no **SQLGetInfo** descrevem quais tipos de cursores são suportados e quais são seus recursos:  
  
-   SQL_CURSOR_SENSITIVITY. Indica se um cursor é sensível às alterações feitas por outro cursor.  
  
-   Sql_scroll_options. Lista os tipos de cursor suportados (somente para frente, estático, orientado por chave, dinâmico ou misto). Todas as fontes de dados devem suportar cursores somente para frente.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor). Lista os tipos de busca suportados por cursores roláveis. Os bits no valor de retorno correspondem aos tipos de busca no **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 ou SQL_STATIC_CURSOR_ATTRIBUTES2 (dependendo do tipo do cursor). Lista se os cursores estáticos e orientados por chave podem detectar suas próprias atualizações, exclusões e inserções.  
  
 Um aplicativo pode determinar os recursos do cursor em tempo de execução, ligando para **o SQLGetInfo** com essas opções. Isso é comumente feito por aplicações genéricas. Os recursos do cursor também podem ser determinados durante o desenvolvimento do aplicativo e seu uso codificado no aplicativo. Isso é comumente feito por aplicativos verticais e personalizados, mas também pode ser feito por aplicativos genéricos que usam uma implementação do cursor do lado do cliente, como a biblioteca do cursor ODBC.
