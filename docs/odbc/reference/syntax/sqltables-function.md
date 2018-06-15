---
title: Função SQLTables | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f98db327f8d764c5f4fdd8a862505c23c99e8893
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923571"
---
# <a name="sqltables-function"></a>Função SQLTables
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: Open Group  
  
 **Resumo**  
 **SQLTables** retorna a lista de nomes de tabela, o catálogo ou esquema e os tipos de tabela, armazenados em uma fonte de dados específico. O driver retorna as informações como um conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução para recuperar resultados.  
  
 *CatalogName*  
 [Entrada] Nome do catálogo. O *CatalogName* argumento aceita padrões de pesquisa, se o atributo de ambiente SQL_ODBC_VERSION SQL_OV_ODBC3; ele não aceita padrões de pesquisa se SQL_OV_ODBC2 for definido. Se um driver dá suporte a catálogos para algumas tabelas, mas não para outras pessoas, como quando um driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica as tabelas que não possuem catálogos.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento de valor padrão; ela será tratada literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *schemaName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de esquema. Se um driver dá suporte a esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica as tabelas que não têm esquemas.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de tabela.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso não é significativo. Se for SQL_FALSE, *TableName* é um argumento de valor padrão; ela será tratada literalmente e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *TableType*  
 [Entrada] Lista de tipos de tabela para corresponder.  
  
 Observe que o atributo de instrução SQL_ATTR_METADATA_ID não tem nenhum efeito após a *TableType* argumento. *TableType* é um argumento de lista de valor, independentemente da configuração de SQL_ATTR_METADATA_ID.  
  
 *NameLength4*  
 [Entrada] Comprimento em caracteres de **TableType*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLTables** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLTables** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornada pelo driver se **SQLFetch** ou **SQLFetchScroll** retornou SQL_NO_DATA.<br /><br /> Um cursor foi aberto o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão de instrução desconhecido|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *informação* retorna nomes de catálogo é suportadas.<br /><br /> (DM), o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* ou *TableName* argumento era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando SQLTables foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento era menor do que 0 mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não dá suporte a catálogos.<br /><br /> Foi especificado um esquema e o driver ou fonte de dados não dá suporte a esquemas.<br /><br /> Um padrão de cadeia de caracteres de pesquisa foi especificado para o nome do catálogo, esquema de tabela ou nome de tabela e a fonte de dados não dá suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não oferecer suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada este conjunto de resultado solicitada. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLTables** lista todas as tabelas no intervalo solicitado. Um usuário pode ou não ter privilégios selecionados para qualquer uma dessas tabelas. Para verificar acessibilidade, um aplicativo pode:  
  
-   Chamar **SQLGetInfo** e verifique se o tipo de informação SQL_ACCESSIBLE_TABLES.  
  
-   Chamar **SQLTablePrivileges** para verificar os privilégios para cada tabela.  
  
 Caso contrário, o aplicativo deve ser capaz de lidar com uma situação em que o usuário seleciona uma tabela para a qual **selecione** privilégios não são concedidos.  
  
 O *SchemaName* e *TableName* argumentos aceitam padrões de pesquisa. O *CatalogName* argumento aceita padrões de pesquisa, se o atributo de ambiente SQL_ODBC_VERSION SQL_OV_ODBC3; ele não aceita padrões de pesquisa se SQL_OV_ODBC2 for definido. Se SQL_OV_ODBC3 for definido, um ODBC 3 *. x* driver exigirá caracteres curinga a *CatalogName* argumento ser substituídas para serem tratados literalmente. Para obter mais informações sobre os padrões de pesquisa válidos, consulte [argumentos de valor padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Para dar suporte à enumeração de catálogos, esquemas e tipos de tabela, a seguinte semântica especial é definida para o *CatalogName*, *SchemaName*, *TableName*e  *TableType* argumentos de **SQLTables**:  
  
-   Se *CatalogName* é SQL_ALL_CATALOGS e *SchemaName* e *TableName* são cadeias de caracteres vazias, o conjunto de resultados contém uma lista de catálogos válidos para a fonte de dados. (Todas as colunas exceto a coluna TABLE_CAT contêm valores nulos).  
  
-   Se *SchemaName* é SQL_ALL_SCHEMAS e *CatalogName* e *TableName* são cadeias de caracteres vazias, o conjunto de resultados contém uma lista de esquemas válidas para a fonte de dados. (Todas as colunas exceto a coluna TABLE_SCHEM contêm valores nulos).  
  
-   Se *TableType* é SQL_ALL_TABLE_TYPES e *CatalogName*, *SchemaName*, e *TableName* são cadeias de caracteres vazias, o conjunto de resultados contém uma lista de tipos de tabela válido para a fonte de dados. (Todas as colunas exceto a coluna TABLE_TYPE contêm valores nulos).  
  
 Se *TableType* não é uma cadeia de caracteres vazia, ele deve conter uma lista de valores separados por vírgulas para os tipos de interesse; cada valor podem ser colocados entre aspas simples (') ou sem aspas, por exemplo, 'TABLE', 'Exibir' ou tabela, exibição. Um aplicativo sempre deve especificar o tipo de tabela em maiusculas; o driver deve converter o tipo de tabela em qualquer caso é necessária para a fonte de dados. Se a fonte de dados não oferece suporte a um tipo de tabela especificada, **SQLTables** não retornar nenhum resultado para esse tipo.  
  
 **SQLTables** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_TYPE, TABLE_CAT, TABLE_SCHEM e TABLE_NAME. Para obter informações sobre como essas informações podem ser usadas, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar os comprimentos reais das colunas TABLE_CAT, TABLE_SCHEM e TABLE_NAME, um aplicativo pode chamar **SQLGetInfo** com as informações de SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_TABLE_NAME_LEN tipos.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar pelo número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3 *. x* coluna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 5 (comentários) podem ser definidas pelo driver. Um aplicativo deve acessar colunas específicas do driver contando do final do conjunto em vez de especificar uma posição ordinal explícita de resultados. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo; NULL se não for aplicável à fonte de dados. Se um driver dá suporte a catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não possuem catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema; NULL se não for aplicável à fonte de dados. Se um driver dá suporte a esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|Nome da tabela.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|Nome do tipo de tabela; um dos seguintes: "Tabela", "Exibir", "Tabela do sistema", "Temporário GLOBAL", "LOCAL temporário", "ALIAS", "Sinônimo" ou um nome de tipo específico de fonte de dados.<br /><br /> Os significados de "ALIAS" e "Sinônimo" são específicos do driver.|  
|COMENTÁRIOS (ODBC 1.0)|5|Varchar|Uma descrição da tabela.|  
  
## <a name="example"></a>Exemplo  
 O código de exemplo a seguir não libera identificadores e conexões. Consulte [função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) e [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md) para exemplos de código liberar identificadores e instruções.  
  
```  
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
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Retornando as colunas em uma tabela ou tabelas|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando estatísticas de tabela e índices|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Retornando privilégios para uma tabela ou tabelas|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
