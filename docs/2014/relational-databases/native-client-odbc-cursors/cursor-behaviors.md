---
title: Comportamentos de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
author: rothja
ms.author: jroth
ms.openlocfilehash: 89c7c4e9a8dcffe03dd12f8013d5ed43810547f3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021072"
---
# <a name="cursor-behaviors"></a>Comportamentos de cursor
  O ODBC dá suporte às opções ISO para especificar o comportamento de cursores por meio da definição de sua rolagem e sensibilidade. Esses comportamentos são especificados definindo as opções SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY em uma chamada para [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md). O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa essas opções solicitando cursores de servidor com as características a seguir.  
  
|Configurações do comportamento de cursor|Características de cursor do servidor solicitadas|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE e SQL_SENSITIVE|Cursor controlado por conjunto de chaves e simultaneidade otimista baseada em versão|  
|SQL_SCROLLABLE e SQL_INSENSITIVE|Cursor estático e simultaneidade somente leitura|  
|SQL_SCROLLABLE e SQL_UNSPECIFIED|Cursor estático e simultaneidade somente leitura|  
|SQL_NONSCROLLABLE e SQL_SENSITIVE|Cursor de somente avanço e simultaneidade otimista baseada em versão|  
|SQL_NONSCROLLABLE e SQL_INSENSITIVE|Conjunto de resultados padrão (somente avanço, somente leitura)|  
|SQL_NONSCROLLABLE e SQL_UNSPECIFIED|Conjunto de resultados padrão (somente avanço, somente leitura)|  
  
 A simultaneidade otimista baseada em versão requer uma coluna **timestamp** na tabela subjacente. Se o controle de simultaneidade otimista baseado em versão for solicitado em uma tabela que não tem uma coluna **timestamp** , o servidor usará a simultaneidade otimista com base em valores.  
  
## <a name="scrollability"></a>Rolagem  
 Quando SQL_ATTR_CURSOR_SCROLLABLE é definido como SQL_SCROLLABLE, o cursor dá suporte a todos os valores diferentes para o parâmetro *FetchOrientation* de [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md). Quando SQL_ATTR_CURSOR_SCROLLABLE é definido como SQL_NONSCROLLABLE, o cursor só dá suporte a um valor de *FetchOrientation* de SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensibilidade  
 Quando SQL_ATTR_CURSOR_SENSITIVITY é definido como SQL_SENSITIVE, o cursor reflete as modificações de dados feitas pelo usuário atual ou confirmadas por outros usuários. Quando SQL_ATTR_CURSOR_SENSITIVITY é definido como SQL_INSENSITIVE, o cursor não reflete as modificações de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Usando cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
