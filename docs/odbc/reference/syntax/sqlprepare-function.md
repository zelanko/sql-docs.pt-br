---
description: Função SQLPrepare
title: Função SQLPrepare | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3b5d68aae8033b0710ee052b001c7942eb1f7d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487182"
---
# <a name="sqlprepare-function"></a>Função SQLPrepare
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLPrepare** prepara uma cadeia de caracteres SQL para execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *StatementText*  
 Entrada Cadeia de texto SQL.  
  
 *TextLength*  
 Entrada Comprimento de **StatementText* em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLPrepare** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPrepare** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|Um atributo de instrução especificado era inválido devido a condições de trabalho de implementação; portanto, um valor semelhante foi substituído temporariamente. (**SQLGetStmtAttr** pode ser chamado para determinar qual é o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|21S01|A lista de valores de inserção não corresponde à lista de colunas|\**StatementText* continha uma instrução **Insert** e o número de valores a serem inseridos não correspondeu ao grau da tabela derivada.|  
|21S02|O grau da tabela derivada não corresponde à lista de colunas|\**StatementText* continha uma instrução **Create View** e o número de nomes especificado não é o mesmo grau que a tabela derivada definida pela especificação de consulta.|  
|22018|Valor de caractere inválido para especificação de conversão|**StatementText* continha uma instrução SQL que continha um literal ou um parâmetro, e o valor era incompatível com o tipo de dados da coluna da tabela associada.|  
|22019|Caractere de escape inválido|O argumento *StatementText* continha um predicado **like** com um **escape** na cláusula **Where** e o comprimento do caractere de escape após **escape** não era igual a 1.|  
|22025|Sequência de escape inválida|O argumento *StatementText* continha "**como** o _valor de padrão_ **escape** escape _Character_" na cláusula **Where** , e o caractere após o caractere de escape no valor Pattern não era "%" nem "_".|  
|24.000|Estado de cursor inválido|(DM) um cursor foi aberto no *StatementHandle*e **SQLFetch** ou **SQLFetchScroll** foi chamado.<br /><br /> Um cursor estava aberto no *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tinha sido chamado.|  
|34000|Nome de cursor inválido|\**StatementText* continha uma **exclusão** posicionada ou uma **atualização**posicionada, e o cursor referenciado pela instrução que está sendo preparada não estava aberto.|  
|3D000|Nome de catálogo inválido|O nome do catálogo especificado em *StatementText* era inválido.|  
|3F000|Nome de esquema inválido|O nome do esquema especificado em *StatementText* era inválido.|  
|42000|Erro de sintaxe ou violação de acesso|\**StatementText* continha uma instrução SQL que não foi preparável ou continha um erro de sintaxe.<br /><br /> **StatementText* continha uma instrução para a qual o usuário não tinha os privilégios necessários.|  
|42S01|A tabela ou exibição base já existe|\**StatementText* continha uma instrução **CREATE TABLE** ou **Create View** , e o nome da tabela ou o nome da exibição especificado já existe.|  
|42S02|Tabela ou exibição de base não encontrada|\**StatementText* continha uma instrução **DROP TABLE** ou **drop View** , e o nome da tabela ou o nome de exibição especificado não existia.<br /><br /> \**StatementText* continha uma instrução **ALTER TABLE** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma instrução **Create View** , e um nome de tabela ou nome de exibição definido pela especificação de consulta não existia.<br /><br /> \**StatementText* continha uma instrução **CREATE INDEX** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma instrução **Grant** ou **REVOKE** e o nome da tabela ou o nome de exibição especificado não existia.<br /><br /> \**StatementText* continha uma instrução **Select** , e um nome de tabela ou nome de exibição especificado não existia.<br /><br /> \**StatementText* continha uma instrução **delete**, **Insert**ou **Update** , e o nome de tabela especificado não existia.<br /><br /> \**StatementText* continha uma instrução **CREATE TABLE** e uma tabela especificada em uma restrição (referenciando uma tabela diferente daquela que está sendo criada) não existia.|  
|42S11|O índice já existe|\**StatementText* continha uma instrução **CREATE INDEX** e o nome de índice especificado já existia.|  
|42S12|Índice não encontrado|\**StatementText* continha uma instrução **drop index** e o nome de índice especificado não existia.|  
|42S21|A coluna já existe|\**StatementText* continha uma instrução **ALTER TABLE** e a coluna especificada na cláusula **Add** não é exclusiva ou identifica uma coluna existente na tabela base.|  
|42S22|Coluna não encontrada|\**StatementText* continha uma instrução **CREATE INDEX** e um ou mais nomes de coluna especificados na lista de colunas não existiam.<br /><br /> \**StatementText* continha uma instrução **Grant** ou **REVOKE** e um nome de coluna especificado não existia.<br /><br /> \**StatementText* continha uma instrução **Select**, **delete**, **Insert**ou **Update** , e um nome de coluna especificado não existia.<br /><br /> \**StatementText* continha uma instrução **CREATE TABLE** e uma coluna especificada em uma restrição (referenciando uma tabela diferente daquela que está sendo criada) não existia.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \* MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado em *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) *StatementText* era um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLPrepare** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o argumento *TextLength* era menor ou igual a 0, mas não igual a SQL_NTS.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A configuração de simultaneidade era inválida para o tipo de cursor definido.<br /><br /> O atributo de instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não dá suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 O aplicativo chama **SQLPrepare** para enviar uma instrução SQL para a fonte de dados para preparação. Para obter mais informações sobre a execução preparada, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). O aplicativo pode incluir um ou mais marcadores de parâmetro na instrução SQL. Para incluir um marcador de parâmetro, o aplicativo insere um ponto de interrogação (?) na cadeia de caracteres SQL na posição apropriada. Para obter informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Se um aplicativo usar **SQLPrepare** para preparar e **SQLExecute** para enviar uma instrução **Commit** ou **Rollback** , ele não será interoperável entre os produtos DBMS. Para confirmar ou reverter uma transação, chame **SQLEndTran**.  
  
 O driver pode modificar a instrução para usar a forma de SQL usada pela fonte de dados e, em seguida, enviá-la à fonte de dados para preparação. Em particular, o driver modifica as sequências de escape usadas para definir a sintaxe SQL para determinados recursos. (Para obter uma descrição da gramática da instrução SQL, consulte [sequências de escape no ODBC e no](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) [Apêndice C: gramática do SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para o driver, um identificador de instrução é semelhante a um identificador de instrução no código SQL inserido. Se a fonte de dados der suporte a identificadores de instrução, o driver poderá enviar um identificador de instrução e valores de parâmetro para a fonte de dados.  
  
 Depois que uma instrução é preparada, o aplicativo usa o identificador de instrução para se referir à instrução em chamadas de função posteriores. A instrução preparada associada ao identificador de instrução pode ser executada novamente chamando **SQLExecute** até que o aplicativo libere a instrução com uma chamada para **SQLFreeStmt** com a opção SQL_DROP ou até que o identificador de instrução seja usado em uma chamada para **SQLPrepare**, **SQLExecDirect**ou uma das funções de catálogo (**SQLColumns**, **SQLTables**e assim por diante). Depois que o aplicativo prepara uma instrução, ele pode solicitar informações sobre o formato do conjunto de resultados. Para algumas implementações, chamar **SQLDescribeCol** ou **SQLDescribeParam** após **SQLPrepare** pode não ser tão eficiente quanto chamar a função após **SQLExecute** ou **SQLExecDirect**.  
  
 Alguns drivers não podem retornar erros de sintaxe ou violações de acesso quando o aplicativo chama **SQLPrepare**. Um driver pode tratar erros de sintaxe e violações de acesso, somente erros de sintaxe ou nenhum erro de sintaxe nem violações de acesso. Portanto, um aplicativo deve ser capaz de lidar com essas condições ao chamar funções relacionadas subsequentes, como **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**e **SQLExecute**.  
  
 Dependendo dos recursos do driver e da fonte de dados, as informações de parâmetro (como tipos de dados) podem ser verificadas quando a instrução for preparada (se todos os parâmetros tiverem sido associados) ou quando ele for executado (se todos os parâmetros não tiverem sido associados). Para a interoperabilidade máxima, um aplicativo deve desassociar todos os parâmetros aplicados a uma instrução SQL antiga antes de preparar uma nova instrução SQL na mesma instrução. Isso evita erros devido a informações de parâmetro antigas sendo aplicadas à nova instrução.  
  
> [!IMPORTANT]  
>  A confirmação de uma transação, seja chamando explicitamente **SQLEndTran** ou trabalhando no modo de confirmação automática, pode fazer com que a fonte de dados exclua os planos de acesso para todas as instruções em uma conexão. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR em [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [efeito de transações em cursores e instruções](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)preparadas.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador de instrução|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma operação Commit ou ROLLBACK|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o número de linhas afetadas por uma instrução|[Função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Definindo um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
