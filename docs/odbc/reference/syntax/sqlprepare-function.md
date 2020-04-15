---
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
ms.openlocfilehash: e9aedd665df2a943627207902d592d597c503c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306877"
---
# <a name="sqlprepare-function"></a>Função SQLPrepare
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLPrepare** prepara uma seqüência SQL para execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *StatementText*  
 [Entrada] Seqüência de texto SQL.  
  
 *TextLength*  
 [Entrada] Comprimento de **DeclaraçãoTexto* em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLPrepare** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLPrepare** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|Um atributo de declaração especificado foi inválido devido às condições de trabalho de implementação, de modo que um valor semelhante foi temporariamente substituído. (**SQLGetStmtAttr** pode ser chamado para determinar qual é o valor temporariamente substituído.) O valor substituto é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos de declaração que podem ser alterados são: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_CURSOR_TYPE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_MAX_ROWS SQL_ATTR_SIMULATE_CURSOR<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|21S01|Inserir lista de valores não corresponde à lista de colunas|\**StatementText* continha uma instrução **INSERT,** e o número de valores a serem inseridos não correspondia ao grau da tabela derivada.|  
|21S02|Grau de tabela derivada não corresponde à lista de colunas|\**StatementText* continha uma instrução **CREATE VIEW,** e o número de nomes especificados não é o mesmo grau da tabela derivada definida pela especificação da consulta.|  
|22018|Valor de caractere inválido para especificação do elenco|**StatementText* continha uma declaração SQL que continha um parâmetro literal ou de que o valor era incompatível com o tipo de dados da coluna de tabela associada.|  
|22019|Caractere de fuga inválido|O argumento *StatementText* continha um predicado **LIKE** com um **ESCAPE** na cláusula **WHERE,** e o comprimento do caractere de fuga após **ESCAPE** não era igual a 1.|  
|22025|Sequência de fuga inválida|O argumento *StatementText* continha "**LIKE** _pattern value_ **ESCAPE** _escape character_" na cláusula **WHERE,** e o caractere que seguia o caractere de fuga no valor padrão não era "%" nem "_".|  
|24.000|Estado de cursor inválido|(DM) Um cursor foi aberto no *StatementHandle*e **o SQLFetchScroll** foi chamado. **SQLFetchScroll**<br /><br /> Um cursor foi aberto no *StatementHandle,* mas **SQLFetch** ou **SQLFetchScroll** não foram chamados.|  
|34000|Nome de cursor inválido|\**StatementText* continha uma **DELETE** posicionada ou uma **ATUALIZAÇÃO**posicionada, e o cursor referenciado pela declaração que estava sendo preparada não estava aberto.|  
|3D000|Nome do catálogo inválido|O nome do catálogo especificado no *StatementText* era inválido.|  
|3F000|Nome do esquema inválido|O nome do esquema especificado no *StatementText* era inválido.|  
|42000|Erro de sintaxe ou violação de acesso|\**StatementText* continha uma declaração SQL que não era preparado ou continha um erro de sintaxe.<br /><br /> **StatementText* continha uma declaração para a qual o usuário não tinha os privilégios necessários.|  
|42S01|Tabela base ou visualização já existe|\**StatementText* continha uma **declaração CREATE TABLE** ou **CREATE VIEW,** e o nome da tabela ou nome de exibição especificado já existe.|  
|42S02|Tabela base ou vista não encontrada|\**StatementText* continha uma **TABELA DROP** ou uma declaração **DROP VIEW,** e o nome de exibição da tabela especificado não existia.<br /><br /> \**StatementText* continha uma declaração **ALTER TABLE** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma instrução **CREATE VIEW,** e um nome de tabela ou nome de exibição definido pela especificação da consulta não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE INDEX** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma declaração **GRANT** ou **REVOKE,** e o nome de tabela especificado ou nome de exibição não existia.<br /><br /> \**StatementText* continha uma declaração **SELECT,** e um nome de tabela especificado ou nome de exibição não existia.<br /><br /> \**StatementText* continha uma instrução **DELETE,** **INSERT**ou **UPDATE,** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE TABLE,** e uma tabela especificada em uma restrição (referindo-se a uma tabela diferente da que está sendo criada) não existia.|  
|42S11|Índice já existe|\**StatementText* continha uma declaração **CREATE INDEX** e o nome do índice especificado já existia.|  
|42S12|Índice não encontrado|\**StatementText* continha uma declaração **DE ÍNDICE DE QUEDA** e o nome do índice especificado não existia.|  
|42S21|Coluna já existe|\**StatementText* continha uma declaração **ALTER TABLE,** e a coluna especificada na cláusula **ADD** não é única ou identifica uma coluna existente na tabela base.|  
|42S22|Coluna não encontrada|\**StatementText* continha uma declaração **CREATE INDEX,** e um ou mais nomes de coluna especificados na lista de colunas não existiam.<br /><br /> \**StatementText* continha uma declaração **GRANT** ou **REVOKE,** e um nome de coluna especificado não existia.<br /><br /> \**StatementText* continha uma instrução **SELECT,** **DELETE,** **INSERT**ou **UPDATE** e um nome de coluna especificado não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE TABLE,** e uma coluna especificada em uma restrição (referindo-se a uma tabela diferente da que está sendo criada) não existia.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|(DM) *StatementText* foi um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLPrepare** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O argumento *TextLength* era menor ou igual a 0, mas não igual a SQL_NTS.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A configuração de simultuário era inválida para o tipo de cursor definido.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 O aplicativo chama **o SQLPrepare** para enviar uma declaração SQL à fonte de dados para preparação. Para obter mais informações sobre execução preparada, consulte [Execução Preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). O aplicativo pode incluir um ou mais marcadores de parâmetro na declaração SQL. Para incluir um marcador de parâmetro, a aplicação incorpora um ponto de interrogação (?) na seqüência SQL na posição apropriada. Para obter informações sobre parâmetros, consulte [Parâmetros de declaração](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Se um aplicativo usar **o SQLPrepare** para preparar e **o SQLExecute** enviar uma declaração **COMMIT** ou **ROLLBACK,** ele não será interoperável entre os produtos DBMS. Para cometer ou reverter uma transação, ligue para **o SQLEndTran**.  
  
 O driver pode modificar a declaração para usar o formulário de SQL usado pela fonte de dados e, em seguida, enviá-la à fonte de dados para preparação. Em particular, o driver modifica as seqüências de fuga usadas para definir a sintaxe SQL para determinadas características. (Para obter uma descrição da gramática da declaração SQL, consulte [Seqüências de fuga no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [no apêndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para o driver, uma alça de declaração é semelhante a um identificador de declaração no código SQL incorporado. Se a fonte de dados suportar identificadores de declaração, o driver poderá enviar um identificador de declaração e valores de parâmetro sustais para a fonte de dados.  
  
 Depois que uma declaração é preparada, o aplicativo usa a alça da declaração para se referir à declaração em chamadas de função posteriores. A declaração preparada associada ao cabo de declaração pode ser reexecutada ligando para **o SQLExecute** até que o aplicativo liberte a declaração com uma chamada para **o SQLFreeStmt** com a opção SQL_DROP ou até que o cabo de declaração seja usado em uma chamada para **SQLPrepare,** **SQLExecDirect,** ou uma das funções do catálogo **(SQLColumns,** **SQLTables,** etc.). Uma vez que o aplicativo prepara uma declaração, ele pode solicitar informações sobre o formato do conjunto de resultados. Para algumas implementações, chamar **SQLDescribeCol** ou **SQLDescribeParam** após **o SQLPrepare** pode não ser tão eficiente quanto chamar a função após **SQLExecute** ou **SQLExecDirect**.  
  
 Alguns drivers não podem retornar erros de sintaxe ou violações de acesso quando o aplicativo chama **SQLPrepare**. Um motorista pode lidar com erros de sintaxe e violações de acesso, apenas erros de sintaxe, ou nem erros de sintaxe nem violações de acesso. Portanto, um aplicativo deve ser capaz de lidar com essas condições ao chamar funções relacionadas subseqüentes, como **SQLNumResultCols,** **SQLDescribeCol,** **SQLColAttribute**e **SQLExecute**.  
  
 Dependendo das capacidades do driver e da fonte de dados, as informações dos parâmetros (como os tipos de dados) podem ser verificadas quando a declaração for preparada (se todos os parâmetros foram vinculados) ou quando for em execução (se todos os parâmetros não tiverem sido vinculados). Para interoperabilidade máxima, um aplicativo deve desvincular todos os parâmetros aplicados a uma declaração SQL antiga antes de preparar uma nova declaração SQL na mesma declaração. Isso evita que erros que se devem às informações de parâmetros antigos sejam aplicados à nova declaração.  
  
> [!IMPORTANT]  
>  Cometer uma transação, seja ligando explicitamente para **o SQLEndTran** ou trabalhando no modo de confirmação automática, pode fazer com que a fonte de dados exclua os planos de acesso de todas as declarações em uma conexão. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [effect of Transactions on Cursors and Prepared Statements](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindParameter,](../../../odbc/reference/syntax/sqlbindparameter-function.md) [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando uma alça de declaração|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Vinculando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o número de linhas afetadas por uma declaração|[Função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Definindo um nome do cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
