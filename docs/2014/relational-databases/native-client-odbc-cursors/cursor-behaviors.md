---
title: Comportamentos de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 15aee78cfc531a7b80e034021b26404e5735a0ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005670"
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
  
 Simultaneidade otimista baseada em versão exige uma **timestamp** coluna na tabela base. Se o controle de simultaneidade otimista baseada em versão for solicitado em uma tabela que não tem um **timestamp** coluna, a servidor usa com base em valores simultaneidade otimista.  
  
## <a name="scrollability"></a>Rolagem  
 Quando SQL_ATTR_CURSOR_SCROLLABLE é definido como SQL_SCROLLABLE, o cursor dá suporte a todos os valores diferentes para o *FetchOrientation* parâmetro [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md). Quando SQL_ATTR_CURSOR_SCROLLABLE é definido como SQL_NONSCROLLABLE, o cursor só dá suporte a um *FetchOrientation* valor SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensibilidade  
 Quando SQL_ATTR_CURSOR_SENSITIVITY é definido como SQL_SENSITIVE, o cursor reflete as modificações de dados feitas pelo usuário atual ou confirmadas por outros usuários. Quando SQL_ATTR_CURSOR_SENSITIVITY é definido como SQL_INSENSITIVE, o cursor não reflete as modificações de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Usar cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  