---
title: Cursores de somente avanço rápido (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
- forward-only cursors
- cursors [ODBC], fast forward-only
- ODBC cursors, fast forward-only
ms.assetid: 0707d07e-fc95-42ed-9280-b7e508ac8c62
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 547d833e31e5f2862aace68c87e72b6e73055dce
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006530"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursores de somente avanço rápido (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Quando conectado a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte a otimizações de desempenho para cursores somente de encaminhamento e somente leitura. Os cursores de somente avanço são implementados internamente pelo driver e pelo servidor de maneira bem semelhante a conjuntos de resultados padrão. Além de ter alto desempenho, os cursores de somente avançado também têm essas características:  
  
-   Não há suporte para [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) . As colunas do conjunto de resultados devem ser associadas para programar variáveis.  
  
-   O servidor fecha automaticamente o cursor quando se detecta a extremidade do cursor. O aplicativo ainda deve chamar [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), mas o driver não precisa enviar a solicitação de fechamento para o servidor. Isso economiza uma viagem de ida-e-volta na rede até o servidor.  
  
 O aplicativo solicita cursores de somente avanço usando o atributo da instrução específica do driver SQL_SOPT_SS_CURSOR_OPTIONS. Quando definidos como SQL_CO_FFO, os cursores de somente avanço são habilitados sem busca automática. Quando definida como SQL_CO_FFO_AF, a opção de busca automática também é habilitada. Para obter mais informações sobre a busca prévia, consulte [usar a busca prévia com cursores ODBC](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md).  
  
 Os cursores de somente avanço com busca automática podem ser usados para recuperar um pequeno conjunto de resultados com apenas uma viagem de ida-e-volta até o servidor. Nestas etapas, *n* é o número de linhas a serem retornadas:  
  
1.  Defina SQL_SOPT_SS_CURSOR_OPTIONS como SQL_CO_FFO_AF.  
  
2.  Defina SQL_ATTR_ROW_ARRAY_SIZE como *n* + 1.  
  
3.  Associe as colunas de resultado a matrizes de *n* + 1 elementos (para ser seguro se as *n* + 1 linhas forem realmente buscadas).  
  
4.  Abra o cursor com **SQLExecDirect** ou **SQLExecute**.  
  
5.  Se o status de retorno for SQL_SUCCESS, chame **SQLFreeStmt** ou **SQLCloseCursor** para fechar o cursor. Todos os dados das linhas estarão nas variáveis de programas associados.  
  
 Com essas etapas, **SQLExecDirect** ou **SQLExecute** envia uma solicitação de abertura de cursor com a opção de AutoBusca habilitada. Nessa solicitação única do cliente, o servidor:  
  
-   Abre o cursor.  
  
-   Compila o conjunto de resultados e envia as linhas para o cliente.  
  
-   Como o tamanho do conjunto de linhas foi definido como 1 além do número de linhas do conjunto de resultados, o servidor detecta o final do cursor e o fecha.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes de programação do cursor &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
