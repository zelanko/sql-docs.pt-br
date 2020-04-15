---
title: Função SQLGetFunctions | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15537b28ff2bae8a4fcd3e7be82426eb53aa83a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285326"
---
# <a name="sqlgetfunctions-function"></a>Função SQLGetFunctions
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLGetFunctions** retorna informações sobre se um driver suporta uma função ODBC específica. Esta função é implementada no Driver Manager; também pode ser implementado em drivers. Se um driver implementar **SQLGetFunctions,** o Driver Manager chamará a função no driver. Caso contrário, ele executa a função em si.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConexãoHandle*  
 [Entrada] Identificador de conexão.  
  
 *Functionid*  
 [Entrada] Um **valor #define** que identifica a função de interesse da ODBC; **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS.** **SQL_API_ODBC3_ALL_FUNCTIONS** é usado por um aplicativo ODBC 3 *.x* para determinar o suporte de ODBC 3 *.x* e funções anteriores. **SQL_API_ALL_FUNCTIONS** é usado por um aplicativo ODBC 2 *.x* para determinar o suporte de ODBC 2 *.x* e funções anteriores.  
  
 Para obter uma lista de **valores #define** que identificam funções ODBC, consulte as tabelas em "Comentários".  
  
 *Ptr suportado*  
 [Saída]  Se *FunctionId* identificar uma única função ODBC, *o SupportedPtr apontará* para um único valor SQLUSMALLINT que é SQL_TRUE se a função especificada for suportada pelo driver e SQL_FALSE se ela não for suportada.  
  
 Se *FunctionId* for SQL_API_ODBC3_ALL_FUNCTIONS, *o SupportedPtr* será com uma matriz SQLSMALLINT com vários elementos iguais aos SQL_API_ODBC3_ALL_FUNCTIONS_SIZE. Esta matriz é tratada pelo Driver Manager como um bitmap de 4.000 bits que pode ser usado para determinar se uma função ODBC 3 *.x* ou anterior é suportada. A macro SQL_FUNC_EXISTS é chamada para determinar o suporte à função. (Veja "Comentários".) Um aplicativo ODBC 3 *.x* pode chamar **SQLGetFunctions** com SQL_API_ODBC3_ALL_FUNCTIONS contra um driver ODBC 3 *.x* ou ODBC 2 *.x.*  
  
 Se *FunctionId* for SQL_API_ALL_FUNCTIONS, *o SupportedPtr* aponte para uma matriz SQLUSMALLINT de 100 elementos. O array é indexado por **valores #define** usados pelo *FunctionId* para identificar cada função ODBC; alguns elementos da matriz não são usados e reservados para uso futuro. Um elemento é SQL_TRUE se ele identificar uma função ODBC 2 *.x* ou anterior suportada pelo driver. É SQL_FALSE se identifica uma função ODBC não suportada pelo driver ou não identifica uma função ODBC.  
  
 As matrizes retornadas em **SupportedPtr* usam indexação baseada em zero.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetFunctions** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *alça* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLGetFunctions** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------|-----|-----------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) **SQLGetFunctions** foi chamado antes **de SQLConnect,** **SQLBrowseConnect**ou **SQLDriverConnect**.<br /><br /> (DM) **O SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes **do SQLBrowseConnect** retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *ConnectionHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY095|Tipo de função fora do alcance|(DM) Um valor *functionId* inválido foi especificado.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetFunctions** sempre retorna que **SQLGetFunctions,** **SQLDataSources**e **SQLDrivers** são suportados. Ele faz isso porque essas funções são implementadas no Driver Manager. O Driver Manager mapeará uma função ANSI para a função Unicode correspondente se a função Unicode existir e mapeará uma função Unicode para a função ANSI correspondente se a função ANSI existir. Para obter informações sobre como os aplicativos usam **SQLGetFunctions,** consulte [Níveis de conformidade de interface](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções que estejam em conformidade com o nível de conformidade das normas ISO 92:  
  
|Valor funcional|Valor funcional|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções em conformidade com o nível de conformidade de padrões do Grupo Aberto:  
  
|Valor funcional|Valor funcional|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções em conformidade com o nível de conformidade de padrões ODBC.  
  
|Valor funcional|Valor funcional|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] Ao trabalhar com um driver ODBC*2.x,* **o SQLBulkOperations** será retornado como suportado apenas se ambos forem verdadeiros: o driver ODBC*2.x* suporta **SQLSetPos**e o tipo de informação SQL_POS_OPERATIONS retorna o SQL_POS_ADD bit como definido.  
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções introduzidas no ODBC 3.8 ou posterior:  
  
|Valor funcional|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** será retornado como suportado apenas se o driver suportar **tanto SQLCancel** quanto **SQLCancelHandle**. Se **o SQLCancel** for suportado, mas **o SQLCancelHandle** não estiver, o aplicativo ainda poderá chamar **sQLCancelHandle** em uma alça de declaração, porque ele será mapeado para **SQLCancel**.  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS Macro  
 A macro*SQL_FUNC_EXISTS(SupportedPtr,* *FunctionID)* é usada para determinar o suporte de funções ODBC 3 *.x* ou anteriores após **o SQLGetFunctions** ter sido chamado com um argumento *FunctionId* de SQL_API_ODBC3_ALL_FUNCTIONS. As chamadas de aplicativo SQL_FUNC_EXISTS com o argumento *SupportedPtr* definido para o *SupportedPtr* aprovado no *SQLGetFunctions,* e com o argumento *FunctionID* definido para o **#define** para a função. SQL_FUNC_EXISTS retorna SQL_TRUE se a função for suportada e SQL_FALSE o contrário.  
  
> [!NOTE]
>  Ao trabalhar com um driver ODBC 2 *.x,* o ODBC 3 *.x* Driver Manager retornará SQL_TRUE para **SQLAllocHandle** e **SQLFreeHandle** porque **o SQLAllocHandle** é mapeado para **SQLAllocEnv,** **SQLAllocConnect,** ou **SQLAllocStmt,** e porque **o SQLFreeHandle** é mapeado para **SQLFreeEnv**, **SQLFreeConnect**, ou **SQLFreeStmt**. **SQLAllocHandle** ou **SQLFreeHandle** com um argumento *HandleType* de SQL_HANDLE_DESC não é suportado, no entanto, embora SQL_TRUE seja devolvido para as funções, porque não há função ODBC 2 *.x* para mapear neste caso.  
  
## <a name="code-example"></a>Exemplo de código  
 Os três exemplos a seguir mostram como um aplicativo usa **SQLGetFunctions** para determinar se um driver suporta **SQLTables,** **SQLColumns**e **SQLStatistics**. Se o driver não suportar essas funções, o aplicativo se desconecta do driver. O primeiro exemplo chama **SQLGetFunctions** uma vez para cada função.  
  
```cpp  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 No segundo exemplo, um aplicativo ODBC 3.x chama **SQLGetFunctions** e passa-lhe um array no qual **o SQLGetFunctions** retorna informações sobre todas as funções ODBC 3.x e anteriores.  
  
```cpp  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 O terceiro exemplo é um aplicativo ODBC 2.x chama **SQLGetFunctions** e passa-lhe um conjunto de 100 elementos nos quais **o SQLGetFunctions** retorna informações sobre todas as funções ODBC 2.x e anteriores.  
  
```cpp  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando a configuração de um atributo de conexão|[Função SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Retornando a configuração de um atributo de declaração|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
