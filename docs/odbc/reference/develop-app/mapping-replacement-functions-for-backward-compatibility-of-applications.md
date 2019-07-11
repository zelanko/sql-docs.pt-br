---
title: Mapeando funções de substituição para compatibilidade de aplicativos - ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 099fd0ff318a77f1f1916395fbd13087ab8ba18b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793316"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Mapear funções de substituição para compatibilidade com versões anteriores de aplicativos
ODBC *3.x* aplicativo funcionando por meio de ODBC *3.x* Gerenciador de Driver funcionará contra um ODBC *2.x* driver, desde que não há novos recursos são usados. Ambos duplicado funcionalidades e alterações de comportamento, no entanto, afetam a maneira como que o ODBC *3.x* aplicativo funciona no ODBC *2.x* driver. Ao trabalhar com ODBC *2.x* driver, o Gerenciador de Driver ODBC a seguir é mapeado *3.x* funções, que substituíram o ODBC de um ou mais *2. x* funções, para o ODBC correspondente *2.x* funções.  
  
|ODBC *3.x* função|ODBC *2.x* função|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**, ou **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**, or **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] outras ações também podem ser executadas, dependendo do atributo que está sendo solicitado.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 O Gerenciador de Driver é mapeado para **SQLAllocEnv**, **SQLAllocConnect**, ou **SQLAllocStmt**, conforme apropriado. A seguinte chamada para **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 resultará no Gerenciador de Driver executando o seguinte (conceituais, nenhuma verificação de erros) mapeamento:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 O Gerenciador de Driver é mapeado para **SQLSetPos**. A seguinte chamada para **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se o argumento de operação for SQL_ADD, o Gerenciador de Driver chamará **SQLSetPos** da seguinte maneira:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Se o argumento de operação não for SQL_ADD, o driver retornará SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  Se o aplicativo tenta alterar o SQL_ATTR_ROW_STATUS_PTR entre as chamadas para **SQLFetch** ou **SQLFetchScroll** e **SQLBulkOperations**, será o Gerenciador de Driver retornar o SQLSTATE HY011 (atributo não pode ser definido agora).  
  
4.  Se o argumento de operação for SQL_ADD, o aplicativo deve chamar **SQLBindCol** para associar os dados a ser inserido. Ele não é possível chamar **SQLSetDescField** ou **SQLSetDescRec** para associar os dados a ser inserido.  
  
5.  Se o argumento de operação é SQL_ADD e o número de linhas a ser inserido não é o mesmo que o tamanho atual do conjunto de linhas, **SQLSetStmtAttr** deve ser chamado para definir o atributo de instrução de SQL_ATTR_ROW_ARRAY_SIZE como o número de linhas a serem inserido antes de chamar **SQLBulkOperations**. Para reverter para o tamanho do conjunto de linhas anterior, o aplicativo deve definir o atributo de instrução antes de SQL_ATTR_ROW_ARRAY_SIZE **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos**é chamado.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 O Gerenciador de Driver é mapeado para **SQLColAttributes**. A seguinte chamada para **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se *FieldIdentifier* é um dos seguintes:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX, or SQL_DESC_LOCAL_TYPE_NAME  
  
     o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY091 (identificador de campo de descritor inválido). Nenhuma regra adicional desta seção se aplicam.  
  
2.  O Gerenciador de Driver mapeia SQL_COLUMN_COUNT, SQL_COLUMN_NAME ou SQL_COLUMN_NULLABLE SQL_DESC_COUNT, SQL_DESC_NAME ou SQL_DESC_NULLABLE, respectivamente. (Um ODBC *2.x* driver precisa dar suporte apenas SQL_COLUMN_COUNT, SQL_COLUMN_NAME e SQL_COLUMN_NULLABLE, não SQL_DESC_COUNT, SQL_DESC_NAME e SQL_DESC_NULLABLE.) A chamada para SQLColAttribute é mapeada para:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Todas as outras *FieldIdentifier* valores são passados para o driver, com **SQLColAttribute** mapeado para **SQLColAttributes** conforme mostrado anteriormente.  
  
4.  Se *BufferLength* é menor que 0, o Gerenciador de Driver de retornará SQL_ERROR com SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres). Nenhuma regra adicional desta seção se aplicam.  
  
5.  Se *FieldIdentifier* é SQL_DESC_CONCISE_TYPE e o tipo retornado é um tipo de dados datetime concisos, os mapas de Gerenciador de Driver, o retorno de valores para códigos de data, hora e carimbo de hora.  
  
6.  O Gerenciador de Driver executa as verificações necessárias para ver se SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Se assim, o Gerenciador de Driver retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função). Nenhuma regra adicional desta seção se aplicam.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 O Gerenciador de Driver é mapeado para **SQLTransact**. A seguinte chamada para **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 resultará no Gerenciador de Driver executando o seguinte (conceituais, nenhuma verificação de erros) mapeamento:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 O Gerenciador de Driver é mapeado para **SQLExtendedFetch** com um *FetchOrientation* argumento de SQL_FETCH_NEXT. A seguinte chamada para **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 resultará no Gerenciador de Driver que chama **SQLExtendedFetch**, da seguinte maneira:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 Nessa chamada, o *pcRow* argumento é definido como o valor que o aplicativo define o atributo de instrução sql_attr_rows_fetched_ptr de modo que a por meio de uma chamada para **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Quando o aplicativo chama **SQLSetStmtAttr** para definir sql_attr_row_status_ptr de modo que aponte para uma matriz de status, o Gerenciador de Driver armazena em cache o ponteiro. *RowStatusArray* pode ser igual a um ponteiro nulo.  
  
 Se o driver não suporta **SQLExtendedFetch** e a biblioteca de cursores é carregada, o Gerenciador de Driver usa a biblioteca de cursores **SQLExtendedFetch** mapear **SQLFetch** para **SQLExtendedFetch**. Se o driver não suporta **SQLExtendedFetch** e não é possível carregar a biblioteca de cursor, o Gerenciador de Driver passará a chamada para **SQLFetch** por meio do driver. Se o aplicativo chamar **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de Driver garante que a matriz é preenchida. Se o aplicativo chamar **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_FETCHED_PTR, o Gerenciador de Driver define esse campo como 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 O Gerenciador de Driver é mapeado para **SQLExtendedFetch**. A seguinte chamada para **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR (que define o campo SQL_DESC_ARRAY_STATUS_PTR do IRD) para apontar para uma matriz de status, o Gerenciador de Driver armazena em cache esse ponteiro. Permitir que esse ponteiro seja *RowStatusArray*; caso contrário, deixe *RowStatusArray* ser igual a um ponteiro nulo. Se o *RowStatusArray* argumento é definido como um ponteiro nulo, o Gerenciador de Driver gera uma matriz de status de linha.  
  
2.  Se *FetchOrientation* não é um dos SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST ou SQL_FETCH_BOOKMARK, o Gerenciador de Driver retornará SQL_ERROR e SQLSTATE HY106 (tipo fora do intervalo de busca). Nenhuma regra adicional desta seção se aplicam.  
  
3.  Caso:  
  
-   Se *FetchOrientation* é igual a SQL_FETCH_BOOKMARK, então:  
  
    -   Se **SQLSetStmtAttr** foi chamado anteriormente para definir o valor de SQL_ATTR_FETCH_BOOKMARK_PTR, e deixe *Bmk* ser o valor obtido pela desreferenciar o ponteiro SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   Caso contrário, retornará SQL_ERROR com SQLSTATE HY111 (valor de indicador inválido). Nenhuma regra adicional desta seção se aplicam.  
  
     Agora chama o Gerenciador de Driver **SQLExtendedFetch**, da seguinte maneira:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   Caso contrário, o Gerenciador de Driver chamará **SQLExtendedFetch**, da seguinte maneira:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     Em que essas chamadas, o *pcRow* argumento é definido como o valor que o aplicativo define o atributo de instrução sql_attr_rows_fetched_ptr de modo que a por meio de uma chamada para **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE é mapeado para SQL_ROWSET_SIZE.  
  
-   Se *rc* é igual a SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e se *FetchOrientation* é igual a SQL_FETCH_BOOKMARK e *FetchOffset* é não igual a 0, em seguida, o Driver Gerenciador posta um aviso, SQLSTATE 01S10 (tentativa de buscar por um deslocamento do indicador, deslocamento valor ignorado) e retornará SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 O Gerenciador de Driver é mapeado para **SQLFreeEnv**, **SQLFreeConnect**, ou **SQLFreeStmt** conforme apropriado. A seguinte chamada para **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 resultará no Gerenciador de Driver executando o seguinte (conceituais, nenhuma verificação de erros) mapeamento:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 O Gerenciador de Driver é mapeado para **SQLGetConnectOption**. A seguinte chamada para **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se *atributo* não é um atributo de conexão ou instrução definido pelo driver e não é um atributo definido no ODBC *2.x*, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (atributo inválido / Identificador de opção). Nenhuma regra adicional nesta seção se aplicam.  
  
2.  Se *atributo* é igual a SQL_ATTR_AUTO_IPD ou SQL_ATTR_METADATA_ID, o Gerenciador de Driver de retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  O Gerenciador de Driver executa as verificações necessárias para ver se o SQLSTATE 08003 (Conexão não está aberta) ou SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Nesse caso, o Gerenciador de Driver retornará SQL_ERROR e posta a mensagem de erro apropriada. Nenhuma regra adicional desta seção se aplicam.  
  
4.  As chamadas de Gerenciador de Driver **SQLGetConnectOption** da seguinte maneira:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Observe que o *BufferLength* e *StringLengthPtr* são ignorados.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama **SQLGetData** com o *ColumnNumber* argumento igual a 0, o ODBC *3.x* Gerenciador de Driver mapeia para uma chamada para **SQLGetStmtOption** com o *opção* atributo definido como SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 O Gerenciador de Driver é mapeado para **SQLGetStmtOption**. A seguinte chamada para **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se *atributo* não é um atributo de conexão ou instrução definido pelo driver e não é um atributo definido no ODBC *2.x*, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (atributo inválido / Identificador de opção). Nenhuma regra adicional nesta seção se aplicam.  
  
2.  Se *atributo* é um dos seguintes:  
  
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
  
     o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional desta seção se aplicam.  
  
3.  O Gerenciador de Driver executa as verificações necessárias para ver se SQLSTATE HY010 (erro de sequência de função) precisa ser gerado. Se assim, o Gerenciador de Driver retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função). Nenhuma regra adicional desta seção se aplicam.  
  
4.  Se *atributo* é igual a SQL_ATTR_ROWS_FETCHED_PTR, a retorna um ponteiro em Gerenciador de Driver à variável interna do Gerenciador de Driver *galinha*, que ele usou ou usará em uma chamada para  **SQLExtendedFetch**. Nenhuma regra adicional desta seção se aplicam.  
  
5.  Se *atributo* é igual para SQL_DESC_FETCH_BOOKMARK_PTR, o Gerenciador de Driver retorna o ponteiro apropriado que ele tivesse armazenado em cache durante uma chamada para **SQLSetStmtAttr**.  
  
6.  Se *atributo* é igual para SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de Driver retorna o ponteiro apropriado que ele tivesse armazenado em cache durante uma chamada para **SQLSetStmtAttr**.  
  
7.  As chamadas de Gerenciador de Driver **SQLGetStmtOption** da seguinte maneira:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     em que *hstmt*, *fOption*, e *pvParam* será definido como os valores de *StatementHandle*, *atributo*, e *ValuePtr*, respectivamente. O *BufferLength* e *StringLengthPtr* são ignorados.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 O Gerenciador de Driver é mapeado para **SQLSetConnectOption**. A seguinte chamada para **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se *atributo* não é um atributo de conexão ou instrução definido pelo driver e não é um atributo definido no ODBC *2.x*, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (atributo inválido / Identificador de opção). Nenhuma regra adicional nesta seção se aplicam.  
  
2.  Se *atributo* é igual a SQL_ATTR_AUTO_IPD, o Gerenciador de Driver de retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  O Gerenciador de Driver executa as verificações necessárias para ver se o SQLSTATE 08003 (Conexão não está aberta) ou SQLSTATE HY010 (erro de sequência de função) precisar ser gerado. Se um desses erros precisa ser gerado, o Gerenciador de Driver retornará SQL_ERROR e posta a mensagem de erro apropriada. Nenhuma regra adicional desta seção se aplicam.  
  
4.  As chamadas de Gerenciador de Driver **SQLSetConnectOption** da seguinte maneira:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     em que *hdbc*, *fOption*, e *vParam* será definido como os valores de *ConnectionHandle*, *atributo*, e *ValuePtr*, respectivamente. *StringLengthPtr* será ignorado.  
  
> [!NOTE]  
>  A capacidade de definir atributos de instrução no nível de conexão foi preterida. Atributos de instrução nunca devem ser definidos no nível de conexão pelo ODBC *3.x* aplicativo.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 O Gerenciador de Driver é mapeado para **SQLSetStmtOption**. A seguinte chamada para **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 resultará na seguinte sequência de etapas:  
  
1.  Se *atributo* não é um atributo de conexão ou instrução definido pelo driver e não é um atributo definido no ODBC *2.x*, o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (atributo inválido / Identificador de opção). Nenhuma regra adicional nesta seção se aplicam.  
  
2.  Se *atributo* é um dos seguintes:  
  
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
  
     o Gerenciador de Driver retornará SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Nenhuma regra adicional desta seção se aplicam.  
  
3.  O Gerenciador de Driver executa as verificações necessárias para ver se SQLSTATE HY010 (erro de sequência de função) precisar ser gerado. Se assim, o Gerenciador de Driver retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função). Nenhuma regra adicional desta seção se aplicam.  
  
4.  Se *atributo* é igual a SQL_ATTR_PARAMSET_SIZE ou SQL_ATTR_PARAMS_PROCESSED_PTR, consulte a seção "Mapeamentos para manipular matrizes de parâmetro," neste tópico. Nenhuma regra adicional desta seção se aplicam.  
  
5.  Se *atributo* é igual a SQL_ATTR_ROWS_FETCHED_PTR, os caches de Gerenciador de Driver de valor para uso posterior com o ponteiro **SQLFetchScroll**.  
  
6.  Se *atributo* é igual a SQL_ATTR_ROW_STATUS_PTR, os caches de Gerenciador de Driver de valor para uso posterior com o ponteiro **SQLFetchScroll** ou **SQLSetPos**. Nenhuma regra adicional desta seção se aplicam.  
  
7.  Se *atributo* é igual a SQL_ATTR_FETCH_BOOKMARK_PTR, os caches de Gerenciador de Driver *ValuePtr* e usará o valor armazenado em cache posteriormente em uma chamada para **SQLFetchScroll**. Nenhuma regra adicional desta seção se aplicam.  
  
8.  As chamadas de Gerenciador de Driver **SQLSetStmtOption** da seguinte maneira:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     em que *hstmt*, *fOption*, e *vParam* será definido como os valores de *StatementHandle*, *atributo*, e *ValuePtr*, respectivamente. O *StringLength* argumento será ignorado.  
  
     Se um ODBC *2.x* driver dá suporte a opções de instrução específicos do driver, de cadeia de caracteres, um ODBC *3.x* aplicativo deve chamar **SQLSetStmtOption** para definir essas opções.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Mapeamentos para manipular matrizes de parâmetros  
 Quando o aplicativo chama:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 chama o Gerenciador de Driver:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 O Gerenciador de Driver posteriormente retorna um ponteiro para essa variável quando o aplicativo chama **SQLGetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR de recuperar. O Gerenciador de Driver não pode alterar essa variável interna até que o identificador de instrução é retornado para o estado preparado ou alocado.  
  
 ODBC *3.x* aplicativo pode chamar **SQLGetStmtAttr** para obter o valor de – sql_attr_params_processed_ptr – mesmo que ele não tiver definido explicitamente o campo SQL_DESC_ARRAY_SIZE no APD. Nessa situação pode surgir, por exemplo, se o aplicativo tem uma rotina genérica que verifica se há "linha" de parâmetros atual que está sendo processado quando **SQLExecute** retornará SQL_NEED_DATA. Essa rotina é invocada se ou não a SQL_DESC_ARRAY_SIZE é 1 ou maior que 1. Para justificar isso, o Gerenciador de Driver será necessário definir essa variável interno se o aplicativo tiver chamou **SQLSetStmtAttr** para definir o campo SQL_DESC_ARRAY_SIZE no APD. Se a SQL_DESC_ARRAY_SIZE não tiver sido definido, o Gerenciador de Driver tem que certificar-se de que essa variável contém o valor 1 antes de retornar da **SQLExecDirect** ou **SQLExecute**.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Em ODBC *3.x*, chamar **SQLFetch** ou **SQLFetchScroll** preenche o SQL_DESC_ARRAY_STATUS_PTR em do IRD e o campo SQL_DIAG_ROW_NUMBER de um determinado diagnóstico Registro contém o número da linha no conjunto de linhas que pertence a este registro a. Usando isso, o aplicativo pode correlacionar uma mensagem de erro com uma posição determinada linha.  
  
 ODBC *2.x* driver não será possível fornecer essa funcionalidade. No entanto, ele fornecerá demarcação de erro com SQLSTATE 01S01 (erro na linha). ODBC *3.x* aplicativo que está usando **SQLFetch** ou **SQLFetchScroll** ao mesmo tempo em que vai contra um ODBC *2.x* driver precisa estar ciente das Esse fato. Observe também que esse aplicativo poderá chamar **SQLGetDiagField** para realmente obter o campo SQL_DIAG_ROW_NUMBER mesmo assim. ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver será capaz de chamar **SQLGetDiagField** apenas com um *DiagIdentifier* argumento de SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE ou SQL_DIAG_SQLSTATE. O ODBC *3.x* Gerenciador de Driver mantém a estrutura de dados de diagnóstico ao trabalhar com ODBC *2.x* driver, mas o ODBC *2.x* driver retornará apenas esses quatro campos.  
  
 Quando um ODBC *2.x* aplicativo está funcionando com um ODBC *2.x* driver, se uma operação pode causar vários erros a serem retornadas pelo Gerenciador de Driver, erros diferentes podem ser retornados pelo ODBC *3.x* o Gerenciador de Driver de ODBC *2.x* Gerenciador de Driver.  
  
## <a name="mappings-for-bookmark-operations"></a>Mapeamentos para operações de indicador  
 O ODBC *3.x* Gerenciador de Driver executa os seguintes mapeamentos quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver executa operações de indicador.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama **SQLBindCol** associar a coluna 0 com *fCType* igual a SQL_C_ VARBOOKMARK, o ODBC *3.x* Gerenciador de Driver verifica para ver se o *BufferLength* argumento é menor que 4 ou maior que 4 e, nesse caso, retornará SQLSTATE HY090 (cadeia de caracteres inválida ou buffer comprimento). Se o *BufferLength* argumento é igual a 4, chama o Gerenciador de Driver **SQLBindCol** no driver, depois de substituir *fCType* com SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama **SQLColAttribute** com o *ColumnNumber* argumento definido como 0, o Gerenciador de Driver retorna o *FieldIdentifier* valores listados na tabela a seguir.  
  
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
 Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama **SQLDescribeCol** com o *ColumnNumber* argumento definido como 0, o Gerenciador de Driver retorna os valores listados na tabela a seguir.  
  
|Buffer|Valor|  
|------------|-----------|  
|ColumnName|"" (cadeia de caracteres vazia)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver faz a chamada a seguir para **SQLGetData** para recuperar um indicador:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 a chamada é mapeada para **SQLGetStmtOption** com um *fOption* de SQL_GET_BOOKMARK, da seguinte maneira:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 em que *hstmt* e *pvParam* são definidos como os valores na *StatementHandle* e *TargetValuePtr*, respectivamente. O indicador é retornado no buffer apontado pela *pvParam* (*TargetValuePtr*) argumento. O valor no buffer apontado pela *StrLen_or_IndPtr* argumento na chamada para **SQLGetData** é definido como 4.  
  
 Esse mapeamento é necessário levar em conta o caso em que **SQLFetch** foi chamado antes da chamada a **SQLGetData** e o ODBC *2.x* driver não oferecia suporte **SQLExtendedFetch**. Nesse caso, **SQLFetch** deve ser passado para o ODBC *2.x* driver, no qual indicador caso não há suporte recuperação.  
  
 **SQLGetData** não pode ser chamado várias vezes em um ODBC *2.x* driver para recuperar um indicador em partes, por isso a chamada **SQLGetData** com o *BufferLength* argumento definido como um valor menor que 4 e o *ColumnNumber* argumento definido como 0 retornará SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres). **SQLGetData** pode, no entanto, ser chamado várias vezes para recuperar o mesmo indicador.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Quando um ODBC *3.x* aplicativo trabalhar com ODBC *2.x* driver chama **SQLSetStmtAttr** para definir o SQL_ATTR_USE_BOOKMARKS atributo SQL_UB_VARIABLE, o Driver Manager define o atributo como SQL_UB_ON no ODBC subjacente *2.x* driver.
