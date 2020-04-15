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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4c8b8a9f22f6005d1af811e56485299bad3a425
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306837"
---
# <a name="sqlprocedures-function"></a>Função SQLProcedures
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLProcedures** retorna a lista de nomes de procedimentoarmazenados em uma fonte de dados específica. *Procedure* é um termo genérico usado para descrever um *objeto executável*, ou uma entidade nomeada que pode ser invocada usando parâmetros de entrada e saída. Para obter mais informações sobre os procedimentos, consulte os [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
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
 [Entrada] Alça de declaração.  
  
 *Catalogname*  
 [Entrada] Catálogo de procedimentos. Se um driver suporta catálogos para algumas tabelas, mas não para outras, como quando o driver recupera dados de diferentes DBMSs, uma string vazia ("") denota as tabelas que não possuem catálogos. *CatalogName* não pode conter um padrão de pesquisa de seqüência.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *o CatalogName* será tratado como um identificador e seu caso não será significativo. Se for SQL_FALSE, *CatalogName* é um argumento comum; é tratado literalmente, e seu caso é significativo. Para obter mais informações, consulte [Argumentos em Funções de Catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Comprimento em caracteres de **CatalogName*.  
  
 *Schemaname*  
 [Entrada] Padrão de pesquisa de cordas para nomes de esquema de procedimento. Se um motorista suporta esquemas para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, uma corda vazia ("") denota os procedimentos que não possuem esquemas.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *O SchemaName* é tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *SchemaName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome2*  
 [Entrada] Comprimento em caracteres de **SchemaName*.  
  
 *Procname*  
 [Entrada] Padrão de pesquisa de cordas para nomes de procedimentos.  
  
 Se o atributo de declaração SQL_ATTR_METADATA_ID for definido como SQL_TRUE, *ProcName* será tratado como um identificador e seu caso não é significativo. Se for SQL_FALSE, *ProcName* é um argumento de valor padrão; é tratado literalmente, e seu caso é significativo.  
  
 *Comprimento de nome3*  
 [Entrada] Comprimento em caracteres de **ProcName*.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLProcedures** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLProcedures** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|24.000|Estado de cursor inválido|Um cursor foi aberto no *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** foram chamados. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|O SQL_ATTR_METADATA_ID atributo de declaração foi definido como SQL_TRUE, o argumento *CatalogName* era um ponteiro nulo e o SQL_CATALOG_NAME *InfoType* retorna que os nomes do catálogo são suportados.<br /><br /> (DM) O atributo de declaração SQL_ATTR_METADATA_ID foi definido como SQL_TRUE, e o argumento *SchemaName* ou *ProcName* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor de um dos argumentos de comprimento do nome foi inferior a 0, mas não igual a SQL_NTS.<br /><br /> O valor de um dos argumentos de comprimento do nome excedeu o valor máximo de comprimento para o nome correspondente.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|Um catálogo de procedimentos foi especificado e o driver ou fonte de dados não suporta catálogos.<br /><br /> Um esquema de procedimento foi especificado, e o driver ou fonte de dados não suporta esquemas.<br /><br /> Um padrão de pesquisa de seqüência foi especificado para o esquema de procedimento ou nome do procedimento, e a fonte de dados não suporta padrões de pesquisa para um ou mais desses argumentos.<br /><br /> A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados solicitado. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta esta função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **O SQLProcedures** lista todos os procedimentos na faixa solicitada. Um usuário pode ou não ter permissão para executar qualquer um desses procedimentos. Para verificar a acessibilidade, um aplicativo pode ligar para **o SQLGetInfo** e verificar o valor das informações SQL_ACCESSIBLE_PROCEDURES. Caso contrário, o aplicativo deve ser capaz de lidar com uma situação em que o usuário seleciona um procedimento que ele não pode executar. Para obter informações sobre como essas informações podem ser usadas, consulte [Procedimentos](../../../odbc/reference/develop-app/procedures-odbc.md).  
  
> [!NOTE]  
>  Para obter mais informações sobre o uso geral, argumentos e dados retornados das funções do catálogo oDBC, consulte [Funções de Catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **O SQLProcedures** retorna os resultados como um conjunto de resultados padrão, ordenado por PROCEDURE_CAT, PROCEDURE_SCHEMA e PROCEDURE_NAME.  
  
> [!NOTE]  
>  **Os procedimentos SQL** podem não retornar todos os procedimentos. Os aplicativos podem usar qualquer procedimento válido, independentemente de ser devolvido pelo **SQLProcedures**.  
  
 As seguintes colunas foram renomeadas para ODBC 3 *.x*. As alterações de nome da coluna não afetam a compatibilidade retrógrada porque os aplicativos se ligam por número de coluna.  
  
|Coluna ODBC 2.0|Coluna ODBC 3 *.x*|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|PROCEDIMENTO _OWNER|PROCEDIMENTO _SCHEM|  
  
 Para determinar os comprimentos reais das colunas de PROCEDURE_CAT, PROCEDURE_SCHEM e PROCEDURE_NAME, um aplicativo pode chamar **sqlGetInfo** com as opções SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN e SQL_MAX_PROCEDURE_NAME_LEN.  
  
 A tabela a seguir lista as colunas no conjunto de resultados. Colunas adicionais além da coluna 8 (PROCEDURE_TYPE) podem ser definidas pelo driver. Um aplicativo deve ter acesso a colunas específicas do driver, contando abaixo do final do conjunto de resultados, em vez de especificar uma posição ordinal explícita. Para obter mais informações, consulte [Dados Retornados por Funções de Catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nome da coluna|Número da coluna|Tipo de dados|Comentários|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|Identificador de catálogo de procedimentos; NULL se não aplicável à fonte de dados. Se um motorista suporta catálogos para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, ele retorna uma string vazia (""" para aqueles procedimentos que não possuem catálogos.|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|Identificador de esquema de procedimento; NULL se não aplicável à fonte de dados. Se um motorista suporta esquemas para alguns procedimentos, mas não para outros, como quando o motorista recupera dados de diferentes DBMSs, ele retorna uma corda vazia (""" para aqueles procedimentos que não possuem esquemas.|  
|PROCEDURE_NAME (ODBC 2.0)|3|Varchar não É NULO|Identificador de procedimento.|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/D|Reservado para uso futuro. Os aplicativos não devem confiar nos dados retornados nestas colunas de resultados.|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/D|Reservado para uso futuro. Os aplicativos não devem confiar nos dados retornados nestas colunas de resultados.|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/D|Reservado para uso futuro. Os aplicativos não devem confiar nos dados retornados nestas colunas de resultados.|  
|OBSERVAÇÕES (ODBC 2.0)|7|Varchar|Uma descrição do procedimento.|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|Define o tipo de procedimento:<br /><br /> SQL_PT_UNKNOWN: Não é possível determinar se o procedimento devolve um valor.<br /><br /> SQL_PT_PROCEDURE: O objeto devolvido é um procedimento; ou seja, não tem um valor de retorno.<br /><br /> SQL_PT_FUNCTION: O objeto retornado é uma função; ou seja, tem um valor de retorno.|  
  
 Os argumentos *SchemaName* e *ProcName* aceitam padrões de pesquisa. Para obter mais informações sobre padrões de pesquisa [válidos,](../../../odbc/reference/develop-app/pattern-value-arguments.md)consulte Argumentos de valor de padrão .  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [Chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Buscar uma única linha ou um bloco de dados em uma direção somente para a frente|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando informações sobre um driver ou fonte de dados|[Função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|Retornando os parâmetros e as colunas de conjunto de resultados de um procedimento|[Função SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|Sintaxe para invocar procedimentos armazenados|[Executando instruções](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
