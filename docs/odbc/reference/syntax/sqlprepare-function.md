---
title: "Função SQLPrepare | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2bdb9a85c14f3636286ea9ca97ea173c9c2b65a4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlprepare-function"></a>Função SQLPrepare
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLPrepare** prepara uma cadeia de caracteres SQL para execução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLPrepare** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLPrepare** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|Um atributo de instrução especificada era inválido devido a condições de trabalho de implementação para que um valor semelhante temporariamente foi substituído. (**SQLGetStmtAttr** pode ser chamado para determinar o que é o valor substituído temporariamente.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado. Os atributos de instrução que podem ser alterados são: SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|21S01|Lista de valores de inserção não corresponde a lista de colunas|\**StatementText* continha um **inserir** instrução e o número de valores a serem inseridos não coincidiu com o grau da tabela derivada.|  
|21S02|Grau da tabela derivada não corresponde à lista de coluna|\**StatementText* continha um **CREATE VIEW** instrução e o número de nomes especificado não é o mesmo grau da tabela derivada definida pela especificação de consulta.|  
|22018|Valor de caractere inválido para especificação de coerção|**StatementText* continha uma instrução SQL que continha um literal ou um parâmetro e o valor era incompatível com o tipo de dados da coluna da tabela associada.|  
|22019|Caractere de escape inválido|O argumento *StatementText* continha um **como** predicado com um **ESCAPE** no **onde** cláusula e o comprimento do escape os seguintes caracteres **ESCAPE** não era igual a 1.|  
|22025|Sequência de escape inválido|O argumento *StatementText* contidos "**como** *padrão valor* **ESCAPE** *decaracteredeescape*"no **onde** cláusula e o caractere que segue o caractere de escape no valor padrão não era"%"nem"_".|  
|24000|Estado de cursor inválido|(DM) um cursor foi aberto o *StatementHandle*, e **SQLFetch** ou **SQLFetchScroll** tivesse sido chamada.<br /><br /> Um cursor foi aberto o *StatementHandle*, mas **SQLFetch** ou **SQLFetchScroll** não tivesse sido chamada.|  
|34000|Nome de cursor inválido|\**StatementText* continha um posicionadas **excluir** ou um posicionadas **atualização**, e o cursor referenciado pela instrução que está sendo preparada não foi aberto.|  
|3D000|Nome de catálogo inválido|O nome de catálogo especificado no *StatementText* era inválido.|  
|3F000|Nome de esquema inválido|O nome do esquema especificado no *StatementText* era inválido.|  
|42000|Sintaxe ou violação de acesso|\**StatementText* continha uma instrução SQL que não era preparável ou contiver um erro de sintaxe.<br /><br /> **StatementText* continha uma instrução para o qual o usuário não tem os privilégios necessários.|  
|42S01|Tabela ou exibição básica já existe|\**StatementText* continha um **CREATE TABLE** ou **CREATE VIEW** instrução e o nome da tabela ou exibição de nome especificado já existe.|  
|42S02|Tabela base ou exibição não encontrado|\**StatementText* continha um **DROP TABLE** ou um **DROP VIEW** instrução e o nome da tabela especificada ou exibição de nome não existe.<br /><br /> \**StatementText* continha um **ALTER TABLE** instrução e o nome da tabela especificada não existe.<br /><br /> \**StatementText* continha um **CREATE VIEW** instrução e um nome de tabela ou exibição definida pela especificação de consulta de nome não existe.<br /><br /> \**StatementText* continha um **CREATE INDEX** instrução e o nome da tabela especificada não existe.<br /><br /> \**StatementText* continha um **GRANT** ou **REVOGAR** instrução e o nome da tabela especificada ou exibição de nome não existe.<br /><br /> \**StatementText* continha um **selecione** instrução e um nome de tabela especificada ou exibição de nome não existe.<br /><br /> \**StatementText* continha um **excluir**, **inserir**, ou **atualização** instrução e o nome da tabela especificada não existe.<br /><br /> \**StatementText* continha um **CREATE TABLE** instrução e uma tabela especificada em uma restrição (fazendo referência a uma tabela que está sendo criado) não existe.|  
|42S11|O índice já existe|\**StatementText* continha um **CREATE INDEX** instrução e o nome do índice especificado já existiam.|  
|42S12|Índice não encontrado|\**StatementText* continha um **DROP INDEX** instrução e o nome do índice especificado não existe.|  
|42S21|Já existe uma coluna|\**StatementText* continha um **ALTER TABLE** instrução e a coluna especificada no **adicionar** cláusula não é exclusiva ou identifica uma coluna existente na tabela base.|  
|42S22|Coluna não encontrada|\**StatementText* continha um **CREATE INDEX** instrução e um ou mais da coluna de nomes especificados na lista de colunas não existe.<br /><br /> \**StatementText* continha um **GRANT** ou **REVOGAR** instrução e um nome de coluna especificado não existe.<br /><br /> \**StatementText* continha um **selecione**, **excluir**, **inserir**, ou **atualização** instrução e uma coluna especificada nome não existe.<br /><br /> \**StatementText* continha um **CREATE TABLE** instrução e uma coluna especificada em uma restrição (fazendo referência a uma tabela que está sendo criado) não existe.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*, e, em seguida, a função foi chamada no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY009|Uso inválido de ponteiro nulo|(DM) *StatementText* foi um ponteiro nulo.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLPrepare** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o argumento *TextLength* era menor ou igual a 0, mas não é igual a SQL_NTS.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A configuração de simultaneidade era inválida para o tipo de cursor definido.<br /><br /> O atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de instrução SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o driver não oferecer suporte a indicadores.|  
|HYT00|Tempo limite esgotado|O período de tempo limite expirou antes da fonte de dados retornou o conjunto de resultados. O período de tempo limite é definido por meio de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 O aplicativo chama **SQLPrepare** para enviar uma instrução SQL para a fonte de dados para preparação. Para obter mais informações sobre a execução preparada, consulte [execução preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md). O aplicativo pode incluir um ou mais marcadores de parâmetro na instrução SQL. Para incluir um marcador de parâmetro, o aplicativo insere um ponto de interrogação (?) na cadeia de caracteres SQL na posição apropriada. Para obter informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).  
  
> [!NOTE]  
>  Se um aplicativo usa **SQLPrepare** para preparar e **SQLExecute** para enviar um **confirmar** ou **REVERSÃO** instrução, ele não será interoperabilidade entre os produtos DBMS. Para confirmar ou reverter uma transação, chame **SQLEndTran**.  
  
 O driver pode modificar a instrução para usar o formulário de SQL usado pela fonte de dados e, em seguida, enviá-lo à fonte de dados para preparação. Em particular, o driver modifica as sequências de escape usadas para definir a sintaxe SQL para determinados recursos. (Para obter uma descrição da gramática de instrução SQL, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) e [gramática de SQL do apêndice c:](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).) Para o driver, um identificador de instrução é semelhante a um identificador de instrução no código SQL inserido. Se a fonte de dados oferece suporte a identificadores de instrução, o driver pode enviar um identificador de instrução e valores de parâmetro para a fonte de dados.  
  
 Depois que uma instrução é preparada, o aplicativo usa o identificador de instrução para referir-se a instrução em chamadas de função posteriormente. A instrução preparada associada com o identificador de instrução pode ser executada novamente chamando **SQLExecute** até que o aplicativo libera a instrução com uma chamada para **SQLFreeStmt** com a opção SQL_DROP ou até que o identificador de instrução é usado em uma chamada para **SQLPrepare**, **SQLExecDirect**, ou uma das funções de catálogo (**SQLColumns**,  **SQLTables**, e assim por diante). Depois que o aplicativo prepara uma instrução, ele pode solicitar informações sobre o formato do conjunto de resultados. Para algumas implementações, chamando **SQLDescribeCol** ou **SQLDescribeParam** depois **SQLPrepare** pode não ser tão eficiente quanto chamando a função após **SQLExecute** ou **SQLExecDirect**.  
  
 Alguns drivers não podem retornar erros de sintaxe ou violações de acesso quando o aplicativo chama **SQLPrepare**. Um driver pode lidar com erros de sintaxe e violações, de acesso somente erros de sintaxe, ou erros de sintaxe nem violações de acesso. Portanto, um aplicativo deve ser capaz de lidar com essas condições ao chamar subsequentes relacionadas a funções como **SQLNumResultCols**, **SQLDescribeCol**, **SQLColAttribute**, e **SQLExecute**.  
  
 Dependendo dos recursos do driver de fonte de dados, informações de parâmetro (como tipos de dados) podem ser verificadas quando a instrução é preparada (se todos os parâmetros de associação) ou quando ele é executado (se todos os parâmetros não foram ligados). Para interoperabilidade máxima, um aplicativo deve desassociar todos os parâmetros que são aplicadas a uma instrução SQL antiga antes de preparar uma nova instrução SQL na mesma instrução. Isso evita erros devido a informações antigas de parâmetro que está sendo aplicadas para a nova instrução.  
  
> [!IMPORTANT]  
>  Confirmar uma transação, ou explicitamente chamando **SQLEndTran** ou trabalhando no modo de confirmação automática, pode fazer com que a fonte de dados excluir os planos de acesso para todas as instruções em uma conexão. Para obter mais informações, consulte os tipos de informações SQL_CURSOR_COMMIT_BEHAVIOR e SQL_CURSOR_ROLLBACK_BEHAVIOR no [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) e [efeito de transações em cursores e instruções preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Alocar um identificador de instrução|[Função SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Um buffer de associação a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executar uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução preparada do SQL|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Retornando o número de linhas afetadas por uma instrução|[Função SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|Definir um nome de cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

