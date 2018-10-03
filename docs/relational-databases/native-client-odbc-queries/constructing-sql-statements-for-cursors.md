---
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5bfb18fea7b36236ad571dbd9b39301069fb00fc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717904"
---
# <a name="constructing-sql-statements-for-cursors"></a>Construindo instruções SQL para cursores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client usa cursores de servidor para implementar a funcionalidade de cursor definida na especificação de ODBC. Um aplicativo ODBC controla o comportamento do cursor utilizando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para definir atributos de instrução diferentes. Estes são os atributos e seus padrões.  
  
|attribute|Padrão|  
|---------------|-------------|  
|SQL_ATTR_CONCURRENCY|SQL_CONCUR_READ_ONLY|  
|SQL_ATTR_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE|SQL_NONSCROLLABLE|  
|SQL_ATTR_CURSOR_SENSITIVITY|SQL_UNSPECIFIED|  
|SQL_ATTR_ROW_ARRAY_SIZE|1|  
  
 Quando essas opções são definidas como seus padrões no momento em que uma instrução SQL é executada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client não usa um cursor de servidor para implementar o conjunto de resultados; em vez disso, ele usa um conjunto de resultados padrão. Se qualquer uma dessas opções são alteradas em relação aos padrões no momento em que uma instrução SQL é executada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client tenta usar um cursor de servidor para implementar o conjunto de resultados.  
  
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
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], caso uma instrução SQL correspondente a alguma dessas condições seja executada com um cursor de servidor, este é implicitamente convertido em um conjunto de resultados padrão. Após **SQLExecDirect** ou **SQLExecute** retorna SQL_SUCCESS_WITH_INFO, o atributos serão definidos para suas configurações padrão de cursor.  
  
 As instruções SQL que não se enquadram nas categorias acima podem ser executadas com qualquer configuração de atributo da instrução; elas funcionam igualmente bem com um conjunto de resultados padrão ou um cursor de servidor.  
  
## <a name="errors"></a>Erros  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 e posterior, uma tentativa de executar uma instrução que produz vários conjuntos de resultados gera SQL_SUCCESS_WITH INFO, além da seguinte mensagem:  
  
```  
SqlState: 01S02"  
pfNative: 0  
szErrorMsgString: "[Microsoft][SQL Server Native Client][SQL Server]  
               Cursor type changed."  
```  
  
 Aplicativos ODBC que recebem essa mensagem podem chamar [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) para determinar as configurações atuais do cursor.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Executando consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
