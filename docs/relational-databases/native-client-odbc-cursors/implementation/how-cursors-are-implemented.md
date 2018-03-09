---
title: "Como os cursores são implementados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC], about ODBC cursors
ms.assetid: 2b1d7dd4-08a4-43fc-b3eb-70c183d0941f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 74e0e6396db2bd5a460c69ba5bec8b1caa828698
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="how-cursors-are-implemented"></a>Como os cursores são implementados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Os aplicativos ODBC controlam o comportamento de um cursor definindo um ou mais atributos de instrução antes de executar uma instrução SQL. ODBC tem dois modos diferentes de especificar as características de um cursor:  
  
-   Tipo de cursor  
  
     Tipos de cursor são definidos usando o atributo SQL_ATTR_CURSOR_TYPE de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Os tipos de cursor ODBC são de somente avanço, estático, controlado por conjunto de chaves, misto e dinâmico. Definir o tipo do cursor era o método original de especificação de cursores no ODBC.  
  
-   Comportamento do cursor  
  
     Comportamento do cursor é definido usando os atributos SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY de **SQLSetStmtAttr**. Esses atributos são modelados nas palavras-chave SCROLL e SENSITIVE definidas para a instrução DECLARE CURSOR com base nos padrões ISO. Essas duas opções ISO foram introduzidas no ODBC versão 3.0.  
  
 As características de um cursor ODBC devem ser especificadas com um desses dois métodos, sendo preferível usar o primeiro, ou seja, tipo do cursor ODBC.  
  
 Além de definir o tipo de um cursor, os aplicativos ODBC também definem outras opções, tais como o número de linhas retornadas em cada extração, opções de simultaneidade e níveis de isolamento da transação. Essas opções podem ser definidas para cursores do tipo ODBC (de somente avanço, estático, controlado por conjunto de chaves, misto e dinâmico) ou cursores ISO (rolagem e sensibilidade).  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a várias maneiras de implementar fisicamente os vários tipos de cursores. O driver implementa alguns tipos de cursor usando um conjunto de resultados padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; ele implementa outros como cursores de servidor ou usando a biblioteca de cursores ODBC.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando conjuntos de resultados padrão do SQL Server](../../../relational-databases/native-client-odbc-cursors/implementation/using-sql-server-default-result-sets.md)  
  
-   [Usando cursores de servidor](../../../relational-databases/native-client-odbc-cursors/implementation/using-server-cursors.md)  
  
-   [Biblioteca de cursores ODBC](../../../relational-databases/native-client-odbc-cursors/implementation/odbc-cursor-library.md)  
  
## <a name="see-also"></a>Consulte também  
 [Usando cursores &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
