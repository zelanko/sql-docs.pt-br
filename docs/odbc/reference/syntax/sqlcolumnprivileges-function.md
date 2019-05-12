---
title: Função SQLColumnPrivileges | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10d05310f7d9580b652f24bffa0896e32b23a40a
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537706"
---
# <a name="sqlcolumnprivileges-function"></a>Função SQLColumnPrivileges
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLColumnPrivileges** retorna uma lista de colunas e os privilégios associados para a tabela especificada. O driver retorna as informações como um conjunto de resultados em especificado *StatementHandle*.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *CatalogName*  
 [Entrada] Nome do catálogo. Se um driver compatível com nomes para alguns catálogos, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") denota desses catálogos que não têm nomes. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Nome do esquema. Se um driver compatível com esquemas para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não tem esquemas. *SchemaName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador. Se for SQL_FALSE, *SchemaName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Nome da tabela. Esse argumento não pode ser um ponteiro nulo. *TableName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *TableName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *TableName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **TableName*.  
  
 *ColumnName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de coluna.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ColumnName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *ColumnName* é um argumento de valor padrão; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength4*  
 [Entrada] Comprimento em caracteres de **ColumnName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLColumnPrivileges** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* sql_handle_stmt e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLColumnPrivileges** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Driver Gerenciador. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto sobre o *StatementHandle,* e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O *TableName* argumento é um ponteiro nulo.<br /><br /> O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *tipo de informação* retorna nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* ou *ColumnName* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento do nome da era menor que 0 mas não iguais a SQL_NTS.|  
|||O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome correspondente. (Consulte "Comentários".)|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Foi especificado um nome de catálogo, e o driver ou fonte de dados não oferece suporte a catálogos.<br /><br /> Foi especificado um nome de esquema e o driver ou fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o nome da coluna, e a fonte de dados não oferece suporte a padrões de pesquisa para o argumento.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_CONCURRENCY e SQL_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLColumnPrivileges** retorna os resultados como um conjunto de resultados padrão, ordenado por TABLE_CAT, por TABLE_SCHEM, TABLE_NAME, COLUMN_NAME e privilégios.  
  
> [!NOTE]  
>  **SQLColumnPrivileges** podem não retornar privilégios para todas as colunas. Por exemplo, um driver pode não retornar informações sobre privilégios para pseudo colunas, como Oracle ROWID. Os aplicativos podem usar qualquer coluna válida, independentemente se ele é retornado por **SQLColumnPrivileges**.  
  
 Os comprimentos das colunas VARCHAR não são mostrados na tabela; os comprimentos reais dependem da fonte de dados. Para determinar os comprimentos reais das colunas CATALOG_NAME, SCHEMA_NAME, TABLE_NAME e nome da coluna, um aplicativo pode chamar **SQLGetInfo** com o SQL_MAX_TABLE_NAME_ SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, LEN e SQL_MAX_COLUMN_NAME_LEN opções.  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 As seguintes colunas foram renomeadas para ODBC 3. *x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar por número de coluna.  
  
|Coluna de ODBC 2.0|ODBC 3. *x* coluna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (IS_GRANTABLE) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Identificador do catálogo; NULL se não for aplicável à fonte de dados. Se um driver compatível com catálogos para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não têm catálogos.|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|Identificador do esquema; NULL se não for aplicável à fonte de dados. Se um driver compatível com esquemas para algumas tabelas, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para as tabelas que não tem esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar não nulo|Identificador de tabela.|  
|COLUMN_NAME (ODBC 1.0)|4|Varchar não nulo|Nome da coluna. O driver retornará uma cadeia de caracteres vazia para uma coluna que não tem um nome.|  
|CONCESSOR (ODBC 1.0)|5|Varchar|Nome do usuário que recebe o privilégio; NULL se não for aplicável à fonte de dados.<br /><br /> Para todas as linhas em que o valor na coluna usuário autorizado é o proprietário do objeto, a coluna GRANTOR será sistema".|  
|USUÁRIO AUTORIZADO (ODBC 1.0)|6|Varchar não nulo|Nome do usuário a quem o privilégio foi concedido.|  
|PRIVILÉGIO DE (ODBC 1.0)|7|Varchar não nulo|Identifica o privilégio de coluna. Pode ser um dos seguintes (ou outras suportadas pelos dados de origem definido pela implementação):<br /><br /> SELECIONE: O usuário autorizado tem permissão para recuperar dados da coluna.<br /><br /> INSERIR: O usuário autorizado tem permissão para fornecer dados para a coluna nas novas linhas são inseridas na tabela associada.<br /><br /> ATUALIZAÇÃO: O usuário autorizado tem permissão para atualizar os dados na coluna.<br /><br /> REFERÊNCIAS: O usuário autorizado tem permissão para fazer referência à coluna dentro de uma restrição (por exemplo, um único, referencial, ou restrição de verificação de tabela).|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|Indica se o usuário autorizado tem permissão para conceder o privilégio para outros usuários. "Sim", "Não" ou "Nulo" se desconhecido ou não aplicável à fonte de dados.<br /><br /> Um privilégio é que podem ser concedidas ou que não podem ser concedidas, mas não ambos. O conjunto de resultados retornado por **SQLColumnPrivileges** nunca conterá duas linhas para o qual todas as colunas, exceto a coluna IS_GRANTABLE contêm o mesmo valor.|  
  
## <a name="code-example"></a>Exemplo de código  
 Para obter um exemplo de código de uma função semelhante, consulte [função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando as colunas em uma tabela ou tabelas|[Função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscar várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando os privilégios para uma tabela ou tabelas|[Função SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|Retornando uma lista de tabelas em uma fonte de dados|[Função SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
