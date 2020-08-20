---
description: Usar cursores (ODBC)
title: Usar cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], how to topics
ms.assetid: c502736f-bca0-45c3-ae25-d2ad52d296bf
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fbb647cc83c9d98aedc15531c919c54f9ae7d53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494064"
---
# <a name="use-cursors-odbc"></a>Usar cursores (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-use-cursors"></a>Para usar cursores  
  
1.  Chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir os atributos de cursor desejados:  
  
     Defina os atributos SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY (esta é a opção preferencial).  
  
     Ou  
  
     Defina os atributos SQL_CURSOR_SCROLLABLE e SQL_CURSOR_SENSITIVITY.  
  
2.  Chame [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir o tamanho do conjunto de linhas usando o atributo SQL_ATTR_ROW_ARRAY_SIZE.  
  
3.  Outra opção será chamar [SQLSetCursorName](https://go.microsoft.com/fwlink/?LinkId=58406) para definir um nome de cursor se as atualizações posicionadas forem feitas usando a cláusula WHERE CURRENT OF.  
  
4.  Execute a instrução SQL.  
  
5.  Outra opção será chamar [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) para definir o nome de cursor se as atualizações posicionadas forem feitas usando a cláusula WHERE CURRENT OF e um nome de cursor não foi fornecido com [SQLSetCursorName](https://go.microsoft.com/fwlink/?LinkId=58406) na Etapa 3.  
  
6.  Chame [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obter o número de colunas (C) no conjunto de linhas.  
  
     Use a associação por coluna.  
  
     \- ou –  
  
     Use a associação por linha.  
  
7.  Busque conjuntos de linhas do cursor conforme desejado.  
  
8.  Chame [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para determinar se outro conjunto de resultados está disponível.  
  
    -   Se SQL_SUCCESS for retornado, outro conjunto de resultados estará disponível.  
  
    -   Se SQL_NO_DATA for retornado, nenhum outro conjunto de resultados estará disponível.  
  
    -   Se SQL_SUCCESS_WITH_INFO ou SQL_ERROR for retornado, chame [SQLGetDiagRec](https://go.microsoft.com/fwlink/?LinkId=58402) para determinar se a saída de uma instrução PRINT ou RAISERROR estará disponível.  
  
     Se parâmetros de instrução associados forem usados para parâmetros de saída ou o valor retornado de um procedimento armazenado, use os dados disponíveis agora nos buffers de parâmetro associados.  
  
     Quando são usados parâmetros associados, cada chamada para [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=58400) ou [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) terá executado a instrução SQL por S vezes, em que S é o número de elementos na matriz de parâmetros associados. Isso significa que haverá S conjuntos de resultados a ser processados, onde cada conjunto consiste em todos os conjuntos de resultados, parâmetros de saída e códigos de retorno normalmente retornados por uma única execução da instrução SQL.  
  
     Observe que, quando um conjunto de resultados contém linhas computadas, cada linha computada é disponibilizada como um conjunto de resultados separado. Esses conjuntos de resultados computados são intercalados nas linhas normais e dividem as linhas normais em vários conjuntos de resultados.  
  
9. Outra opção é chamar [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com SQL_UNBIND para liberar qualquer buffer de coluna associado.  
  
10. Se outro conjunto de resultados estiver disponível, vá para a Etapa 6.  
  
     Na Etapa 9, chamar [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) em um conjunto de resultados parcialmente processado limpa o restante do conjunto de resultados. Outra maneira de limpar um conjunto de resultados parcialmente processado é chamar [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md).  
  
     Você pode controlar o tipo de cursor usado definindo SQL_ATTR_CURSOR_TYPE e SQL_ATTR_CONCURRENCY ou definindo SQL_ATTR_CURSOR_SENSITIVITY e SQL_ATTR_CURSOR_SCROLLABLE. Você não deve misturar os dois métodos de especificação de comportamento de cursor.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre o uso de cursores &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
