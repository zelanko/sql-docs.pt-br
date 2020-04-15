---
title: Cursors rápidos somente para frente (ODBC) | Microsoft Docs
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
ms.openlocfilehash: 50d79875e0f3f661c0a959f50ce68c4f2761d186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298409"
---
# <a name="fast-forward-only-cursors-odbc"></a>Cursores de somente avanço rápido (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Quando conectado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de , o driver Cliente Nativo ODBC suporta otimizações de desempenho para cursores somente de leitura para frente. Os cursores de somente avanço são implementados internamente pelo driver e pelo servidor de maneira bem semelhante a conjuntos de resultados padrão. Além de ter alto desempenho, os cursores de somente avançado também têm essas características:  
  
-   [O SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) não é suportado. As colunas do conjunto de resultados devem ser associadas para programar variáveis.  
  
-   O servidor fecha automaticamente o cursor quando se detecta a extremidade do cursor. O aplicativo ainda deve ligar para [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)(SQL_CLOSE), mas o driver não precisa enviar a solicitação próxima ao servidor. Isso economiza uma viagem de ida-e-volta na rede até o servidor.  
  
 O aplicativo solicita cursores de somente avanço usando o atributo da instrução específica do driver SQL_SOPT_SS_CURSOR_OPTIONS. Quando definidos como SQL_CO_FFO, os cursores de somente avanço são habilitados sem busca automática. Quando definida como SQL_CO_FFO_AF, a opção de busca automática também é habilitada. Para obter mais informações sobre autofetch, consulte [Usando autofetch com Cursors ODBC](../../../relational-databases/native-client-odbc-cursors/programming/using-autofetch-with-odbc-cursors.md).  
  
 Os cursores de somente avanço com busca automática podem ser usados para recuperar um pequeno conjunto de resultados com apenas uma viagem de ida-e-volta até o servidor. Nestas etapas, *n* é o número de linhas a serem devolvidas:  
  
1.  Defina SQL_SOPT_SS_CURSOR_OPTIONS como SQL_CO_FFO_AF.  
  
2.  Definir SQL_ATTR_ROW_ARRAY_SIZE para *n* + 1.  
  
3.  Vincule as colunas de resultado a matrizes de *n* + 1 elementos (para ser seguro se *n* + 1 linhas forem realmente buscadas).  
  
4.  Abra o cursor com **SQLExecDirect** ou **SQLExecute**.  
  
5.  Se o status de retorno for SQL_SUCCESS, ligue para **SQLFreeStmt** ou **SQLCloseCursor** para fechar o cursor. Todos os dados das linhas estarão nas variáveis de programas associados.  
  
 Com essas etapas, o **SQLExecDirect** ou **o SQLExecute** enviam uma solicitação aberta do cursor com a opção autofetch ativada. Nessa solicitação única do cliente, o servidor:  
  
-   Abre o cursor.  
  
-   Compila o conjunto de resultados e envia as linhas para o cliente.  
  
-   Como o tamanho do conjunto de linhas foi definido como 1 além do número de linhas do conjunto de resultados, o servidor detecta o final do cursor e o fecha.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhes da programação do cursor &#40;&#41;da ODBC](../../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
  
