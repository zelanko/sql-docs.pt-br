---
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
ms.openlocfilehash: ae52e6431679ed0f260e6885090ac38363b4ef3d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287126"
---
# <a name="sqltables-function"></a>Função SQLTables
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: Open Group  
  
 **Resumo**  
 **O SQLTables** retorna a lista de nomes de tabela, catálogo ou esquema, e tipos de tabela, armazenados em uma fonte de dados específica. O motorista retorna as informações como um conjunto de resultados.  
  
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
 [Entrada] Alça de declaração para resultados recuperados.  
  
 *Catalogname*  
 [Entrada] Nome do catálogo. O *argumento CatalogName* aceita padrões de pesquisa se o atributo de ambiente SQL_ODBC_VERSION estiver SQL_OV_ODBC3; ele não aceita padrões de pesquisa se SQL_OV_ODBC2 for definido. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando um driver recupera dados de diferentes DBMSs, uma string vazia ("") indica as tabelas que não possuem catálogos.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Padrão de busca de cordas para nomes de esquemas. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") indica aquelas tabelas que não possuem esquemas.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Tablename*  
 [Entrada] Padrão de pesquisa de cordas para nomes de tabela.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID estiver definido como SQL_TRUE, *O Nome da Tabela* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *TableName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *TableType*  
 [Entrada] Lista de tipos de tabela saem para combinar.  
  
 Observe que o atributo de declaração SQL_ATTR_METADATA_ID não tem efeito sobre o argumento *TableType.* *TableType* é um argumento de lista de valores, independentemente da configuração de SQL_ATTR_METADATA_ID.  
  
 *Comprimento de nome4*  
 [Entrada] Comprimento em caracteres de **TableType*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLTables** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLTables** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida por causa de um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* ou *TableName* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando o SQLTables foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento foi inferior a 0, mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o nome correspondente.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um esquema foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> Um padrão de pesquisa de strings foi especificado para o nome do catálogo, esquema de tabela ou nome da tabela, e a fonte de dados não suporta padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLTables** lista todas as tabelas no intervalo solicitado. Um usuário pode ou não ter privilégios SELECT para qualquer uma dessas tabelas. Para verificar a acessibilidade, um aplicativo pode:  
  
-   Ligue para **o SQLGetInfo** e verifique o tipo de informação SQL_ACCESSIBLE_TABLES.  
  
-   Ligue para **o SQLTablePrivileges** para verificar os privilégios de cada tabela.  
  
 Caso contrário, o aplicativo deve ser capaz de lidar com uma situação em que o usuário seleciona uma tabela para a qual **privilégios SELECT** não são concedidos.  
  
 Os argumentos *SchemaName* e *TableName* aceitam padrões de pesquisa. O *argumento CatalogName* aceita padrões de pesquisa se o atributo de ambiente SQL_ODBC_VERSION estiver SQL_OV_ODBC3; ele não aceita padrões de pesquisa se SQL_OV_ODBC2 for definido. Se SQL_OV_ODBC3 estiver definido, um driver ODBC 3 *.x* exigirá que os caracteres curingas no argumento *CatalogName* sejam escapados para serem tratados literalmente. Para obter mais informações sobre padrões de pesquisa [válidos,](../../../odbc/reference/develop-app/pattern-value-arguments.md)consulte Argumentos de valor de padrão .  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Para suportar a enumeração de catálogos, esquemas e tipos de tabela, as seguintes semânticas especiais são definidas para os argumentos *CatalogName*, *SchemaName,* *TableName*e *TableType* de **SQLTables**:  
  
-   Se *CatalogName* for SQL_ALL_CATALOGS e *SchemaName* e *TableName* estiverem em cadeias de seqüências vazias, o conjunto de resultados contém uma lista de catálogos válidos para a fonte de dados. (Todas as colunas, exceto a coluna TABLE_CAT contêm NULLs.)  
  
-   Se *SchemaName* for SQL_ALL_SCHEMAS e *CatalogName* e *TableName* estiverem em strings vazias, o conjunto de resultados contém uma lista de esquemas válidos para a fonte de dados. (Todas as colunas, exceto a coluna TABLE_SCHEM contêm NULLs.)  
  
-   Se *TableType* for SQL_ALL_TABLE_TYPES e *CatalogName,* *SchemaName*e *TableName* forem strings vazios, o conjunto de resultados contém uma lista de tipos de tabela válidos para a fonte de dados. (Todas as colunas, exceto a coluna TABLE_TYPE contêm NULLs.)  
  
 Se *TableType* não for uma seqüência de string vazia, ele deve conter uma lista de valores separados por comuma para os tipos de interesse; cada valor pode ser incluído entre aspas simples (') ou não, por exemplo, 'TABELA', 'VIEW' ou TABELA, VIEW. Um aplicativo deve sempre especificar o tipo de tabela em maiúsculas; o driver deve converter o tipo de tabela para qualquer caso necessário pela fonte de dados. Se a fonte de dados não suportar um tipo de tabela especificado, **o SQLTables** não retornará nenhum resultado para esse tipo.  
  
 **O SQLTables** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_TYPE, TABLE_CAT, TABLE_SCHEM e TABLE_NAME. Para obter informações sobre como essas informações podem ser usadas, consulte [Usos de Dados de Catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Para determinar os comprimentos reais das colunas de TABLE_CAT, TABLE_SCHEM e TABLE_NAME, um aplicativo pode ligar para **o SQLGetInfo** com os tipos de informações SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_TABLE_NAME_LEN.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *.x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|Coluna ODBC 3 *.x*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 5 (OBSERVAÇÕES) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nome do catálogo; NULL se não aplicável à fonte de dados. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nome do esquema; NULL se não aplicável à fonte de dados. Se um driver suporta esquemas para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aquelas tabelas que não possuem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|Nome da tabela.|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|Nome do tipo de tabela; um dos seguintes: "TABLE", "VIEW", "SYSTEM TABLE", "GLOBAL TEMPORARY", "LOCAL TEMPORARY", "ALIAS", "SYNONYM" ou um nome de tipo específico de origem de dados.<br /><br /> Os significados de "ALIAS" e "SYNONYM" são específicos do driver.|  
|OBSERVAÇÕES (ODBC 1.0)|5|Varchar|Uma descrição da tabela.|  
  
## <a name="example"></a>Exemplo  
 O código de amostra a seguir não libera alças e conexões. Consulte [SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md) e [SQLFreeStmt Function](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obter amostras de código para obter alças e instruções gratuitas.  
  
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
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolvendo privilégios para uma coluna ou colunas|[Função SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Retornando as colunas em uma tabela ou tabela|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Estatísticas e índices da tabela de retorno|[Função SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Devolvendo privilégios para uma tabela ou tabela|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
