---
title: Usando SQL Server conjuntos de resultados padrão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d7101cf4775e5280c22cc27ecae009410d231d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62511681"
---
# <a name="using-sql-server-default-result-sets"></a>Usando conjuntos de resultados padrão do SQL Server
  Os atributos padrão de cursor do ODBC são:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 Sempre que esses atributos são definidos para seus padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] um conjunto de resultados padrão. Os conjuntos de resultado padrão podem ser usados para qualquer instrução do SQL com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e são o método mais eficiente para transferir todo um conjunto de resultados para o cliente.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]introduziu suporte para MARS (vários conjuntos de resultados ativos); Agora, os aplicativos podem ter mais de um conjunto de resultados padrão ativo por conexão. O MARS não está habilitado por padrão.  
  
 Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os conjuntos de resultados padrão não ofereciam suporte a várias instruções ativas na mesma conexão. Depois que uma instrução SQL é executada em uma conexão, o servidor não aceita comandos (exceto uma solicitação para cancelar o restante do conjunto de resultados) do cliente nessa conexão até que todas as linhas do conjunto de resultados sejam processadas. Para cancelar o restante de um conjunto de resultados parcialmente processado, chame [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) com o parâmetro *fOption* definido como SQL_CLOSE. Para concluir um conjunto de resultados parcialmente processado e testar a presença de outro conjunto de resultados, chame [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md). Se um aplicativo ODBC tentar um comando em um identificador de conexão antes que um conjunto de resultados padrão seja completamente processado, a chamada gerará SQL_ERROR e uma chamada para **SQLGetDiagRec** retornará:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Como os cursores são implementados](how-cursors-are-implemented.md)  
  
  
