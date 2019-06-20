---
title: Como os cursores são implementados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c92391b1d8874da3a8901ccc5c6245e48334241
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188522"
---
# <a name="how-cursors-are-implemented"></a>Como os cursores são implementados
  Os aplicativos ODBC controlam o comportamento de um cursor definindo um ou mais atributos de instrução antes de executar uma instrução SQL. ODBC tem dois modos diferentes de especificar as características de um cursor:  
  
-   Tipo de cursor  
  
     Tipos de cursor são definidos usando o atributo SQL_ATTR_CURSOR_TYPE [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). Os tipos de cursor ODBC são de somente avanço, estático, controlado por conjunto de chaves, misto e dinâmico. Definir o tipo do cursor era o método original de especificação de cursores no ODBC.  
  
-   Comportamento do cursor  
  
     Comportamento do cursor é definido usando os atributos SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY de **SQLSetStmtAttr**. Esses atributos são modelados nas palavras-chave SCROLL e SENSITIVE definidas para a instrução DECLARE CURSOR com base nos padrões ISO. Essas duas opções ISO foram introduzidas no ODBC versão 3.0.  
  
 As características de um cursor ODBC devem ser especificadas com um desses dois métodos, sendo preferível usar o primeiro, ou seja, tipo do cursor ODBC.  
  
 Além de definir o tipo de um cursor, os aplicativos ODBC também definem outras opções, tais como o número de linhas retornadas em cada extração, opções de simultaneidade e níveis de isolamento da transação. Essas opções podem ser definidas para cursores do tipo ODBC (de somente avanço, estático, controlado por conjunto de chaves, misto e dinâmico) ou cursores ISO (rolagem e sensibilidade).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client dá suporte a várias maneiras de implementar fisicamente os vários tipos de cursores. O driver implementa alguns tipos de cursor usando um conjunto de resultados padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; ele implementa outros como cursores de servidor ou usando a biblioteca de cursores ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando conjuntos de resultados padrão do SQL Server](using-sql-server-default-result-sets.md)  
  
-   [Usando cursores de servidor](using-server-cursors.md)  
  
-   [Biblioteca de cursores ODBC](odbc-cursor-library.md)  
  
## <a name="see-also"></a>Consulte também  
 [Uso de cursores &#40;ODBC&#41;](../using-cursors-odbc.md)  
  
  
