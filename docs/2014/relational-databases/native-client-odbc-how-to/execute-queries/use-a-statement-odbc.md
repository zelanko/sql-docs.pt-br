---
title: Use uma instrução (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC]
ms.assetid: f7573f8f-6f21-4e03-8dd5-a5f2ea4878cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 842e862dff7eca85a05df0222989c6ee6390ab89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200330"
---
# <a name="use-a-statement-odbc"></a>Usar uma instrução (ODBC)
    
### <a name="to-use-a-statement"></a>Para usar uma instrução  
  
1.  Chame [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) com um *HandleType* de SQL_HANDLE_STMT para alocar um identificador da instrução.  
  
2.  Outra opção é chamar o [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) para definir opções de instrução ou [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) para obter atributos de instrução.  
  
     Para usar cursores de servidor, você deve definir atributos de cursor como valores diferente de seus padrões.  
  
3.  Opcionalmente, se a instrução for executada várias vezes, prepare a instrução para execução com a [Função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360).  
  
4.  Opcionalmente, se a instrução associou marcadores de parâmetro, associe os marcadores de parâmetro para programar variáveis usando [SQLBindParameter](../../native-client-odbc-api/sqlbindparameter.md). Se a instrução tiver sido preparada, você poderá chamar [SQLNumParams](https://go.microsoft.com/fwlink/?LinkId=58404) e [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md) para localizar o número e características dos parâmetros.  
  
5.  Execute uma instrução diretamente usando SQLExecDirect.  
  
     \- ou –  
  
     Se a instrução tiver sido preparada, execute-a várias vezes usando [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400).  
  
     \- ou –  
  
     Chame uma função de catálogo, que retorna resultados.  
  
6.  Processe os resultados associando as colunas de conjunto de resultados a variáveis do programa, movendo dados das colunas do conjunto de resultados para programar variáveis usando [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) ou uma combinação de dois métodos.  
  
     Busque uma linha de cada vez no conjunto de resultados de uma instrução.  
  
     \- ou –  
  
     Busque várias linhas por vez no conjunto de resultados usando um cursor em bloco.  
  
     \- ou –  
  
     Chame [SQLRowCount](../../native-client-odbc-api/sqlrowcount.md) para determinar o número de linhas afetadas por uma instrução INSERT, UPDATE ou DELETE.  
  
     Se a instrução SQL tiver vários conjuntos de resultados, chame [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) no fim de cada conjunto de resultados para ver se há outros conjuntos de resultados para processar.  
  
7.  Depois que os resultados forem processados, as ações a seguir poderão ser necessárias para tornar o identificador da instrução disponível para executar uma nova instrução:  
  
    -   Se você não tiver chamado [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) até ele retornar SQL_NO_DATA, chame [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) para fechar o cursor.  
  
    -   Se você associar marcadores de parâmetro para programar variáveis, chame [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) com *Option* definido como SQL_RESET_PARAMS para liberar os parâmetros associados.  
  
    -   Se você associar colunas do conjunto de resultados para programar variáveis, chame [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) com *Option* definido como SQL_UNBIND para liberar as colunas associadas.  
  
    -   Para reutilizar o identificador de instrução, vá para Etapa 2.  
  
8.  Chame [SQLFreeHandle](../../native-client-odbc-api/sqlfreehandle.md) com um *HandleType* de SQL_HANDLE_STMT para liberar o identificador de instrução.  
  
## <a name="see-also"></a>Consulte também  
 [Executar consultas de tópicos de instruções &#40;ODBC&#41;](executing-queries-how-to-topics-odbc.md)  
  
  
