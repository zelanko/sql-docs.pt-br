---
title: Mapeamento de funções de substituição para compatibilidade de aplicativos - ODBC | Microsoft Docs
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
ms.openlocfilehash: b18669fe9b6edbd39859166e382ad18d1b04a99a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301086"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Mapear funções de substituição para compatibilidade com versões anteriores de aplicativos
Um aplicativo ODBC *3.x* que funciona através do ODBC *3.x* Driver Manager funcionará contra um driver ODBC *2.x,* desde que não sejam usados novos recursos. Tanto a funcionalidade duplicada quanto as mudanças comportamentais afetam, no entanto, a forma como o aplicativo ODBC *3.x* funciona em um driver ODBC *2.x.* Ao trabalhar com um driver ODBC *2.x,* o Driver Manager mapeia as seguintes funções ODBC *3.x,* que substituíram uma ou mais funções ODBC *2.x,* nas funções ODBC *2.x* correspondentes.  
  
|Função ODBC *3.x*|Função ODBC *2.x*|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv,** **SQLAllocConnect**ou **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributea**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**Sqlextendedfetch**|  
|**SQLFetchScroll**|**Sqlextendedfetch**|  
|**SQLFreeHandle**|**SQLFreeEnv,** **SQLFreeConnect**ou **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**Opção SQLGetConnect**|  
|**SQLGetDiagRec**|**Sqlerror**|  
|**SQLGetStmtAttr**|**SQLGetStmtOpção**[1]|  
|**SQLSetConnectAttr**|**Sqlsetconnectoption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOpção**[1]|  
  
 [1] Outras ações também podem ser tomadas, dependendo do atributo solicitado.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 O Driver Manager mapeia isso para **SQLAllocEnv,** **SQLAllocConnect**ou **SQLAllocStmt,** conforme apropriado. A seguinte chamada para **SQLAllocHandle:**  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 resultará no driver manager realizando o seguinte mapeamento (conceitual, sem verificação de erros):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 O Gerenciador de driver mapeia isso para **SQLSetPos**. A seguinte chamada para **SQLBulkOperations:**  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 resultará na seguinte seqüência de etapas:  
  
1.  Se o argumento Operação for SQL_ADD, o Gerenciador de drivers chamará **SQLSetPos** da seguinte forma:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Se o argumento Operação não for SQL_ADD, o driver readiarreia O SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  Se o aplicativo tentar alterar a SQL_ATTR_ROW_STATUS_PTR entre chamadas para **SQLFetch** ou **SQLFetchScroll** e **SQLBulkOperations,** o Driver Manager retornará SQLSTATE HY011 (Atributo não pode ser definido agora).  
  
4.  Se o argumento Operação for SQL_ADD, o aplicativo deve ligar para **o SQLBindCol** para vincular os dados a serem inseridos. Ele não pode chamar **SQLSetDescField** ou **SQLSetDescRec** para vincular os dados a serem inseridos.  
  
5.  Se o argumento Operação for SQL_ADD e o número de linhas a serem inseridas não for o mesmo que o tamanho atual do conjunto de linhas, o **SQLSetStmtAttr** deve ser chamado para definir o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE ao número de linhas a serem inseridas antes de chamar **SQLBulkOperations**. Para reverter o tamanho anterior do conjunto de linhas, o aplicativo deve definir o atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE antes **que SQLFetch,** **SQLFetchScroll**ou **SQLSetPos** seja chamado.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 O Gerenciador de driver mapeia isso para **SQLColAttributes**. A seguinte chamada para **SQLColAttribute:**  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 resultará na seguinte seqüência de etapas:  
  
1.  Se *fieldidentifier* é um dos seguintes:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX ou SQL_DESC_LOCAL_TYPE_NAME  
  
     o Driver Manager retorna SQL_ERROR com SQLSTATE HY091 (identificador de campo descritor inválido). Não se aplicam mais regras desta seção.  
  
2.  O Driver Manager mapeia SQL_COLUMN_COUNT, SQL_COLUMN_NAME ou SQL_COLUMN_NULLABLE para SQL_DESC_COUNT, SQL_DESC_NAME ou SQL_DESC_NULLABLE, respectivamente. (Um driver ODBC *2.x* precisa apenas de suporte SQL_COLUMN_COUNT, SQL_COLUMN_NAME e SQL_COLUMN_NULLABLE, não SQL_DESC_COUNT, SQL_DESC_NAME e SQL_DESC_NULLABLE.) A chamada para SQLColAttribute é mapeada para:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Todos os outros valores *do FieldIdentifier* são passados para o driver, com **SQLColAttribute** mapeado para **SQLColAttributes** como mostrado anteriormente.  
  
4.  Se *bufferLength* for menor que 0, o Gerenciador de driver retorna SQL_ERROR com SQLSTATE HY090 (string inválida ou comprimento de buffer). Não se aplicam mais regras desta seção.  
  
5.  Se *o FieldIdentifier* for SQL_DESC_CONCISE_TYPE e o tipo retornado for um tipo de dados de data-hora concisa, o Gerenciador de driver mapeia os valores de retorno para códigos de data, hora e carimbo de hora.  
  
6.  O Driver Manager realiza as verificações necessárias para ver se o SQLSTATE HY010 (erro de seqüência de função) precisa ser levantado. Nesse caso, o Driver Manager retorna SQL_ERROR e SQLSTATE HY010 (erro de seqüência de funções). Não se aplicam mais regras desta seção.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 O Driver Manager mapeia isso para **o SQLTransact**. A seguinte chamada para **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 resultará no driver manager realizando o seguinte mapeamento (conceitual, sem verificação de erros):  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 O Gerenciador de driver mapeia isso para **SQLExtendedFetch** com um argumento *FetchOrientation* de SQL_FETCH_NEXT. A seguinte chamada para **SQLFetch:**  
  
```  
SQLFetch (StatementHandle);  
```  
  
 resultará no Driver Manager chamando **SQLExtendedFetch,** da seguinte forma:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 Nesta chamada, o argumento *pcRow* é definido para o valor ao que o aplicativo define o atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR por meio de uma chamada para **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR para apontar para uma matriz de status, o Gerenciador de driver satisfaz o ponteiro. *RowStatusArray* pode ser igual a um ponteiro nulo.  
  
 Se o driver não suportar **sQLExtendedFetch** e a biblioteca do cursor estiver carregada, o Gerenciador de driver usará o **SQLExtendedFetch** da biblioteca do cursor para mapear **O SQLFetch** para **SQLExtendedFetch**. Se o driver não suportar **sQLExtendedFetch** e a biblioteca do cursor não estiver carregada, o Driver Manager passará a chamada para **SQLFetch** para o driver. Se o aplicativo chamar **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver garante que a matriz está preenchida. Se o aplicativo chamar **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_FETCHED_PTR, o Gerenciador de driver define este campo como 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 O Driver Manager mapeia isso para **SQLExtendedFetch**. A seguinte chamada para **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 resultará na seguinte seqüência de etapas:  
  
1.  Quando o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR (que define o campo de SQL_DESC_ARRAY_STATUS_PTR no IRD) para apontar para um array de status, o Gerenciador de driver armazena esse ponteiro. Deixe este ponteiro ser *RowStatusArray;* caso contrário, deixe *rowStatusArray* ser igual a um ponteiro nulo. Se o argumento *RowStatusArray* estiver definido como um ponteiro nulo, o Gerenciador de driver susta/a.  
  
2.  Se *o FetchOrientation* não for um dos SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST ou SQL_FETCH_BOOKMARK, o Driver Manager retorna com SQL_ERROR e SQLSTATE HY106 (tipo Buscar fora de alcance). Não se aplicam mais regras desta seção.  
  
3.  Capitalização:  
  
-   Se *FetchOrientation* é igual a SQL_FETCH_BOOKMARK, então:  
  
    -   Se **sqlsetstmtAttr** foi chamado anteriormente para definir o valor de SQL_ATTR_FETCH_BOOKMARK_PTR, então deixe *Bmk* ser o valor obtido dereferencndo o ponteiro SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   Caso contrário, o retorno SQL_ERROR com SQLSTATE HY111 (valor inválido do marcador). Não se aplicam mais regras desta seção.  
  
     O Driver Manager agora chama **SQLExtendedFetch,** da seguinte forma:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   Caso contrário, o Driver Manager chama **SQLExtendedFetch,** da seguinte forma:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     Nessas chamadas, o argumento *pcRow* é definido para o valor ao que o aplicativo define o atributo de declaração SQL_ATTR_ROWS_FETCHED_PTR através de uma chamada para **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE está mapeado para SQL_ROWSET_SIZE.  
  
-   Se *rc* é igual a SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, e se *FetchOrientation* é igual a SQL_FETCH_BOOKMARK e *FetchOffset* não é igual a 0, então o Driver Manager posta um aviso, SQLSTATE 01S10 (Tentativa de buscar por um marcador deslocamento, valor de deslocamento ignorado) e retornos SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 O Driver Manager mapeia isso para **SQLFreeEnv,** **SQLFreeConnect**ou **SQLFreeStmt** conforme apropriado. A seguinte chamada para **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 resultará no driver manager realizando o seguinte mapeamento (conceitual, sem verificação de erros):  
  
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
  
 resultará na seguinte seqüência de etapas:  
  
1.  Se *O Atributo* não for um atributo de conexão ou declaração definido pelo driver e não for um atributo definido no ODBC *2.x,* o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Não se aplicam mais regras nesta seção.  
  
2.  Se *o Atributo* for igual a SQL_ATTR_AUTO_IPD ou SQL_ATTR_METADATA_ID, o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  O Driver Manager realiza verificações necessárias para ver se o SQLSTATE 08003 (Conexão não aberta) ou o SQLSTATE HY010 (erro de seqüência de função) precisam ser levantados. Nesse caso, o Gerenciador de driver retorna SQL_ERROR e posta a mensagem de erro apropriada. Não se aplicam mais regras desta seção.  
  
4.  O Driver Manager chama **sQLGetConnectOption** da seguinte forma:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Observe que o *BufferLength* e *o StringLengthLengthPtr* são ignorados.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chama **SQLGetData** com o argumento *ColunaNúmero* igual a 0, o Gerenciador de Driver ODBC *3.x* mapeia isso para uma chamada para **SQLGetStmtOption** com o atributo *Opção* definido para SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 O Gerenciador de driver mapeia isso para **SQLGetStmtOption**. A seguinte chamada para **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 resultará na seguinte seqüência de etapas:  
  
1.  Se *O Atributo* não for um atributo de conexão ou declaração definido pelo driver e não for um atributo definido no ODBC *2.x,* o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Não se aplicam mais regras nesta seção.  
  
2.  Se *Atributo* for um dos seguintes:  
  
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
  
     o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Não se aplicam mais regras desta seção.  
  
3.  O Driver Manager realiza as verificações necessárias para ver se o SQLSTATE HY010 (erro de seqüência de função) precisa ser levantado. Nesse caso, o Driver Manager retorna SQL_ERROR e SQLSTATE HY010 (erro de seqüência de funções). Não se aplicam mais regras desta seção.  
  
4.  Se *o Atributo* for igual a SQL_ATTR_ROWS_FETCHED_PTR, o Driver Manager retorna um ponteiro para o *cRow*variável do Driver Manager interno, que ele usou ou usará em uma chamada para **SQLExtendedFetch**. Não se aplicam mais regras desta seção.  
  
5.  Se *O Atributo* for igual a SQL_DESC_FETCH_BOOKMARK_PTR, o Gerenciador de driver retorna o ponteiro apropriado que ele havia armazenado em cache durante uma chamada para **SQLSetStmtAttr**.  
  
6.  Se *o Atributo* for igual a SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver retorna o ponteiro apropriado que ele havia armazenado em cache durante uma chamada para **SQLSetStmtAttr**.  
  
7.  O Driver Manager chama **sQLGetStmtOption** da seguinte forma:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     onde *hstmt,* *fOption*e *pvParam* serão definidos para os valores de *StatementHandle,* *Attribute*e *ValuePtr,* respectivamente. O *BufferLength* e *o StringLengthLengthPtr* são ignorados.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 O Gerenciador de driver mapeia isso para **SQLSetConnectOption**. A seguinte chamada para **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 resultará na seguinte seqüência de etapas:  
  
1.  Se *O Atributo* não for um atributo de conexão ou declaração definido pelo driver e não for um atributo definido no ODBC *2.x,* o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Não se aplicam mais regras nesta seção.  
  
2.  Se *o Atributo* for igual a SQL_ATTR_AUTO_IPD, o Driver Manager retorna SQL_ERROR com O SQLSTATE HY092 (identificador de atributo/opção inválido).  
  
3.  O Driver Manager realiza as verificações necessárias para ver se o SQLSTATE 08003 (Conexão não aberta) ou o SQLSTATE HY010 (erro de seqüência de função) precisam ser levantados. Se um desses erros precisar ser levantado, o Driver Manager retorna SQL_ERROR e posta a mensagem de erro apropriada. Não se aplicam mais regras desta seção.  
  
4.  O Driver Manager chama **sqlsetconnectoption** da seguinte forma:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     onde *hdbc,* *fOption*e *vParam* serão definidos para os valores de *ConnectionHandle,* *Attribute*e *ValuePtr,* respectivamente. *StringLengthPtr* é ignorado.  
  
> [!NOTE]  
>  A capacidade de definir atributos de declaração no nível de conexão foi depreciada. Os atributos de declaração nunca devem ser definidos no nível de conexão por um aplicativo ODBC *3.x.*  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 O Gerenciador de driver mapeia isso para **SQLSetStmtOption**. A seguinte chamada para **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 resultará na seguinte seqüência de etapas:  
  
1.  Se *O Atributo* não for um atributo de conexão ou declaração definido pelo driver e não for um atributo definido no ODBC *2.x,* o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Não se aplicam mais regras nesta seção.  
  
2.  Se *Atributo* for um dos seguintes:  
  
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
  
     o Driver Manager retorna SQL_ERROR com SQLSTATE HY092 (identificador de atributo/opção inválido). Não se aplicam mais regras desta seção.  
  
3.  O Driver Manager realiza as verificações necessárias para ver se o SQLSTATE HY010 (erro de seqüência de funções) precisa ser levantado. Nesse caso, o Driver Manager retorna SQL_ERROR e SQLSTATE HY010 (erro de seqüência de funções). Não se aplicam mais regras desta seção.  
  
4.  Se *O Atributo* for igual a SQL_ATTR_PARAMSET_SIZE ou SQL_ATTR_PARAMS_PROCESSED_PTR, consulte a seção "Mapeamentos para matrizes de parâmetros de manuseio", mais tarde neste tópico. Não se aplicam mais regras desta seção.  
  
5.  Se *O Atributo* for igual a SQL_ATTR_ROWS_FETCHED_PTR, o Gerenciador de driver armazena o valor do ponteiro para uso posterior com **SQLFetchScroll**.  
  
6.  Se *O Atributo* for igual a SQL_ATTR_ROW_STATUS_PTR, o Gerenciador de driver armazena o valor do ponteiro para uso posterior com **SQLFetchScroll** ou **SQLSetPos**. Não se aplicam mais regras desta seção.  
  
7.  Se *O Atributo* for igual a SQL_ATTR_FETCH_BOOKMARK_PTR, o Gerenciador de driver armazena *caches ValuePtr* e usará o valor armazenado em cache mais tarde em uma chamada para **SQLFetchScroll**. Não se aplicam mais regras desta seção.  
  
8.  O Gerenciador de driver chama **sQLSetStmtOption** da seguinte forma:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     onde *hstmt,* *fOption*e *vParam* serão definidos para os valores de *StatementHandle,* *Attribute*e *ValuePtr,* respectivamente. O argumento *StringLength* é ignorado.  
  
     Se um driver ODBC *2.x* for suporte a opções de instrução específicas de caracteres e driver, um aplicativo ODBC *3.x* deve ligar para **sqlsetstmtOption** para definir essas opções.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Mapeamentos para matrizes de parâmetros de manuseio  
 Quando o aplicativo chama:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 o Driver Manager chama:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 O Gerenciador de driver retorna mais tarde um ponteiro para esta variável quando o aplicativo chama **SQLGetStmtAttr** para recuperar SQL_ATTR_PARAMS_PROCESSED_PTR. O Driver Manager não pode alterar essa variável interna até que a alça da declaração seja devolvida ao estado preparado ou alocado.  
  
 Um aplicativo ODBC *3.x* pode chamar **SQLGetStmtAttr** para obter o valor de SQL_ATTR_PARAMS_PROCESSED_PTR mesmo que não tenha explicitamente definido o SQL_DESC_ARRAY_SIZE campo na APD. Essa situação pode surgir, por exemplo, se o aplicativo tiver uma rotina genérica que verifica a "linha" atual de parâmetros que estão sendo processados quando **o SQLExecute** retorna SQL_NEED_DATA. Essa rotina é invocada se o SQL_DESC_ARRAY_SIZE é ou não 1 ou é maior que 1. Para explicar isso, o Driver Manager precisará definir essa variável interna se o aplicativo chamou ou não **de SQLSetStmtAttr** para definir o campo SQL_DESC_ARRAY_SIZE na APD. Se SQL_DESC_ARRAY_SIZE não tiver sido definido, o Driver Manager deve certificar-se de que essa variável contém o valor 1 antes de retornar do **SQLExecDirect** ou **do SQLExecute**.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Em ODBC *3.x,* chamar **SQLFetch** ou **SQLFetchScroll** preenche o SQL_DESC_ARRAY_STATUS_PTR no IRD, e o campo SQL_DIAG_ROW_NUMBER de um determinado registro de diagnóstico contém o número da linha no conjunto de linhas a que este registro pertence. Usando isso, o aplicativo pode correlacionar uma mensagem de erro com uma posição de linha dada.  
  
 Um driver ODBC *2.x* não será capaz de fornecer essa funcionalidade. No entanto, ele fornecerá demarcação de erros com SQLSTATE 01S01 (Erro em linha). Um aplicativo ODBC *3.x* que está usando **SQLFetch** ou **SQLFetchScroll** enquanto vai contra um driver ODBC *2.x* precisa estar ciente desse fato. Observe também que tal aplicativo não será capaz de chamar **SQLGetDiagField** para realmente obter o SQL_DIAG_ROW_NUMBER campo de qualquer maneira. Um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* poderá ligar para **o SQLGetDiagField** apenas com um argumento *DiagIdentifier* de SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE ou SQL_DIAG_SQLSTATE. O ODBC *3.x* Driver Manager mantém a estrutura de dados de diagnóstico ao trabalhar com um driver ODBC *2.x,* mas o driver ODBC *2.x* retorna apenas esses quatro campos.  
  
 Quando um aplicativo ODBC *2.x* está trabalhando com um driver ODBC *2.x,* se uma operação pode causar vários erros a serem devolvidos pelo Driver Manager, diferentes erros podem ser retornados pelo Gerenciador de Driver ODBC *3.x* do que pelo Gerenciador de Driver oDBC *2.x.*  
  
## <a name="mappings-for-bookmark-operations"></a>Mapeamentos para operações de marcadores  
 O ODBC *3.x* Driver Manager realiza os seguintes mapeamentos quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* realiza operações de marcação de marcadores.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chama **o SQLBindCol** para vincular à coluna 0 com *fCType* igual a SQL_C_VARBOOKMARK, o ODBC *3.x* Driver Manager verifica se o argumento *BufferLength* é menor que 4 ou maior que 4, e se assim for, retorna SQLSTATE HY090 (string inválido ou comprimento de buffer). Se o argumento *BufferLength* for igual a 4, o Driver Manager chamará **SQLBindCol** no driver, depois de substituir *fCType* por SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chama **SQLColAttribute** com o argumento *ColunaNúmero* definido como 0, o Gerenciador de driver retorna os valores *fieldIdentifier* listados na tabela a seguir.  
  
|*FieldIdentifier*|Valor|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (cadeia de caracteres vazia)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|O mesmo valor devolvido por **SQLNumResultCols**|  
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
 Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chama **SQLDescribeCol** com o argumento *ColunaNúmero* definido como 0, o Gerenciador de driver retorna os valores listados na tabela a seguir.  
  
|Buffer|Valor|  
|------------|-----------|  
|ColumnName|"" (cadeia de caracteres vazia)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Quando um aplicativo ODBC *3.x* trabalhando com um driver ODBC *2.x* faz a seguinte chamada para **SQLGetData** para recuperar um marcador:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 a chamada é mapeada para **SQLGetStmtOption** com uma *fOption* de SQL_GET_BOOKMARK, da seguinte forma:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 onde *hstmt* e *pvParam* são definidos para os valores em *StatementHandle* e *TargetValuePtr,* respectivamente. O marcador é devolvido no buffer apontado pelo argumento *pvParam* (*TargetValuePtr).* O valor no buffer apontado pelo *argumento StrLen_or_IndPtr* na chamada para **SQLGetData** é definido como 4.  
  
 Este mapeamento é necessário para explicar o caso em que o **SQLFetch** foi chamado antes da chamada para **SQLGetData** e o driver ODBC *2.x* não **suportava SQLExtendedFetch**. Neste caso, **o SQLFetch** seria passado para o driver ODBC *2.x,* nesse caso a recuperação de marcadores não é suportada.  
  
 **O SQLGetData** não pode ser chamado várias vezes em um driver ODBC *2.x* para recuperar um marcador em partes, portanto, chamando **SQLGetData** com o argumento *BufferLength* definido para um valor menor que 4 e o argumento *ColunaNúmero* definido como 0 retornará SQLSTATE HY090 (string inválido ou comprimento de buffer). **SQLGetData** pode, no entanto, ser chamado várias vezes para recuperar o mesmo marcador.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Quando um aplicativo ODBC *3.x* que trabalha com um driver ODBC *2.x* chama **SQLSetStmtAttr** para definir o atributo SQL_ATTR_USE_BOOKMARKS para SQL_UB_VARIABLE, o Driver Manager define o atributo para SQL_UB_ON no driver ODBC *2.x* subjacente.
