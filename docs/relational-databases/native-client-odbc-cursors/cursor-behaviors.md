---
title: Comportamentos de cursor | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: bd5ce2d661903558a0bb564f61a04e889fa071df
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39536216"
---
# <a name="cursor-behaviors"></a>Comportamentos de cursor
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O ODBC dá suporte às opções ISO para especificar o comportamento de cursores por meio da definição de sua rolagem e sensibilidade. Esses comportamentos são especificados definindo as opções SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY em uma chamada para [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa essas opções solicitando cursores de servidor com as características a seguir.  
  
|Configurações do comportamento de cursor|Características de cursor do servidor solicitadas|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE e SQL_SENSITIVE|Cursor controlado por conjunto de chaves e simultaneidade otimista baseada em versão|  
|SQL_SCROLLABLE e SQL_INSENSITIVE|Cursor estático e simultaneidade somente leitura|  
|SQL_SCROLLABLE e SQL_UNSPECIFIED|Cursor estático e simultaneidade somente leitura|  
|SQL_NONSCROLLABLE e SQL_SENSITIVE|Cursor de somente avanço e simultaneidade otimista baseada em versão|  
|SQL_NONSCROLLABLE e SQL_INSENSITIVE|Conjunto de resultados padrão (somente avanço, somente leitura)|  
|SQL_NONSCROLLABLE e SQL_UNSPECIFIED|Conjunto de resultados padrão (somente avanço, somente leitura)|  
  
 Simultaneidade otimista baseada em versão exige uma **carimbo de hora** coluna na tabela subjacente. Se o controle de simultaneidade otimista baseada em versão for solicitado em uma tabela que não tem um **carimbo de hora** coluna, a servidor usa com base em valores a simultaneidade otimista.  
  
## <a name="scrollability"></a>Rolagem  
 Quando SQL_ATTR_CURSOR_SCROLLABLE é definido como SQL_SCROLLABLE, o cursor dá suporte a todos os valores diferentes para o *FetchOrientation* parâmetro do [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Quando SQL_ATTR_CURSOR_SCROLLABLE é definido como SQL_NONSCROLLABLE, o cursor dá suporte apenas a um *FetchOrientation* valor SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensibilidade  
 Quando SQL_ATTR_CURSOR_SENSITIVITY é definido como SQL_SENSITIVE, o cursor reflete as modificações de dados feitas pelo usuário atual ou confirmadas por outros usuários. Quando SQL_ATTR_CURSOR_SENSITIVITY é definido como SQL_INSENSITIVE, o cursor não reflete as modificações de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cursores (ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) [propriedades do Cursor](properties/cursor-properties.md) 
  
  
