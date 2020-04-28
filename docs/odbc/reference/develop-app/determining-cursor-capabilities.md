---
title: Determinando os recursos do cursor | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305877"
---
# <a name="determining-cursor-capabilities"></a>Determinar os recursos de cursor
As quatro opções a seguir em **SQLGetInfo** descrevem quais tipos de cursores têm suporte e quais são seus recursos:  
  
-   SQL_CURSOR_SENSITIVITY. Indica se um cursor é sensível a alterações feitas por outro cursor.  
  
-   SQL_SCROLL_OPTIONS. Lista os tipos de cursor com suporte (somente avanço, estático, controlado por conjunto de chaves, dinâmico ou misto). Todas as fontes de dados devem dar suporte a cursores somente de avanço.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo do cursor). Lista os tipos de busca com suporte pelos cursores roláveis. Os bits no valor de retorno correspondem aos tipos de busca em **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 ou SQL_STATIC_CURSOR_ATTRIBUTES2 (dependendo do tipo do cursor). Lista se cursores estáticos e controlados por conjunto de chaves podem detectar suas próprias atualizações, exclusões e inserções.  
  
 Um aplicativo pode determinar os recursos de cursor em tempo de execução chamando **SQLGetInfo** com essas opções. Isso é normalmente feito por aplicativos genéricos. Os recursos de cursor também podem ser determinados durante o desenvolvimento de aplicativos e seu uso embutido no aplicativo. Isso é normalmente feito por aplicativos verticais e personalizados, mas também pode ser feito por aplicativos genéricos que usam uma implementação de cursor do lado do cliente, como a biblioteca de cursores ODBC.
