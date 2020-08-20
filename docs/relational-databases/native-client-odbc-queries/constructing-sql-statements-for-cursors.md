---
description: Construindo instruções SQL para cursores
title: Construindo instruções SQL para cursores | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], statement construction
- ODBC applications, cursors
- SQL Server Native Client ODBC driver, statements
- statements [ODBC], constructing
- ODBC applications, statements
- statements [ODBC], cursors
ms.assetid: 134003fd-9c93-4f5c-a988-045990933b80
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a67f2a7ed3d01ee3a98356efc4c15cf2865ee154
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470384"
---
# <a name="constructing-sql-statements-for-cursors"></a>Construindo instruções SQL para cursores
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client usa cursores de servidor para implementar a funcionalidade de cursor definida na especificação ODBC. Um aplicativo ODBC controla o comportamento do cursor usando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir atributos de instrução diferentes. Estes são os atributos e seus padrões.  
  
|Atributo|Padrão|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 Quando essas opções são definidas para seus padrões no momento em que uma instrução SQL é executada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client não usa um cursor de servidor para implementar o conjunto de resultados; em vez disso, ele usa um conjunto de resultados padrão. Se qualquer uma dessas opções for alterada de seus padrões no momento em que uma instrução SQL for executada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client tentará usar um cursor de servidor para implementar o conjunto de resultados.  
  
 Conjuntos de resultados padrão oferecem suporte a todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Não há nenhuma restrição quanto aos tipos de instruções SQL que podem ser executados ao usar um conjunto de resultados padrão.  
  
 Os cursores de servidor não oferecem suporte a todas as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Os cursores de servidor não oferecem suporte a nenhuma instrução SQL que gera vários conjuntos de resultados.  
  
 Os seguintes tipos de instruções não oferecem suporte por meio de cursores de servidor:  
  
-   Lotes  
  
     Instruções SQL criadas a partir de duas ou mais instruções SQL SELECT individuais, por exemplo:  
  
    ```  
    SELECT * FROM Authors; SELECT * FROM Titles  
    ```  
  
-   Procedimentos armazenados com várias instruções SELECT  
  
     As instruções SQL que executam um procedimento armazenado contendo mais de uma instrução SELECT. Isso inclui instruções SELECT que preenchem parâmetros ou variáveis.  
  
-   Palavras-chave  
  
     Instruções SQL que contêm as palavras-chave FOR BROWSE ou INTO.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], caso uma instrução SQL correspondente a alguma dessas condições seja executada com um cursor de servidor, este é implicitamente convertido em um conjunto de resultados padrão. Após **SQLExecDirect** ou **SQLExecute** retornar SQL_SUCCESS_WITH_INFO, os atributos de cursor serão definidos de volta para suas configurações padrão.  
  
 As instruções SQL que não se enquadram nas categorias acima podem ser executadas com qualquer configuração de atributo da instrução; elas funcionam igualmente bem com um conjunto de resultados padrão ou um cursor de servidor.  
  
## <a name="errors"></a>Errors  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 e posterior, uma tentativa de executar uma instrução que produz vários conjuntos de resultados gera SQL_SUCCESS_WITH INFO, além da seguinte mensagem:  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 Os aplicativos ODBC que recebem essa mensagem podem chamar [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) para determinar as configurações atuais do cursor.  
  
 Uma tentativa de executar um procedimento com várias instruções SELECT durante o uso de cursores de servidor gera o seguinte erro:  
  
```  
SqlState: 42000  
pfNative: 16937  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               A server cursor is not allowed on a stored procedure  
               with more than one SELECT statement in it. Use a  
               default result set or client cursor.  
```  
  
 Uma tentativa de executar um lote com várias instruções SELECT durante o uso de cursores de servidor gera o seguinte erro:  
  
```  
SqlState: 42000  
pfNative: 16938  
szErrorMsgString: [Microsoft][SQL Server Native Client][SQL Server]  
               sp_cursoropen. The statement parameter can only  
               be a single SELECT statement or a single stored   
               procedure.  
```  
  
 Aplicativos ODBC que recebem esses erros devem restaurar todos padrões dos atributos de instrução de cursor antes de tentar executá-la.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
