---
title: Usando conjuntos de resultados padrão do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a4ad5f55da7e5188b4555fbbfe3c4a3fabdc3ae
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415008"
---
# <a name="using-sql-server-default-result-sets"></a>Usando conjuntos de resultados padrão do SQL Server
  Os atributos padrão de cursor do ODBC são:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 Sempre que esses atributos são definidos como seus padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client usa um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conjunto de resultados padrão. Os conjuntos de resultado padrão podem ser usados para qualquer instrução do SQL com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e são o método mais eficiente para transferir todo um conjunto de resultados para o cliente.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu o suporte para vários conjuntos de resultados ativos (MARS); aplicativos agora podem ter mais de um conjunto de resultados padrão ativo por conexão. O MARS não está habilitado por padrão.  
  
 Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os conjuntos de resultados padrão não ofereciam suporte a várias instruções ativas na mesma conexão. Depois que uma instrução SQL é executada em uma conexão, o servidor não aceita comandos (exceto uma solicitação para cancelar o restante do conjunto de resultados) do cliente nessa conexão até que todas as linhas do conjunto de resultados sejam processadas. Para cancelar o restante de um conjunto de resultados parcialmente processado, chame [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) com o *fOption* parâmetro definido como SQL_CLOSE. Para concluir um conjunto de resultados parcialmente processado e testar a presença de outro conjunto de resultados, chame [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md). Se um aplicativo ODBC tentar um comando em um identificador de conexão antes de um conjunto de resultados padrão foi processado completamente, a chamada gera SQL_ERROR e uma chamada para **SQLGetDiagRec** retorna:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>Consulte também  
 [Como os cursores são implementados](how-cursors-are-implemented.md)  
  
  
