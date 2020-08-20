---
description: Função SQLProcedures
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c4e44a708f96883891d44d629fdd3c945eb283a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487142"
---
# <a name="sqlprocedures-function"></a>Função SQLProcedures
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ODBC  
  
 **Resumo**  
 **SQLProcedures** retorna a lista de nomes de procedimentos armazenados em uma fonte de dados específica. O *procedimento* é um termo genérico usado para descrever um *objeto executável*ou uma entidade nomeada que pode ser invocada usando parâmetros de entrada e saída. Para obter mais informações sobre procedimentos, consulte os [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
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
 Entrada Identificador de instrução.  
  
 *CatalogName*  
 Entrada Catálogo de procedimentos. Se um driver oferecer suporte a catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota as tabelas que não têm catálogos. *CatalogName* não pode conter um padrão de pesquisa de cadeia de caracteres.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* será um argumento comum; Ele é tratado literalmente e seu caso é significativo. Para obter mais informações, consulte [argumentos em funções de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 Entrada Comprimento em caracteres de **nome_do_catálogo*.  
  
 *SchemaName*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de esquema de procedimento. Se um driver oferecer suporte a esquemas para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, uma cadeia de caracteres vazia ("") denota os procedimentos que não têm esquemas.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *SchemaName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength2*  
 Entrada Comprimento em caracteres de **SchemaName*.  
  
 *Procname só*  
 Entrada Padrão de pesquisa de cadeia de caracteres para nomes de procedimento.  
  
 Se o atributo da instrução SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ProcName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *ProcName* será um argumento de valor de padrão; Ele é tratado literalmente e seu caso é significativo.  
  
 *NameLength3*  
 Entrada Comprimento em caracteres de **ProcName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLProcedures** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLProcedures** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|24.000|Estado de cursor inválido|Um cursor estava aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado. Esse erro será retornado pelo Gerenciador de driver se **SQLFetch** ou **SQLFetchScroll** não tiver retornado SQL_NO_DATA e será retornado pelo driver se **SQLFetch** ou **SQLFetchScroll** tiver retornado SQL_NO_DATA.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|40001|Falha de serialização|A transação foi revertida devido a um deadlock de recurso com outra transação.|  
|40003|Conclusão de instrução desconhecida|A conexão associada falhou durante a execução dessa função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|O atributo da instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes de catálogo têm suporte.<br /><br /> (DM) o atributo de instrução SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* ou *ProcName* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor de um dos argumentos de comprimento do nome era menor que 0, mas não é igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor de comprimento máximo para o nome correspondente.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo de procedimentos foi especificado e o driver ou a fonte de dados não oferece suporte a catálogos.<br /><br /> Um esquema de procedimento foi especificado e o driver ou a fonte de dados não oferece suporte a esquemas.<br /><br /> Um padrão de pesquisa de cadeia de caracteres foi especificado para o esquema de procedimento ou o nome do procedimento, e a fonte de dados não oferece suporte a padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de instrução SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não era suportada pelo driver ou pela fonte de dados.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte a essa função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLProcedures** lista todos os procedimentos no intervalo solicitado. Um usuário pode ou não ter permissão para executar qualquer um desses procedimentos. Para verificar a acessibilidade, um aplicativo pode chamar **SQLGetInfo** e verificar o valor das informações de SQL_ACCESSIBLE_PROCEDURES. Caso contrário, o aplicativo deve ser capaz de lidar com uma situação em que o usuário seleciona um procedimento que ele não pode executar. Para obter informações sobre como essas informações podem ser usadas, consulte [procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados de funções de catálogo ODBC, consulte [Catalog Functions](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLProcedures** retorna os resultados como um conjunto de resultados padrão, ordenados por PROCEDURE_CAT, PROCEDURE_SCHEMA e PROCEDURE_NAME.  
  
> [!NOTE]  
>  **SQLProcedures** pode não retornar todos os procedimentos. Os aplicativos podem usar qualquer procedimento válido, independentemente de terem sido retornados por **SQLProcedures**.  
  
 As colunas a seguir foram renomeadas para ODBC 3 *. x*. As alterações de nome de coluna não afetam a compatibilidade com versões anteriores porque os aplicativos são associados por número de coluna.  
  
|Coluna ODBC 2,0|Coluna ODBC 3 *. x*|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMENTO _OWNER|PROCEDIMENTO _SCHEM|  
  
 Para determinar os comprimentos reais das colunas PROCEDURE_CAT, PROCEDURE_SCHEM e PROCEDURE_NAME, um aplicativo pode chamar **SQLGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_PROCEDURE_NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PROCEDURE_TYPE) podem ser definidas pelo driver. Um aplicativo deve obter acesso a colunas específicas do driver, contando a partir do final do conjunto de resultados em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [dados retornados por funções de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2,0)|1|Varchar|Identificador do catálogo de procedimentos; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a catálogos para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para os procedimentos que não têm catálogos.|  
|PROCEDURE_SCHEM (ODBC 2,0)|2|Varchar|Identificador de esquema de procedimento; NULL se não for aplicável à fonte de dados. Se um driver oferecer suporte a esquemas para alguns procedimentos, mas não para outros, como quando o driver recupera dados de DBMSs diferentes, ele retorna uma cadeia de caracteres vazia ("") para os procedimentos que não têm esquemas.|  
|PROCEDURE_NAME (ODBC 2,0)|3|Varchar não nulo|Identificador de procedimento.|  
|NUM_INPUT_PARAMS (ODBC 2,0)|4|N/D|Reservado para uso futuro. Os aplicativos não devem depender dos dados retornados nessas colunas de resultado.|  
|NUM_OUTPUT_PARAMS (ODBC 2,0)|5|N/D|Reservado para uso futuro. Os aplicativos não devem depender dos dados retornados nessas colunas de resultado.|  
|NUM_RESULT_SETS (ODBC 2,0)|6|N/D|Reservado para uso futuro. Os aplicativos não devem depender dos dados retornados nessas colunas de resultado.|  
|COMENTÁRIOS (ODBC 2,0)|7|Varchar|Uma descrição do procedimento.|  
|PROCEDURE_TYPE (ODBC 2,0)|8|Smallint|Define o tipo de procedimento:<br /><br /> SQL_PT_UNKNOWN: não é possível determinar se o procedimento retorna um valor.<br /><br /> SQL_PT_PROCEDURE: o objeto retornado é um procedimento; ou seja, ele não tem um valor de retorno.<br /><br /> SQL_PT_FUNCTION: o objeto retornado é uma função; ou seja, ele tem um valor de retorno.|  
  
 Os argumentos *SchemaName* e *ProcName* aceitam padrões de pesquisa. Para obter mais informações sobre padrões de pesquisa válidos, consulte [argumentos de valor de padrão](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção somente de avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando informações sobre um driver ou uma fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Retornando os parâmetros e as colunas do conjunto de resultados de um procedimento|[Função SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|Sintaxe para invocar procedimentos armazenados|[Executando instruções](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
