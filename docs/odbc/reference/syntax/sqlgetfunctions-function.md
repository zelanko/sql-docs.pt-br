---
title: Função SQLGetFunctions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0a44320072f11a56b735502be3f1776f29cc1c0
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538015"
---
# <a name="sqlgetfunctions-function"></a>Função SQLGetFunctions
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetFunctions** retorna informações sobre se um driver dá suporte a uma função específica do ODBC. Essa função é implementada no Gerenciador de Driver. Ele também pode ser implementado em drivers. Se um driver implementa **SQLGetFunctions**, o Gerenciador de Driver chama a função no driver. Caso contrário, ele executa a função em si.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de Conexão.  
  
 *FunctionId*  
 [Entrada] Um **#define** valor que identifica a função ODBC de interesse; **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**. **SQL_API_ODBC3_ALL_FUNCTIONS** é usado por um ODBC 3 *. x* aplicativo para determinar o suporte do ODBC 3 *. x* e funções anteriores. **SQL_API_ALL_FUNCTIONS** é usado por um ODBC 2 *. x* aplicativo para determinar o suporte do ODBC 2 *. x* e funções anteriores.  
  
 Para obter uma lista dos **#define** valores que identificam as funções ODBC, consulte as tabelas "Comentários".  
  
 *SupportedPtr*  
 [Saída]  Se *FunctionId* identifica uma única função ODBC, *SupportedPtr* aponta para um único SQLUSMALLINT valor SQL_TRUE se a função especificada é compatível com o driver e SQL_FALSE se não for com suporte.  
  
 Se *FunctionId* é SQL_API_ODBC3_ALL_FUNCTIONS, *SupportedPtr* aponta para uma matriz SQLSMALLINT com um número de elementos iguais a SQL_API_ODBC3_ALL_FUNCTIONS_SIZE. Essa matriz é tratado pelo Gerenciador de Driver como um bitmap de 4.000 bits que pode ser usado para determinar se um ODBC 3 *. x* ou função earlier é suportada. A macro SQL_FUNC_EXISTS é chamada para determinar o suporte da função. (Consulte "Comentários".) Um ODBC 3 *. x* aplicativo pode chamar **SQLGetFunctions** com SQL_API_ODBC3_ALL_FUNCTIONS contra um ODBC 3 *. x* ou o ODBC 2 *. x* driver.  
  
 Se *FunctionId* é SQL_API_ALL_FUNCTIONS, *SupportedPtr* aponta para uma matriz SQLUSMALLINT de elementos de 100. A matriz é indexada por **#define** valores usados pela *FunctionId* para identificar cada função ODBC; alguns elementos da matriz são reservadas para uso futuro e não utilizados. Um elemento será SQL_TRUE se ele identifica um ODBC 2 *. x* ou função earlier têm suportada no driver. Ele é SQL_FALSE se identifica uma função ODBC não têm suportada no driver ou não identifica uma função ODBC.  
  
 As matrizes retornadas em **SupportedPtr* usar indexação de base zero.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLGetFunctions** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DBC e uma *manipular* dos *ConnectionHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLGetFunctions** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------|-----|-----------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) **SQLGetFunctions** foi chamado antes **SQLConnect**, **SQLBrowseConnect**, ou **SQLDriverConnect**.<br /><br /> (DM) **SQLBrowseConnect** foi chamado para o *ConnectionHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de **SQLBrowseConnect** retornado SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *ConnectionHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY095|Tipo de função fora do intervalo|(DM) inválido *FunctionId* valor foi especificado.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetFunctions** sempre retorna que **SQLGetFunctions**, **SQLDataSources**, e **SQLDrivers** têm suporte. Isso ocorre porque essas funções são implementadas no Gerenciador de Driver. O Gerenciador de Driver mapeará uma função de ANSI para a função Unicode correspondente, se a função Unicode existe e mapeará uma função de Unicode para a função ANSI correspondente se existir a função ANSI. Para obter informações sobre como os aplicativos usam **SQLGetFunctions**, consulte [níveis de conformidade de Interface](../../../odbc/reference/develop-app/interface-conformance-levels.md).  
  
 A seguir está uma lista de valores válidos para *FunctionId* para as funções que estão em conformidade com o nível de conformidade com padrões ISO 92:  
  
|FunctionId valor|FunctionId valor|  
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
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções em conformidade com o nível de conformidade com padrões Open Group:  
  
|FunctionId valor|FunctionId valor|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções em conformidade com o nível de conformidade com padrões ODBC.  
  
|FunctionId valor|FunctionId valor|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] quando estiver trabalhando com um ODBC 2 *. x* driver, **SQLBulkOperations** serão retornados como tem suporte apenas se as duas seguintes forem verdadeiras: ODBC 2 *. x* oferecesuporteadriver **SQLSetPos**, e o tipo de informação SQL_POS_OPERATIONS retorna o bit SQL_POS_ADD como conjunto.  
  
 A seguir está uma lista de valores válidos para *FunctionId* para funções introduzidas no ODBC 3.8 ou posterior:  
  
|FunctionId valor|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle** serão retornados como tem suporte apenas se o driver dá suporte a ambos **SQLCancel** e **SQLCancelHandle**. Se **SQLCancel** tem suporte, mas **SQLCancelHandle** não for, o aplicativo ainda pode chamar **SQLCancelHandle** em um identificador de instrução, pois ele será mapeado para  **SQLCancel**.  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS Macro  
 O SQL_FUNC_EXISTS (*SupportedPtr*, *FunctionID*) macro é usada para determinar o suporte do ODBC 3 *. x* ou funções anteriores depois **SQLGetFunctions**  foi chamado com um *FunctionId* argumento de SQL_API_ODBC3_ALL_FUNCTIONS. O aplicativo chama SQL_FUNC_EXISTS com o *SupportedPtr* argumento definido como o *SupportedPtr* passado *SQLGetFunctions*e com o  *FunctionID* argumento definido como o **#define** para a função. SQL_FUNC_EXISTS SQL_TRUE se a função é suportada e SQL_FALSE caso contrário, retornará.  
  
> [!NOTE]
>  Ao trabalhar com um ODBC 2 *. x* driver, o ODBC 3 *. x* Gerenciador de Driver retornará SQL_TRUE para **SQLAllocHandle** e **SQLFreeHandle**porque **SQLAllocHandle** é mapeado para **SQLAllocEnv**, **SQLAllocConnect**, ou **SQLAllocStmt**, e porque **SQLFreeHandle** é mapeado para **SQLFreeEnv**, **SQLFreeConnect**, ou **SQLFreeStmt**. **Falha de SQLAllocHandle** ou **SQLFreeHandle** com um *HandleType* argumento do SQL_HANDLE_DESC não for compatível, no entanto, mesmo que SQL_TRUE é retornado para as funções, porque não há nenhum 2 de ODBC *. x* função para mapear para nesse caso.  
  
## <a name="code-example"></a>Exemplo de código  
 Os três exemplos a seguir mostram como um aplicativo usa **SQLGetFunctions** para determinar se um driver suporta **SQLTables**, **SQLColumns**, e  **SQLStatistics**. Se o driver não oferece suporte a essas funções, se o aplicativo desconecta o driver. O primeiro exemplo chama **SQLGetFunctions** uma vez para cada função.  
  
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
  
 No segundo exemplo, um aplicativo de 3.x ODBC chama **SQLGetFunctions** e a passa uma matriz na qual **SQLGetFunctions** retorna informações sobre todos os ODBC 3. x e funções anteriores.  
  
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
  
 O terceiro exemplo é um aplicativo ODBC 2.x chama **SQLGetFunctions** e a passa uma matriz de elementos de 100 no qual **SQLGetFunctions** retorna informações sobre todos os ODBC 2. x e funções anteriores.  
  
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
|Retornando a configuração de um atributo de instrução|[Função SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
