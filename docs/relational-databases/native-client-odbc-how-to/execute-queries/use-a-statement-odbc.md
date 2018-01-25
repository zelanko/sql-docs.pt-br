---
title: "Use uma instrução (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-how-to
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ff3c37923f2b4d6d81f8e7e1e61c39d030b7168
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="use-a-statement-odbc"></a>Usar uma instrução (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-a-statement"></a>Para usar uma instrução  
  
1.  Chame [SQLAllocHandle](http://go.microsoft.com/fwlink/?LinkId=58396) com um *HandleType* de SQL_HANDLE_STMT para alocar um identificador da instrução.  
  
2.  Outra opção é chamar o [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir opções de instrução ou [SQLGetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) para obter atributos de instrução.  
  
     Para usar cursores de servidor, você deve definir atributos de cursor como valores diferente de seus padrões.  
  
3.  Opcionalmente, se a instrução for executada várias vezes, prepare a instrução para execução com a [Função SQLPrepare](http://go.microsoft.com/fwlink/?LinkId=59360).  
  
4.  Opcionalmente, se a instrução associou marcadores de parâmetro, associe os marcadores de parâmetro para programar variáveis usando [SQLBindParameter](../../../relational-databases/native-client-odbc-api/sqlbindparameter.md). Se a instrução tiver sido preparada, você poderá chamar [SQLNumParams](http://go.microsoft.com/fwlink/?LinkId=58404) e [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md) para localizar o número e características dos parâmetros.  
  
5.  Execute uma instrução diretamente usando SQLExecDirect.  
  
     \- ou –  
  
     Se a instrução tiver sido preparada, execute-a várias vezes usando [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400).  
  
     \- ou –  
  
     Chame uma função de catálogo, que retorna resultados.  
  
6.  Processe os resultados associando as colunas de conjunto de resultados a variáveis do programa, movendo dados das colunas do conjunto de resultados para programar variáveis usando [SQLGetData](../../../relational-databases/native-client-odbc-api/sqlgetdata.md) ou uma combinação de dois métodos.  
  
     Busque uma linha de cada vez no conjunto de resultados de uma instrução.  
  
     \- ou –  
  
     Busque várias linhas por vez no conjunto de resultados usando um cursor em bloco.  
  
     \- ou –  
  
     Chame [SQLRowCount](../../../relational-databases/native-client-odbc-api/sqlrowcount.md) para determinar o número de linhas afetadas por uma instrução INSERT, UPDATE ou DELETE.  
  
     Se a instrução SQL tiver vários conjuntos de resultados, chame [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) no fim de cada conjunto de resultados para ver se há outros conjuntos de resultados para processar.  
  
7.  Depois que os resultados forem processados, as ações a seguir poderão ser necessárias para tornar o identificador da instrução disponível para executar uma nova instrução:  
  
    -   Se você não tiver chamado [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) até ele retornar SQL_NO_DATA, chame [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) para fechar o cursor.  
  
    -   Se você associar marcadores de parâmetro para programar variáveis, chame [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com *Option* definido como SQL_RESET_PARAMS para liberar os parâmetros associados.  
  
    -   Se você associar colunas do conjunto de resultados para programar variáveis, chame [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com *Option* definido como SQL_UNBIND para liberar as colunas associadas.  
  
    -   Para reutilizar o identificador de instrução, vá para Etapa 2.  
  
8.  Chame [SQLFreeHandle](../../../relational-databases/native-client-odbc-api/sqlfreehandle.md) com um *HandleType* de SQL_HANDLE_STMT para liberar o identificador de instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Execução de tópicos de instruções de consultas &#40; ODBC &#41;](../../../relational-databases/native-client-odbc-how-to/execute-queries/executing-queries-how-to-topics-odbc.md)  
  
  
