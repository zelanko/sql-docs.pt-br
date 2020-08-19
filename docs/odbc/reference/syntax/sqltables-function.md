---
description: Função SQLTables
title: Função SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1eb095849362914074e2c1e7f02166db2712894
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421040"
---
# <a name="sqltables-function"></a>Função SQLTables
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: abrir grupo  
  
 **Resumo**  
 **SQLTables** retorna a lista de nomes de tabela, catálogo ou esquema e tipos de tabela, armazenados em uma fonte de dados específica. O driver retorna as informações como um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução para resultados recuperados.  
  
 *CatalogName*  
 Entrada Nome do catálogo. O argumento *CatalogName* aceita padrões de pesquisa se o atributo de ambiente SQL_ODBC_VERSION for SQL_OV_ODBC3; Ele não aceitará padrões de pesquisa se SQL_OV_ODBC2 estiver definido. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando um driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") indicará as tabelas que não têm catálogos.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de esquema. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") indicará as tabelas que não têm esquemas.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de tabela.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **TableName*.  
  
 *TableName*  
 Entrada Lista de tipos de tabela para correspondência.  
  
 Observe que o atributo de instrução SQL_ATTR_METADATA_ID não tem nenhum efeito sobre o argumento *TableName* . *TableName* é um argumento de lista de valores, independentemente da configuração de SQL_ATTR_METADATA_ID.  
  
 *NameLength4*  
 Entrada Comprimento em caracteres de **TableName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLTables** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLTables** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e for retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* ou *TableName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando SQLTables foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento era menor que 0, mas diferente de SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o nome do catálogo, o esquema da tabela ou o nome da tabela, e a fonte de dados não oferece suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLTables** lista todas as tabelas no intervalo solicitado. Um usuário pode ou não ter privilégios de seleção para qualquer uma dessas tabelas. Para verificar a acessibilidade, um aplicativo pode:  
  
-   Chame **SQLGetInfo** e verifique o tipo de informação SQL_ACCESSIBLE_TABLES.  
  
-   Chame **SQLTablePrivileges** para verificar os privilégios de cada tabela.  
  
 Caso contrário, o aplicativo deve ser capaz de lidar com uma situação em que o usuário seleciona uma tabela para a qual os privilégios **selecionados** não são concedidos.  
  
 Os argumentos *SchemaName* e *TableName* aceitam padrões de pesquisa. O argumento *CatalogName* aceita padrões de pesquisa se o atributo de ambiente SQL_ODBC_VERSION for SQL_OV_ODBC3; Ele não aceitará padrões de pesquisa se SQL_OV_ODBC2 estiver definido. Se SQL_OV_ODBC3 for definido, um driver ODBC 3 *. x* exigirá que os caracteres curinga no argumento *CatalogName* sejam tratados literalmente. Para obter mais informações sobre padrões de pesquisa válidos, consulte [argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Para dar suporte à enumeração de catálogos, esquemas e tipos de tabela, as semânticas especiais a seguir são definidas para os argumentos *CatalogName*, *schemas*, *TableName*e *TableName* de **SQLTables**:  
  
-   Se *CatalogName* for SQL_ALL_CATALOGS e *SchemaName* e *TableName* forem cadeias de caracteres vazias, o conjunto de resultados conterá uma lista de catálogos válidos para a fonte de dados. (Todas as colunas, exceto a TABLE_CAT coluna contêm valores nulos.)  
  
-   Se *SchemaName* for SQL_ALL_SCHEMAS e *nome_do_catálogo* e *TableName* forem cadeias de caracteres vazias, o conjunto de resultados conterá uma lista de esquemas válidos para a fonte de dados. (Todas as colunas, exceto a TABLE_SCHEM coluna contêm valores nulos.)  
  
-   Se o tipo de *tabela* for SQL_ALL_TABLE_TYPES e *CatalogName*, *schemas*e *TableName* forem cadeias de caracteres vazias, o conjunto de resultados conterá uma lista de tipos de tabela válidos para a fonte de dados. (Todas as colunas, exceto a TABLE_TYPE coluna contêm valores nulos.)  
  
 Se *TableName* não for uma cadeia de caracteres vazia, ele deverá conter uma lista de valores separados por vírgulas para os tipos de interesse; cada valor pode ser colocado entre aspas simples (') ou sem aspas, por exemplo, ' TABLE ', ' VIEW ' ou TABLE, VIEW. Um aplicativo sempre deve especificar o tipo de tabela em letras maiúsculas; o driver deve converter o tipo de tabela para qualquer caso necessário para a fonte de dados. Se a fonte de dados não oferecer suporte a um tipo de tabela especificado, **SQLTables** não retornará nenhum resultado para esse tipo.  
  
 **SQLTables** retorna os resultados como um conjunto de resultados padrão, ordenados por TABLE_TYPE, TABLE_CAT, TABLE_SCHEM e TABLE_NAME. Para obter informações sobre como essas informações podem ser usadas, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar os comprimentos reais das colunas TABLE_CAT, TABLE_SCHEM e TABLE_NAME, um aplicativo pode chamar **SQLGetInfo** com os tipos de informações SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_TABLE_NAME_LEN.  
  
 As colunas a seguir foram renomeadas para ODBC 3 *. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|Coluna ODBC 3 *. x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 5 (comentários) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas de driver, contando a partir do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1,0)|1|Varchar|Nome do catálogo; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1,0)|2|Varchar|Nome do esquema; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|TABLE_NAME (ODBC 1,0)|3|Varchar|Nome da tabela.|  
|TABLE_TYPE (ODBC 1,0)|4|Varchar|Nome do tipo de tabela; um dos seguintes: "tabela", "exibição", "tabela do sistema", "temporário GLOBAL", "temporário LOCAL", "ALIAS", "sinônimo" ou um nome de tipo específico da fonte de dados.<br /><br /> Os significados de "ALIAS" e "sinônimo" são específicos do driver.|  
|COMENTÁRIOS (ODBC 1,0)|5|Varchar|Uma descrição da tabela.|  
  
## <a name="example"></a>Exemplo  
 O código de exemplo a seguir não libera identificadores e conexões. Consulte a função [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) e a [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obter exemplos de código para liberar identificadores e instruções.  
  
```cpp  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Retornando as colunas em uma tabela ou tabelas|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando índices e estatísticas de tabela|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Retornando privilégios para uma tabela ou tabelas|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
