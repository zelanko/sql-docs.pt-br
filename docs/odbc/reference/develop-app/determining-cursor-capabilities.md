---
title: Determinando os recursos de Cursor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 716471786400c030febb62ebf41c8422770a8c09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598365"
---
# <a name="determining-cursor-capabilities"></a>Determinar os recursos de cursor
As quatro opções a seguir no **SQLGetInfo** descrevem quais tipos de cursores têm suporte e quais são seus recursos:  
  
-   SQL_CURSOR_SENSITIVITY. Indica se um cursor é sensível às mudanças feitas pelo outro cursor.  
  
-   SQL_SCROLL_OPTIONS. Lista os tipos de cursor com suporte (somente avanço, estáticos, controlado por, dinâmicos ou mistos). Todas as fontes de dados devem dar suporte a cursores de somente avanço.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo de cursor). Lista os tipos de fetch com suporte pelo cursores roláveis. Os bits no valor de retorno correspondem aos tipos de busca no **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 ou SQL_STATIC_CURSOR_ATTRIBUTES2 (dependendo do tipo de cursor). Indica se os cursores estáticos e controlados por podem detectar suas próprias atualizações, inserções e exclusões.  
  
 Um aplicativo pode determinar os recursos de cursor em tempo de execução chamando **SQLGetInfo** com essas opções. Normalmente, isso é feito por aplicativos genéricos. Recursos de cursor também podem ser determinados durante o desenvolvimento de aplicativo e seu uso embutido em código no aplicativo. Isso normalmente é feito por aplicativos personalizados e verticais, mas também pode ser feito por aplicativos genéricos que usam uma implementação de cursor do lado do cliente, como a biblioteca de cursores ODBC.
