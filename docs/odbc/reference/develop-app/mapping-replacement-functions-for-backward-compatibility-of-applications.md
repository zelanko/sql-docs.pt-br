---
description: Mapear funções de substituição para compatibilidade com versões anteriores de aplicativos
title: Mapeando funções de substituição para compatibilidade de aplicativos-ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7cba29b0dda2b0d4533444fd3fa8b83eaaeae7a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461408"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Mapear funções de substituição para compatibilidade com versões anteriores de aplicativos
Um aplicativo ODBC *3. x* funcionando por meio do Gerenciador de driver ODBC *3. x* funcionará em um driver ODBC *2. x* , desde que nenhum novo recurso seja usado. No entanto, a funcionalidade duplicada e as alterações comportamentais afetam a maneira como o aplicativo ODBC *3. x* funciona em um driver ODBC *2. x* . Ao trabalhar com um driver ODBC *2. x* , o Gerenciador de driver mapeia as seguintes funções ODBC *3. x* , que substituíram uma ou mais funções ODBC *2. x* nas funções ODBC *2* . x correspondentes.  
  
|Função ODBC *3. x*|Função ODBC *2. x*|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**ou **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**ou **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] outras ações também podem ser tomadas, dependendo do atributo que está sendo solicitado.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 O Gerenciador de driver mapeia isso para **SQLAllocEnv**, **SQLAllocConnect**ou **SQLAllocStmt**, conforme apropriado. A seguinte chamada para **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 o fará com que o Gerenciador de driver execute o seguinte mapeamento (conceitual, sem verificação de erro):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 O Gerenciador de driver mapeia isso para **SQLSetPos**. A seguinte chamada para **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se o argumento da operação for SQL_ADD, o Gerenciador de driver chamará **SQLSetPos** da seguinte maneira:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Se o argumento da operação não for SQL_ADD, o driver retornará SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  Se o aplicativo tentar alterar o SQL_ATTR_ROW_STATUS_PTR entre chamadas para **SQLFetch** ou **SQLFetchScroll** e **SQLBulkOperations**, o Gerenciador de driver retornará SQLSTATE hy011 (o atributo não pode ser definido agora).  
  
4.  Se o argumento da operação for SQL_ADD, o aplicativo deverá chamar **SQLBindCol** para associar os dados a serem inseridos. Ele não pode chamar **SQLSetDescField** ou **SQLSetDescRec** para associar os dados a serem inseridos.  
  
5.  Se o argumento da operação for SQL_ADD e o número de linhas a serem inseridas não for igual ao tamanho atual do conjunto de linhas, **SQLSetStmtAttr** deverá ser chamado para definir o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem inseridas antes de chamar **SQLBulkOperations**. Para reverter para o tamanho anterior do conjunto de linhas, o aplicativo deve definir o atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE antes de **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos** ser chamado.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 O Gerenciador de driver mapeia isso para **SQLColAttributes**. A seguinte chamada para **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se *FieldIdentifier* for um dos seguintes:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX ou SQL_DESC_LOCAL_TYPE_NAME  
  
     o Gerenciador de driver retorna SQL_ERROR com SQLSTATE HY091 (identificador de campo de descritor inválido). Nenhuma regra adicional desta seção se aplica.  
  
2.  O Gerenciador de driver mapeia SQL_COLUMN_COUNT, SQL_COLUMN_NAME ou SQL_COLUMN_NULLABLE para SQL_DESC_COUNT, SQL_DESC_NAME ou SQL_DESC_NULLABLE, respectivamente. (Um driver ODBC *2. x* precisa apenas de suporte SQL_COLUMN_COUNT, SQL_COLUMN_NAME e SQL_COLUMN_NULLABLE, não SQL_DESC_COUNT, SQL_DESC_NAME e SQL_DESC_NULLABLE.) A chamada para SQLColAttribute é mapeada para:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Todos os outros valores de *FieldIdentifier* são passados para o driver, com **SQLColAttribute** mapeado para **SQLColAttributes** , conforme mostrado anteriormente.  
  
4.  Se *BufferLength* for menor que 0, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido). Nenhuma regra adicional desta seção se aplica.  
  
5.  Se *FieldIdentifier* for SQL_DESC_CONCISE_TYPE e o tipo retornado for um tipo de dados DateTime conciso, o Gerenciador de driver mapeará os valores retornados para os códigos de data, hora e timestamp.  
  
6.  O Gerenciador de driver executa as verificações necessárias para ver se o SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Nesse caso, o Gerenciador de driver retorna SQL_ERROR e SQLSTATE HY010 (erro de sequência de função). Nenhuma regra adicional desta seção se aplica.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 O Gerenciador de driver mapeia isso para **SQLTransact**. A seguinte chamada para **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 o fará com que o Gerenciador de driver execute o seguinte mapeamento (conceitual, sem verificação de erro):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 O Gerenciador de driver mapeia isso para **SQLExtendedFetch** com um argumento *FetchOrientation* de SQL_FETCH_NEXT. A seguinte chamada para **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 o fará com que o Gerenciador de driver chame **SQLExtendedFetch**, da seguinte maneira:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 Nesta chamada, o argumento *pcRow* é definido como o valor que o aplicativo define o atributo SQL_ATTR_ROWS_FETCHED_PTR Statement por meio de uma chamada para **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR para apontar para uma matriz de status, o Gerenciador de driver armazena o ponteiro em cache. *RowStatusArray* pode ser igual a um ponteiro NULL.  
  
 Se o driver não oferecer suporte a **SQLExtendedFetch** e a biblioteca de cursores for carregada, o Gerenciador de driver usará o **SQLExtendedFetch** da biblioteca de cursor para mapear **SQLFetch** para **SQLExtendedFetch**. Se o driver não oferecer suporte a **SQLExtendedFetch** e a biblioteca de cursores não estiver carregada, o Gerenciador de driver passará a chamada para **SQLFetch** até o driver. Se o aplicativo chamar **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver garantirá que a matriz seja populada. Se o aplicativo chamar **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_FETCHED_PTR, o Gerenciador de driver definirá esse campo como 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 O Gerenciador de driver mapeia isso para **SQLExtendedFetch**. A seguinte chamada para **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR (que define o campo SQL_DESC_ARRAY_STATUS_PTR no IRD) para apontar para uma matriz de status, o Gerenciador de driver armazena esse ponteiro em cache. Permitir que esse ponteiro seja *RowStatusArray*; caso contrário, permita que *RowStatusArray* seja igual a um ponteiro nulo. Se o argumento *RowStatusArray* for definido como um ponteiro NULL, o Gerenciador de driver gerará uma matriz de status de linha.  
  
2.  Se *FetchOrientation* não for um dos SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST ou SQL_FETCH_BOOKMARK, o Gerenciador de driver retornará com SQL_ERROR e SQLSTATE HY106 (tipo de busca fora do intervalo). Nenhuma regra adicional desta seção se aplica.  
  
3.  Capitalização:  
  
-   Se *FetchOrientation* for igual a SQL_FETCH_BOOKMARK, então:  
  
    -   Se **SQLSetStmtAttr** foi chamado anteriormente para definir o valor de SQL_ATTR_FETCH_BOOKMARK_PTR, deixe que *BMK* seja o valor obtido ao desreferenciar o ponteiro SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   Caso contrário, retorne SQL_ERROR com SQLSTATE HY111 (valor de indicador inválido). Nenhuma regra adicional desta seção se aplica.  
  
     O Gerenciador de driver agora chama **SQLExtendedFetch**, da seguinte maneira:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   Caso contrário, o Gerenciador de driver chama **SQLExtendedFetch**, da seguinte maneira:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     Nessas chamadas, o argumento *pcRow* é definido como o valor que o aplicativo define o atributo SQL_ATTR_ROWS_FETCHED_PTR Statement por meio de uma chamada para **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE está mapeado para SQL_ROWSET_SIZE.  
  
-   Se o *RC* for igual a SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e, se *FetchOrientation* for igual a SQL_FETCH_BOOKMARK e *FetchOffset* for diferente de 0, o Gerenciador de driver lançará um aviso, SQLSTATE 01S10 (tentativa de buscar por um deslocamento de indicador, valor de deslocamento ignorado) e retornará SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 O Gerenciador de driver mapeia isso para **SQLFreeEnv**, **SQLFreeConnect**ou **SQLFreeStmt** conforme apropriado. A seguinte chamada para **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 o fará com que o Gerenciador de driver execute o seguinte mapeamento (conceitual, sem verificação de erro):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 O Gerenciador de driver mapeia isso para **SQLGetConnectOption**. A seguinte chamada para **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se o *atributo* não for um atributo de instrução ou de conexão definido por driver e não for um atributo definido no ODBC *2. x*, o gerenciador de driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional nesta seção se aplica.  
  
2.  Se o *atributo* for igual a SQL_ATTR_AUTO_IPD ou SQL_ATTR_METADATA_ID, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  O Gerenciador de driver executa as verificações necessárias para ver se SQLSTATE 08003 (conexão não aberta) ou SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Nesse caso, o Gerenciador de driver retorna SQL_ERROR e posta a mensagem de erro apropriada. Nenhuma regra adicional desta seção se aplica.  
  
4.  O Gerenciador de driver chama **SQLGetConnectOption** da seguinte maneira:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Observe que *BufferLength* e *StringLengthPtr* são ignorados.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Quando um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chama **SQLGetData** com o argumento *ColumnNumber* igual a 0, o Gerenciador de driver ODBC *3. x* mapeia isso para uma chamada para **SQLGetStmtOption** com o atributo *Option* definido como SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 O Gerenciador de driver mapeia isso para **SQLGetStmtOption**. A seguinte chamada para **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se o *atributo* não for um atributo de instrução ou de conexão definido por driver e não for um atributo definido no ODBC *2. x*, o gerenciador de driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional nesta seção se aplica.  
  
2.  Se o *atributo* for um dos seguintes:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     o Gerenciador de driver retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional desta seção se aplica.  
  
3.  O Gerenciador de driver executa as verificações necessárias para ver se o SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Nesse caso, o Gerenciador de driver retorna SQL_ERROR e SQLSTATE HY010 (erro de sequência de função). Nenhuma regra adicional desta seção se aplica.  
  
4.  Se *Attribute* for igual a SQL_ATTR_ROWS_FETCHED_PTR, o Gerenciador de driver retornará um ponteiro para a variável interna do Gerenciador de driver de *galinha*, que ele usou ou usará em uma chamada para **SQLExtendedFetch**. Nenhuma regra adicional desta seção se aplica.  
  
5.  Se o *atributo* for igual a SQL_DESC_FETCH_BOOKMARK_PTR, o Gerenciador de driver retornará o ponteiro apropriado que ele tinha armazenado em cache durante uma chamada para **SQLSetStmtAttr**.  
  
6.  Se o *atributo* for igual a SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver retornará o ponteiro apropriado que ele tinha armazenado em cache durante uma chamada para **SQLSetStmtAttr**.  
  
7.  O Gerenciador de driver chama **SQLGetStmtOption** da seguinte maneira:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     em que *HSTMT*, *fOption*e *pvParam* serão definidos como os valores de *StatementHandle*, *Attribute*e *ValuePtr*, respectivamente. *BufferLength* e *StringLengthPtr* são ignorados.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 O Gerenciador de driver mapeia isso para **SQLSetConnectOption**. A seguinte chamada para **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se o *atributo* não for um atributo de instrução ou de conexão definido por driver e não for um atributo definido no ODBC *2. x*, o gerenciador de driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional nesta seção se aplica.  
  
2.  Se o *atributo* for igual a SQL_ATTR_AUTO_IPD, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  O Gerenciador de driver executa as verificações necessárias para ver se o SQLSTATE 08003 (conexão não aberta) ou o SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Se um desses erros precisar ser gerado, o Gerenciador de driver retornará SQL_ERROR e lançará a mensagem de erro apropriada. Nenhuma regra adicional desta seção se aplica.  
  
4.  O Gerenciador de driver chama **SQLSetConnectOption** da seguinte maneira:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     em que *HDBC*, *fOption*e *vParam* serão definidos como os valores de *ConnectionHandle*, *Attribute*e *ValuePtr*, respectivamente. *StringLengthPtr* é ignorado.  
  
> [!NOTE]  
>  A capacidade de definir atributos de instrução no nível de conexão foi preterida. Os atributos de instrução nunca devem ser definidos no nível de conexão por um aplicativo ODBC *3. x* .  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 O Gerenciador de driver mapeia isso para **SQLSetStmtOption**. A seguinte chamada para **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se o *atributo* não for um atributo de instrução ou de conexão definido por driver e não for um atributo definido no ODBC *2. x*, o gerenciador de driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional nesta seção se aplica.  
  
2.  Se o *atributo* for um dos seguintes:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     o Gerenciador de driver retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional desta seção se aplica.  
  
3.  O Gerenciador de driver executa as verificações necessárias para ver se o SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Nesse caso, o Gerenciador de driver retorna SQL_ERROR e SQLSTATE HY010 (erro de sequência de função). Nenhuma regra adicional desta seção se aplica.  
  
4.  Se o *atributo* for igual a SQL_ATTR_PARAMSET_SIZE ou SQL_ATTR_PARAMS_PROCESSED_PTR, consulte a seção "mapeamentos para tratamento de matrizes de parâmetros", mais adiante neste tópico. Nenhuma regra adicional desta seção se aplica.  
  
5.  Se o *atributo* for igual a SQL_ATTR_ROWS_FETCHED_PTR, o Gerenciador de driver armazenará em cache o valor do ponteiro para uso posterior com **SQLFetchScroll**.  
  
6.  Se o *atributo* for igual a SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver armazenará em cache o valor do ponteiro para uso posterior com **SQLFetchScroll** ou **SQLSetPos**. Nenhuma regra adicional desta seção se aplica.  
  
7.  Se o *atributo* for igual a SQL_ATTR_FETCH_BOOKMARK_PTR, o Gerenciador de driver armazenará em cache *ValuePtr* e usará o valor armazenado em cache posteriormente em uma chamada para **SQLFetchScroll**. Nenhuma regra adicional desta seção se aplica.  
  
8.  O Gerenciador de driver chama **SQLSetStmtOption** da seguinte maneira:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     em que *HSTMT*, *fOption*e *vParam* serão definidos como os valores de *StatementHandle*, *Attribute*e *ValuePtr*, respectivamente. O argumento *StringLength* é ignorado.  
  
     Se um driver ODBC *2. x* oferecer suporte a cadeia de caracteres, opções de instrução específicas do driver, um aplicativo ODBC *3. x* deverá chamar **SQLSetStmtOption** para definir essas opções.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Mapeamentos para tratamento de matrizes de parâmetros  
 Quando o aplicativo chama:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 o Gerenciador de driver chama:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 O Gerenciador de driver posteriormente retorna um ponteiro para essa variável quando o aplicativo chama **SQLGetStmtAttr** para recuperar SQL_ATTR_PARAMS_PROCESSED_PTR. O Gerenciador de driver não pode alterar essa variável interna até que o identificador de instrução seja retornado para o estado preparado ou alocado.  
  
 Um aplicativo ODBC *3. x* pode chamar **SQLGetStmtAttr** para obter o valor de SQL_ATTR_PARAMS_PROCESSED_PTR mesmo que não tenha definido explicitamente o campo SQL_DESC_ARRAY_SIZE no APD. Essa situação pode ocorrer, por exemplo, se o aplicativo tiver uma rotina genérica que verifica a "linha" atual dos parâmetros que estão sendo processados quando **SQLExecute** retorna SQL_NEED_DATA. Essa rotina é invocada se a SQL_DESC_ARRAY_SIZE é ou não 1 ou maior que 1. Para considerar isso, o Gerenciador de driver precisará definir essa variável interna, independentemente de o aplicativo ter chamado **SQLSetStmtAttr** para definir o campo SQL_DESC_ARRAY_SIZE em APD. Se SQL_DESC_ARRAY_SIZE não tiver sido definido, o Gerenciador de driver precisará certificar-se de que essa variável contém o valor 1 antes de retornar de **SQLExecDirect** ou **SQLExecute**.  
  
## <a name="error-handling"></a>Tratamento de erros  
 No ODBC *3. x*, chamar **SQLFetch** ou **SQLFETCHSCROLL** popula o SQL_DESC_ARRAY_STATUS_PTR no IRD e o campo SQL_DIAG_ROW_NUMBER de um determinado registro de diagnóstico contém o número da linha no conjunto de linhas ao qual esse registro pertence. Usando isso, o aplicativo pode correlacionar uma mensagem de erro com uma determinada posição de linha.  
  
 Um driver ODBC *2. x* não poderá fornecer essa funcionalidade. No entanto, ele fornecerá a demarcação de erro com SQLSTATE 01S01 (erro na linha). Um aplicativo ODBC *3. x* que está usando **SQLFetch** ou **SQLFetchScroll** ao ir para um driver ODBC *2. x* precisa estar ciente desse fato. Observe também que esse aplicativo não será capaz de chamar **SQLGetDiagField** para realmente obter o campo de SQL_DIAG_ROW_NUMBER de qualquer forma. Um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* poderá chamar **SQLGetDiagField** somente com um argumento *DiagIdentifier* de SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE ou SQL_DIAG_SQLSTATE. O Gerenciador de driver ODBC *3. x* mantém a estrutura de dados de diagnóstico ao trabalhar com um driver ODBC *2. x* , mas o driver ODBC *2. x* retorna apenas esses quatro campos.  
  
 Quando um aplicativo ODBC *2. x* estiver funcionando com um driver ODBC *2. x* , se uma operação puder causar a retorno de vários erros pelo Gerenciador de driver, erros diferentes poderão ser retornados pelo Gerenciador de driver ODBC *3. x* do que pelo Gerenciador de driver ODBC *2. x* .  
  
## <a name="mappings-for-bookmark-operations"></a>Mapeamentos para operações de indicador  
 O Gerenciador de driver ODBC *3. x* executa os seguintes mapeamentos quando um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* executa operações de indicador.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Quando um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chama **SQLBindCol** para associar à coluna 0 com *fCType* igual a SQL_C_VARBOOKMARK, o Gerenciador de driver ODBC *3. x* verifica se o argumento *BufferLength* é menor que 4 ou maior que 4 e, nesse caso, retorna SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido). Se o argumento *BufferLength* for igual a 4, o Gerenciador de driver chamará **SQLBindCol** no driver, depois de substituir *fCType* por SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Quando um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chama **SQLColAttribute** com o argumento *ColumnNumber* definido como 0, o Gerenciador de driver retorna os valores *FieldIdentifier* listados na tabela a seguir.  
  
|*FieldIdentifier*|Valor|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|O mesmo valor retornado por **SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (cadeia de caracteres vazia)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (cadeia de caracteres vazia)|  
|SQL_DESC_LITERAL_SUFFIX|"" (cadeia de caracteres vazia)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Quando um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chama **SQLDescribeCol** com o argumento *ColumnNumber* definido como 0, o Gerenciador de driver retorna os valores listados na tabela a seguir.  
  
|Buffer|Valor|  
|------------|-----------|  
|ColumnName|"" (cadeia de caracteres vazia)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Quando um aplicativo ODBC *3. x* trabalhando com um driver ODBC *2. x* faz a seguinte chamada para **SQLGetData** para recuperar um indicador:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 a chamada é mapeada para **SQLGetStmtOption** com um *fOption* de SQL_GET_BOOKMARK, da seguinte maneira:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 em que *HSTMT* e *pvParam* são definidos como os valores em *StatementHandle* e *TargetValuePtr*, respectivamente. O indicador é retornado no buffer apontado pelo argumento *pvParam* (*TargetValuePtr*). O valor no buffer apontado pelo argumento *StrLen_or_IndPtr* na chamada para **SQLGetData** é definido como 4.  
  
 Esse mapeamento é necessário para considerar o caso em que **SQLFetch** foi chamado antes da chamada para **SQLGetData** e o driver ODBC *2. x* não dava suporte a **SQLExtendedFetch**. Nesse caso, **SQLFetch** seria passado para o driver ODBC *2. x* , caso em que a recuperação do indicador não é suportada.  
  
 **SQLGetData** não pode ser chamado várias vezes em um driver ODBC *2. x* para recuperar um indicador em partes, de modo que chamar **SQLGetData** com o argumento *BufferLength* definido como um valor menor que 4 e o argumento *ColumnNumber* definido como 0 retornará SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido). No entanto, **SQLGetData** pode ser chamado várias vezes para recuperar o mesmo indicador.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Quando um aplicativo ODBC *3. x* que trabalha com um driver ODBC *2. x* chama **SQLSetStmtAttr** para definir o atributo SQL_ATTR_USE_BOOKMARKS como SQL_UB_VARIABLE, o Gerenciador de driver define o atributo como SQL_UB_ON no driver ODBC *2. x* subjacente.
