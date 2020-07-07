---
title: Usando SQL Server conjuntos de resultados padrão | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ded0e559f7724450fc9787a57c32fd68cf42719b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86000582"
---
# <a name="using-sql-server-default-result-sets"></a>Usando conjuntos de resultados padrão do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Os atributos padrão de cursor do ODBC são:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 Sempre que esses atributos são definidos para seus padrões, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC do Native Client usa um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conjunto de resultados padrão. Os conjuntos de resultado padrão podem ser usados para qualquer instrução do SQL com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e são o método mais eficiente para transferir todo um conjunto de resultados para o cliente.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]introduziu suporte para MARS (vários conjuntos de resultados ativos); Agora, os aplicativos podem ter mais de um conjunto de resultados padrão ativo por conexão. O MARS não está habilitado por padrão.  
  
 Antes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], os conjuntos de resultados padrão não ofereciam suporte a várias instruções ativas na mesma conexão. Depois que uma instrução SQL é executada em uma conexão, o servidor não aceita comandos (exceto uma solicitação para cancelar o restante do conjunto de resultados) do cliente nessa conexão até que todas as linhas do conjunto de resultados sejam processadas. Para cancelar o restante de um conjunto de resultados parcialmente processado, chame [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) ou [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com o parâmetro *fOption* definido como SQL_CLOSE. Para concluir um conjunto de resultados parcialmente processado e testar a presença de outro conjunto de resultados, chame [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md). Se um aplicativo ODBC tentar um comando em um identificador de conexão antes que um conjunto de resultados padrão seja completamente processado, a chamada gerará SQL_ERROR e uma chamada para **SQLGetDiagRec** retornará:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Como os cursores são implementados](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
