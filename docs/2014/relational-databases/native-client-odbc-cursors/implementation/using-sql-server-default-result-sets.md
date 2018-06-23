---
title: Usando conjuntos de resultados padrão do SQL Server | Microsoft Docs
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
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e4b818f3ec580468a3ae1120709ffaa9c19a8ffe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122386"
---
# <a name="using-sql-server-default-result-sets"></a>Usando conjuntos de resultados padrão do SQL Server
  Os atributos padrão de cursor do ODBC são:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 Sempre que esses atributos são definidos como seus padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client usa um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conjunto de resultados padrão. Os conjuntos de resultado padrão podem ser usados para qualquer instrução do SQL com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e são o método mais eficiente para transferir todo um conjunto de resultados para o cliente.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Introdução de suporte para vários conjuntos de resultados ativos (MARS); aplicativos agora podem ter mais de um conjunto de resultados padrão ativo por conexão. O MARS não está habilitado por padrão.  
  
 Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os conjuntos de resultados padrão não ofereciam suporte a várias instruções ativas na mesma conexão. Depois que uma instrução SQL é executada em uma conexão, o servidor não aceita comandos (exceto uma solicitação para cancelar o restante do conjunto de resultados) do cliente nessa conexão até que todas as linhas do conjunto de resultados sejam processadas. Para cancelar o restante de um conjunto de resultados parcialmente processado, chame [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) com o *fOption* parâmetro definido como SQL_CLOSE. Para concluir um conjunto de resultados parcialmente processado e testar a presença de outro conjunto de resultados, chame [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md). Se um aplicativo ODBC tentar um comando em um identificador de conexão antes de um conjunto de resultados padrão foi processado completamente, a chamada gerará SQL_ERROR e uma chamada para **SQLGetDiagRec** retorna:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como os cursores são implementados](how-cursors-are-implemented.md)  
  
  