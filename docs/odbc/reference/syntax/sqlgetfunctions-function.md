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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: edb58ebff212e494b84aed12397def2876d3728d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68345606"
---
# <a name="sqlgetfunctions-function"></a>Função SQLGetFunctions
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLGetFunctions** retorna informações sobre se um driver dá suporte a uma função ODBC específica. Essa função é implementada no Gerenciador de driver; Ele também pode ser implementado em drivers. Se um driver implementar **SQLGetFunctions**, o Gerenciador de driver chamará a função no driver. Caso contrário, ele executa a própria função.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexão.  
  
 *FunctionId*  
 Entrada Um valor **#define** que identifica a função de ODBC de interesse; **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**. **SQL_API_ODBC3_ALL_FUNCTIONS** é usado por um aplicativo ODBC 3 *. x* para determinar o suporte ao ODBC 3 *. x* e às funções anteriores. **SQL_API_ALL_FUNCTIONS** é usado por um aplicativo ODBC 2 *. x* para determinar o suporte do ODBC 2 *. x* e das funções anteriores.  
  
 Para obter uma lista de valores de **#define** que identificam funções ODBC, consulte as tabelas em "Comentários".  
  
 *SupportedPtr*  
 Der  Se *FunctionID* identificar uma única função ODBC, *SupportedPtr* apontará para um único valor de SQLUSMALLINT SQL_TRUE se a função especificada for suportada pelo driver e SQL_FALSE se não houver suporte.  
  
 Se *FunctionID* for SQL_API_ODBC3_ALL_FUNCTIONS, *SupportedPtr* apontará para uma matriz SQLSMALLINT com um número de elementos igual a SQL_API_ODBC3_ALL_FUNCTIONS_SIZE. Essa matriz é tratada pelo Gerenciador de driver como um bitmap de 4.000 bits que pode ser usado para determinar se há suporte para uma função ODBC 3 *. x* ou anterior. A macro SQL_FUNC_EXISTS é chamada para determinar o suporte de função. (Consulte "Comentários".) Um aplicativo ODBC 3 *. x* pode chamar **SQLGetFunctions** com SQL_API_ODBC3_ALL_FUNCTIONS em relação a um driver ODBC 3 *. x* ou ODBC 2 *. x* .  
  
 Se *FunctionID* for SQL_API_ALL_FUNCTIONS, *SupportedPtr* apontará para uma matriz SQLUSMALLINT de elementos 100. A matriz é indexada por **#define** valores usados por *FunctionID* para identificar cada função ODBC; alguns elementos da matriz são não utilizados e reservados para uso futuro. Um elemento é SQL_TRUE se ele identificar uma função ODBC 2 *. x* ou anterior com suporte pelo driver. É SQL_FALSE se ele identifica uma função ODBC sem suporte do driver ou não identifica uma função ODBC.  
  
 As matrizes retornadas em **SupportedPtr* usam a indexação baseada em zero.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLGetFunctions** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e um *identificador* de *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetFunctions** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------|-----|-----------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLGetFunctions** foi chamado antes de **SQLConnect**, **SQLBrowseConnect**ou **SQLDriverConnect**.<br /><br /> (DM) **SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornou SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornar SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *ConnectionHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY095|Tipo de função fora do intervalo|(DM) um valor *FunctionID* inválido foi especificado.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetFunctions** sempre retorna que **SQLGetFunctions**, **SQLDataSources**e **SQLDrivers** têm suporte. Ele faz isso porque essas funções são implementadas no Gerenciador de driver. O Gerenciador de driver mapeará uma função ANSI para a função Unicode correspondente se a função Unicode existir e mapeará uma função Unicode para a função ANSI correspondente, se a função ANSI existir. Para obter informações sobre como os aplicativos usam o **SQLGetFunctions**, consulte [níveis de conformidade da interface](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 A seguir está uma lista de valores válidos para *FunctionID* para funções que estão em conformidade com o nível de conformidade de padrões ISO 92:  
  
|Valor de FunctionID|Valor de FunctionID|  
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
  
 A seguir está uma lista de valores válidos para *FunctionID* para funções que estão de acordo com o nível de conformidade de padrões do grupo aberto:  
  
|Valor de FunctionID|Valor de FunctionID|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 A seguir está uma lista de valores válidos para *FunctionID* para funções que estão de acordo com o nível de conformidade de padrões ODBC.  
  
|Valor de FunctionID|Valor de FunctionID|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS [1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] ao trabalhar com um driver ODBC 2 *. x* , **SQLBulkOperations** será retornado como com suporte somente se ambos os itens a seguir forem verdadeiros: o driver ODBC 2 *. x* oferece suporte a **SQLSetPos**e o tipo de informação SQL_POS_OPERATIONS retorna o bit SQL_POS_ADD como definido.  
  
 A seguir está uma lista de valores válidos para *FunctionID* para funções introduzidas no ODBC 3,8 ou posterior:  
  
|Valor de FunctionID|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** será retornado como com suporte apenas se o driver der suporte a **SQLCancel** e **SQLCancelHandle**. Se **SQLCancel** for suportado, mas **SQLCancelHandle** não for, o aplicativo ainda poderá chamar **SQLCancelHandle** em um identificador de instrução, pois ele será mapeado para **SQLCancel**.  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS macro  
 A macro SQL_FUNC_EXISTS (*SupportedPtr*, *FunctionID*) é usada para determinar o suporte de funções ODBC 3 *. x* ou anteriores após **SQLGetFunctions** ter sido chamado com um argumento *FunctionID* de SQL_API_ODBC3_ALL_FUNCTIONS. O aplicativo chama SQL_FUNC_EXISTS com o argumento *SupportedPtr* definido como o *SupportedPtr* passado em *SQLGetFunctions*e com o argumento *FunctionID* definido como o **#define** para a função. SQL_FUNC_EXISTS retornará SQL_TRUE se a função tiver suporte e SQL_FALSE caso contrário.  
  
> [!NOTE]
>  Ao trabalhar com um driver ODBC 2 *. x* , o Gerenciador de driver ODBC 3 *. x* retornará SQL_TRUE para **SQLAllocHandle** e **SQLFreeHandle** , pois **SQLAllocHandle** é mapeado para **SQLAllocEnv**, **SQLAllocConnect**ou **SQLAllocStmt**, e como **SQLFreeHandle** é mapeado para **SQLFreeEnv**, **SQLFreeConnect**ou **SQLFreeStmt**. **SQLAllocHandle** ou **SQLFreeHandle** com um argumento *HandleType* de SQL_HANDLE_DESC não tem suporte, no entanto, embora SQL_TRUE seja retornada para as funções, porque não há nenhuma função ODBC 2 *. x* para a qual mapear nesse caso.  
  
## <a name="code-example"></a>Exemplo de código  
 Os três exemplos a seguir mostram como um aplicativo usa **SQLGetFunctions** para determinar se um driver dá suporte a **SQLTables**, **SQLColumns**e **SQLStatistics**. Se o driver não oferecer suporte a essas funções, o aplicativo se desconectará do driver. O primeiro exemplo chama **SQLGetFunctions** uma vez para cada função.  
  
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
  
 No segundo exemplo, um aplicativo ODBC 3. x chama **SQLGetFunctions** e passa a ele uma matriz na qual **SQLGetFunctions** retorna informações sobre todas as funções ODBC 3. x e anteriores.  
  
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
  
 O terceiro exemplo é um aplicativo ODBC 2. x que chama **SQLGetFunctions** e passa a ele uma matriz de 100 elementos em que **SQLGetFunctions** retorna informações sobre todas as funções ODBC 2. x e anteriores.  
  
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
|Retornando informações sobre um driver ou uma fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
