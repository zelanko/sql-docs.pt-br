---
title: "Cursores de somente avanço rápido (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9305f67ec1c4146336e3cc55178c093acf28b183
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursores de somente avanço rápido (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Quando conectado a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client oferece suporte a otimizações de desempenho para cursores de somente avanço, somente leitura. Os cursores de somente avanço são implementados internamente pelo driver e pelo servidor de maneira bem semelhante a conjuntos de resultados padrão. Além de ter alto desempenho, os cursores de somente avançado também têm essas características:  
  
-   [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) não tem suporte. As colunas do conjunto de resultados devem ser associadas para programar variáveis.  
  
-   O servidor fecha automaticamente o cursor quando se detecta a extremidade do cursor. O aplicativo ainda deve chamar [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), mas o driver não precisa enviar a solicitação de fechamento para o servidor. Isso economiza uma viagem de ida-e-volta na rede até o servidor.  
  
 O aplicativo solicita cursores de somente avanço usando o atributo da instrução específica do driver SQL_SOPT_SS_CURSOR_OPTIONS. Quando definidos como SQL_CO_FFO, os cursores de somente avanço são habilitados sem busca automática. Quando definida como SQL_CO_FFO_AF, a opção de busca automática também é habilitada. Para obter mais informações sobre a busca automática, consulte [usando a opção de Autofetch com cursores ODBC](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md).  
  
 Os cursores de somente avanço com busca automática podem ser usados para recuperar um pequeno conjunto de resultados com apenas uma viagem de ida-e-volta até o servidor. Nestas etapas,  *n*  é o número de linhas a serem retornadas:  
  
1.  Defina SQL_SOPT_SS_CURSOR_OPTIONS como SQL_CO_FFO_AF.  
  
2.  Defina SQL_ATTR_ROW_ARRAY_SIZE como  *n*  + 1.  
  
3.  Associar as colunas de resultados a matrizes de  *n*  + 1 elementos (seguro se  *n*  + 1 linhas sejam efetivamente buscadas).  
  
4.  Abrir o cursor com um **SQLExecDirect** ou **SQLExecute**.  
  
5.  Se o status de retorno seja SQL_SUCCESS, chame **SQLFreeStmt** ou **SQLCloseCursor** para fechar o cursor. Todos os dados das linhas estarão nas variáveis de programas associados.  
  
 Com essas etapas, o **SQLExecDirect** ou **SQLExecute** envia uma solicitação de cursor aberta com a opção de busca automática habilitada. Nessa solicitação única do cliente, o servidor:  
  
-   Abre o cursor.  
  
-   Compila o conjunto de resultados e envia as linhas para o cliente.  
  
-   Como o tamanho do conjunto de linhas foi definido como 1 além do número de linhas do conjunto de resultados, o servidor detecta o final do cursor e o fecha.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhes de programação de cursor &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
