---
title: Função SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96299b8b3fb7a4e22bfc3500b82429720b493462
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686634"
---
# <a name="sqlprocedures-function"></a>Função SQLProcedures
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: ODBC  
  
 **Resumo**  
 **SQLProcedures** retorna a lista de nomes de procedimentos armazenados em uma fonte de dados específico. *Procedimento* é um termo genérico usado para descrever uma *objeto executável*, ou uma entidade nomeada que pode ser invocada usando parâmetros de entrada e saída. Para obter mais informações sobre procedimentos, consulte a [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *CatalogName*  
 [Entrada] Catálogo de procedimento. Se um driver compatível com catálogos para algumas tabelas, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; ela será tratada, literalmente, e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de esquema de procedimento. Se um driver compatível com esquemas para alguns procedimentos, mas não para outros, como quando o driver recupera os dados de diferentes DBMSs, uma cadeia de caracteres vazia ("") indica que esses procedimentos que não têm esquemas.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *ProcName*  
 [Entrada] Padrão de pesquisa de cadeia de caracteres para nomes de procedimento.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ProcName* é tratado como um identificador e o seu caso de não é significativo. Se for SQL_FALSE, *ProcName* é um argumento de valor padrão; ela será tratada, literalmente, e seu caso é significativo.  
  
 *NameLength3*  
 [Entrada] Comprimento em caracteres de **ProcName*.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLProcedures** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLProcedures** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|24000|Estado de cursor inválido|Um cursor foi aberto sobre o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada. Esse erro é retornado pelo Gerenciador de Driver, se **SQLFetch** ou **SQLFetchScroll** não retornou SQL_NO_DATA e é retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tem retornar SQL_NO_DATA.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|40001|Falha na serialização|A transação foi revertida devido a um deadlock de recursos com outra transação.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o *CatalogName* argumento era um ponteiro nulo e o SQL_CATALOG_NAME *tipo de informação* retorna nomes de catálogo têm suporte.<br /><br /> (DM) o atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE e o *SchemaName* ou *ProcName* argumento é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona foi ainda era executar quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor de um dos argumentos de comprimento do nome da era menor que 0 mas não iguais a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento de nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo de procedimento foi especificado e o driver ou fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema de procedimento foi especificado e o driver ou fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o esquema de procedimento ou o nome do procedimento e a fonte de dados não dá suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era compatível com a driver ou fonte de dados.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada um conjunto de resultado solicitada. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não oferece suporte a essa função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLProcedures** lista todos os procedimentos no intervalo solicitado. Um usuário pode ou não pode ter a permissão para executar qualquer um destes procedimentos. Para verificar a acessibilidade, um aplicativo pode chamar **SQLGetInfo** e verifique o valor de informações SQL_ACCESSIBLE_PROCEDURES. Caso contrário, o aplicativo deve ser capaz de lidar com uma situação em que o usuário seleciona um procedimento que ele não é possível executar. Para obter informações sobre como essas informações podem ser usadas, consulte [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, os argumentos e os dados retornados de funções de catálogo ODBC, consulte [funções de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedures** retorna os resultados como um conjunto de resultados padrão, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEMA e PROCEDURE_NAME.  
  
> [!NOTE]  
>  **SQLProcedures** não pode retornar todos os procedimentos. Os aplicativos podem usar qualquer procedimento válido, independentemente se ele é retornado por **SQLProcedures**.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores, porque aplicativos associar por número de coluna.  
  
|Coluna de ODBC 2.0|3 de ODBC *. x* coluna|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMENTO _OWNER|PROCEDIMENTO _SCHEM|  
  
 Para determinar os comprimentos reais das colunas PROCEDURE_CAT, PROCEDURE_SCHEM e PROCEDURE_NAME, um aplicativo pode chamar **SQLGetInfo** com o SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_PROCEDURE_ Opções de NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PROCEDURE_TYPE) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contagem regressiva do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados pelas funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Identificador do catálogo de procedimento; NULL se não for aplicável à fonte de dados. Se um driver compatível com catálogos para alguns procedimentos, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para esses procedimentos que não têm catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Identificador do esquema de procedimento; NULL se não for aplicável à fonte de dados. Se um driver compatível com esquemas para alguns procedimentos, mas não para outras pessoas, como quando o driver recupera os dados de diferentes DBMSs, ele retorna uma cadeia de caracteres vazia ("") para esses procedimentos que não tem esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar não nulo|Identificador de procedimento.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/A|Reservado para uso futuro. Aplicativos não devem confiar nos dados retornados nessas colunas de resultado.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/A|Reservado para uso futuro. Aplicativos não devem confiar nos dados retornados nessas colunas de resultado.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/A|Reservado para uso futuro. Aplicativos não devem confiar nos dados retornados nessas colunas de resultado.|  
|COMENTÁRIOS (ODBC 2.0)|7|Varchar|Uma descrição do procedimento.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|Define o tipo de procedimento:<br /><br /> SQL_PT_UNKNOWN: Ele não é possível determinar se o procedimento retorna um valor.<br /><br /> SQL_PT_PROCEDURE: O objeto retornado é um procedimento; ou seja, ele não tem um valor de retorno.<br /><br /> SQL_PT_FUNCTION: O objeto retornado é uma função; ou seja, ele tem um valor de retorno.|  
  
 O *SchemaName* e *ProcName* argumentos aceitam os padrões de pesquisa. Para obter mais informações sobre padrões de pesquisa válida, consulte [argumentos de valor padrão de](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Retornando os parâmetros e o resultado de conjunto de colunas de um procedimento|[Função SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|Sintaxe para chamar procedimentos armazenados|[Execução de instruções](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
