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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 292b1c4d9cd0281de610af4e53f25aa3d0ab6f90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005761"
---
# <a name="sqlprepare-function"></a>Função SQLPrepare
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 1.0 ODBC: ISO 92  
  
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
 [Entrada] Identificador de instrução.  
  
 *StatementText*  
 [Entrada] Cadeia de caracteres de texto SQL.  
  
 *TextLength*  
 [Entrada] Comprimento de **StatementText* em caracteres.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLPrepare** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPrepare** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|Um atributo de declaração especificada era inválido devido a condições de trabalho de implementação, portanto, um valor semelhante foi substituído temporariamente. (**SQLGetStmtAttr** pode ser chamado para determinar o que é o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|21S01|Lista de valores de inserção não corresponde a lista de colunas|\**StatementText* continha um **inserir** instrução e o número de valores a serem inseridos não correspondeu ao grau da tabela derivada.|  
|21S02|Grau da tabela derivada não corresponde à lista de colunas|\**StatementText* continha uma **CREATE VIEW** instrução e o número de nomes especificado não é o mesmo grau da tabela derivada definida pela especificação de consulta.|  
|22018|Valor de caractere inválido para especificação de conversão|**StatementText* continha uma instrução SQL que continha um literal ou um parâmetro e o valor era incompatível com o tipo de dados da coluna da tabela associada.|  
|22019|Caractere de escape inválido|O argumento *StatementText* contidos um **como** predicado com um **ESCAPE** no **onde** cláusula e o comprimento do escape a seguir caractere **ESCAPE** não era igual a 1.|  
|22025|Sequência de escape inválida|O argumento *StatementText* contido "**como** _valor de padrão_ **ESCAPE** _decaracteredeescape_"no **onde** cláusula e o caractere que segue o caractere de escape no valor padrão não foi"%"nem"_".|  
|24000|Estado de cursor inválido|(DM) um cursor foi aberto sobre o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada.<br /><br /> Um cursor foi aberto sobre o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|34000|Nome de cursor inválido|\**StatementText* continha um posicionadas **exclua** ou um posicionadas **atualização**, e o cursor referenciado pela instrução que está sendo preparada não foi aberto.|  
|3D000|Nome de catálogo inválido|O nome de catálogo especificado na *StatementText* era inválido.|  
|3F000|Nome de esquema inválido|O nome do esquema especificado na *StatementText* era inválido.|  
|42000|Sintaxe ou violação de acesso|\**StatementText* continha uma instrução SQL que não era preparável ou continha um erro de sintaxe.<br /><br /> **StatementText* continha uma instrução para o qual o usuário não tem os privilégios necessários.|  
|42S01|Tabela base ou exibição já existe|\**StatementText* continha uma **CREATE TABLE** ou **CREATE VIEW** instrução e o nome da tabela ou exibição, o nome especificado já existe.|  
|42S02|Tabela base ou exibição não encontrado|\**StatementText* continha uma **DROP TABLE** ou uma **DROP VIEW** instrução e o nome da tabela especificada ou exibição de nome não existe.<br /><br /> \**StatementText* continha um **ALTER TABLE** instrução e o nome da tabela especificada não existe.<br /><br /> \**StatementText* continha uma **CREATE VIEW** instrução e um nome de tabela ou exibição definida pela especificação de consulta de nome não existe.<br /><br /> \**StatementText* continha uma **CREATE INDEX** instrução e o nome da tabela especificada não existe.<br /><br /> \**StatementText* continha uma **GRANT** ou **REVOGAR** instrução e o nome da tabela especificada ou exibição de nome não existe.<br /><br /> \**StatementText* continha uma **selecione** instrução e um nome de tabela especificada ou exibição de nome não existe.<br /><br /> \**StatementText* continha uma **excluir**, **inserir**, ou **atualização** instrução e o nome da tabela especificada não existe.<br /><br /> \**StatementText* continha uma **CREATE TABLE** instrução e uma tabela especificada em uma restrição (que referenciam uma tabela diferente daquele que está sendo criado) não existe.|  
|42S11|O índice já existe|\**StatementText* continha uma **CREATE INDEX** instrução e o nome do índice especificado já existiam.|  
|42S12|Índice não encontrado|\**StatementText* continha uma **DROP INDEX** instrução e o nome do índice especificado não existe.|  
|42S21|A coluna já existe|\**StatementText* continha um **ALTER TABLE** instrução e a coluna especificada na **adicionar** cláusula não é exclusiva ou identifica uma coluna existente na tabela base.|  
|42S22|Coluna não encontrada|\**StatementText* continha uma **CREATE INDEX** instrução e um ou mais da coluna nomes especificados na lista de colunas não existia.<br /><br /> \**StatementText* continha uma **GRANT** ou **REVOGAR** instrução e um nome de coluna especificado não existe.<br /><br /> \**StatementText* continha uma **selecionar**, **excluir**, **inserir**, ou **atualização** instrução e um nome de coluna especificado não existe.<br /><br /> \**StatementText* continha uma **CREATE TABLE** instrução e uma coluna especificada em uma restrição (que referenciam uma tabela diferente daquele que está sendo criado) não existe.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) *StatementText* é um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLPrepare** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o argumento *TextLength* era menor que ou igual a 0, mas não é igual a SQL_NTS.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A configuração de simultaneidade era inválida para o tipo de cursor definido.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo SQL_ATTR_CURSOR_TYPE de instrução foi definido como um tipo de cursor para o qual o driver não oferece suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes da fonte de dados retornado o conjunto de resultados. O período de tempo limite é definido por meio **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 O aplicativo chama **SQLPrepare** para enviar uma instrução SQL para a fonte de dados para preparação. Para obter mais informações sobre a execução preparada, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). O aplicativo pode incluir um ou mais marcadores de parâmetro na instrução SQL. Para incluir um marcador de parâmetro, o aplicativo insere um ponto de interrogação (?) na cadeia de caracteres SQL na posição apropriada. Para obter informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Se um aplicativo usa **SQLPrepare** para se preparar e **SQLExecute** para enviar um **confirmar** ou **REVERSÃO** instrução, ele não poderá ser interoperabilidade entre os produtos DBMS. Para confirmar ou reverter uma transação, chame **SQLEndTran**.  
  
 O driver pode modificar a instrução para usar o formulário de SQL usado pela fonte de dados e, em seguida, enviá-lo à fonte de dados para preparação. Em particular, o driver modifica as sequências de escape usadas para definir a sintaxe SQL para determinados recursos. (Para obter uma descrição de gramática de instrução SQL, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [apêndice c: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para o driver, um identificador de instrução é semelhante a um identificador de instrução no código inserido do SQL. Se a fonte de dados dá suporte a identificadores de instrução, o driver pode enviar um identificador de instrução e valores de parâmetro para a fonte de dados.  
  
 Depois que uma instrução é preparada, o aplicativo usa o identificador de instrução para referir-se à instrução em chamadas de função posteriores. A instrução preparada associada com o identificador de instrução pode ser executada novamente chamando **SQLExecute** até que o aplicativo liberará a instrução com uma chamada para **SQLFreeStmt** com a opção SQL_DROP ou até que o identificador de instrução é usado em uma chamada para **SQLPrepare**, **SQLExecDirect**, ou uma das funções de catálogo (**SQLColumns**,  **SQLTables**e assim por diante). Depois que o aplicativo prepara uma instrução, ele pode solicitar informações sobre o formato do conjunto de resultados. Para algumas implementações, chamando **SQLDescribeCol** ou **SQLDescribeParam** após **SQLPrepare** pode não ser tão eficiente quanto chamar a função após **SQLExecute** ou **SQLExecDirect**.  
  
 Alguns drivers não podem retornar erros de sintaxe ou violações de acesso quando o aplicativo chama **SQLPrepare**. Um driver pode lidar com erros de sintaxe e acessar violações, apenas erros de sintaxe, ou erros de sintaxe nem violações de acesso. Portanto, um aplicativo deve ser capaz de lidar com essas condições quando chamar subsequentes relacionadas a funções como **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**, e **SQLExecute**.  
  
 Dependendo dos recursos do driver e fonte de dados, informações de parâmetro (como tipos de dados) podem ser verificadas quando a instrução está preparada (se todos os parâmetros de associação) ou quando ele é executado (se todos os parâmetros não foram ligados). Para interoperabilidade máxima, um aplicativo deve desassociar todos os parâmetros que são aplicadas a uma instrução SQL antiga antes de preparar uma nova instrução SQL na mesma instrução. Isso impede que os erros que ocorrem devido a informações antigas de parâmetro que está sendo aplicadas a nova instrução.  
  
> [!IMPORTANT]  
>  Confirmar uma transação, ou explicitamente chamando **SQLEndTran** ou trabalhando no modo de confirmação automática, pode fazer com que a fonte de dados excluir os planos de acesso para todas as instruções em uma conexão. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR na [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocando um identificador de instrução|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o número de linhas afetadas por uma instrução|[Função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Configuração de um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
