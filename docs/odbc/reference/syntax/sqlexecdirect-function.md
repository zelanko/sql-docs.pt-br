---
title: Função SQLExecDirect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5739e397467deb684a4cd6c7b13a507f30b53fa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286106"
---
# <a name="sqlexecdirect-function"></a>Função SQLExecDirect
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLExecDirect** executa uma declaração de preparável, usando os valores atuais das variáveis de marcador de parâmetro, se houver algum parâmetro na declaração. **SQLExecDirect** é a maneira mais rápida de enviar uma declaração SQL para execução única.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *StatementText*  
 [Entrada] Declaração SQL a ser executada.  
  
 *TextLength*  
 [Entrada] Comprimento de **DeclaraçãoTexto* em caracteres.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO SQL_NEED_DATA, SQL_STILL_EXECUTING, SQL_ERROR, SQL_NO_DATA, SQL_INVALID_HANDLE ou SQL_PARAM_DATA_AVAILABLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLExecDirect** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLExecDirect** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01001|Conflito de operação do cursor|\**StatementText* continha uma declaração de atualização ou exclusão posicionada, e nenhuma linha ou mais de uma linha foi atualizada ou excluída. (Para obter mais informações sobre atualizações em mais de uma linha, consulte a descrição do *atributo* SQL_ATTR_SIMULATE_CURSOR em **SQLSetStmtAttr**.)<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01003|Valor NULA eliminado na função definida|O argumento *StatementText* continha uma função definida (como **AVG**, **MAX**, **MIN,** e assim por diante), mas não a função de conjunto **COUNT,** e os valores de argumento NULL foram eliminados antes da função ser aplicada. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Os dados de seqüência ou binário retornados para um parâmetro de entrada/saída ou de saída resultaram na truncação de caracteres não em branco ou dados binários não-NULOS. Se fosse um valor de corda, era truncado. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01006|Privilégio não revogado|\**StatementText* continha uma declaração **REVOKE,** e o usuário não tinha o privilégio especificado. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01007|Privilégio não concedido|StatementText era uma declaração **GRANT,** e o usuário não poderia receber o privilégio especificado. * \**|  
|01S02|Valor da opção alterado|Um atributo de declaração especificado foi inválido devido às condições de trabalho de implementação, de modo que um valor semelhante foi temporariamente substituído. (**SQLGetStmtAttr** pode ser chamado para determinar qual é o valor temporariamente substituído.) O valor de substituição é válido para o *StatementHandle* até que o cursor seja fechado, momento em que o atributo da declaração reverte para o valor anterior. Os atributos de declaração que podem ser alterados são:<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncação fracionada|Os dados retornados para um parâmetro de entrada/saída ou de saída foram truncados de tal forma que a parte fracionada de um tipo de dados numérico foi truncada ou a parte fracionada do componente de tempo de um período, carimbo de tempo ou tipo de dados de intervalo foi truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07002|Campo COUNT incorreto|O número de parâmetros especificados no **SQLBindParameter** foi menor do que \*o número de parâmetros na declaração SQL contida no *StatementText*.<br /><br /> **SQLBindParameter** foi chamado com *ParameterValuePtr* definido como um ponteiro nulo, *não StrLen_or_IndPtr* definido como SQL_NULL_DATA ou SQL_DATA_AT_EXEC, e *InputOutputType* não definido para SQL_PARAM_OUTPUT, de modo que o número de parâmetros especificados no **SQLBindParameter** era maior do que o número de parâmetros na declaração SQL contida em **StatementText*.|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados identificado pelo argumento *ValueType* no **SQLBindParameter** para o parâmetro bound não pôde ser convertido para o tipo de dados identificado pelo argumento *ParameterType* no **SQLBindParameter**.<br /><br /> O valor dos dados retornado para um parâmetro vinculado à SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT não pôde ser convertido para o tipo de dados identificado pelo argumento *ValueType* no **SQLBindParameter**.<br /><br /> (Se os valores de dados de uma ou mais linhas não pudessem ser convertidos, mas uma ou mais linhas foram devolvidas com sucesso, essa função retorna SQL_SUCCESS_WITH_INFO.)|  
|07007|Violação do valor do parâmetro restrito|O tipo de parâmetro SQL_PARAM_INPUT_OUTPUT_STREAM é usado apenas para um parâmetro que envia e recebe dados em partes. Não é permitido um buffer de entrada para este tipo de parâmetro.<br /><br /> Esse erro ocorrerá quando o tipo de parâmetro \*estiver SQL_PARAM_INPUT_OUTPUT e quando o *StrLen_or_IndPtr* especificado no **SQLBindParameter** não for igual a SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_LEN_DATA_AT_EXEC(len) ou SQL_DATA_AT_EXEC.|  
|07S01|Uso inválido de parâmetro padrão|Um valor de parâmetro, definido com **SQLBindParameter,** foi SQL_DEFAULT_PARAM, e o parâmetro correspondente não tinha um valor padrão.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|21S01|Inserir lista de valores não corresponde à lista de colunas|\**StatementText* continha uma instrução **INSERT,** e o número de valores a serem inseridos não correspondia ao grau da tabela derivada.|  
|21S02|Grau de tabela derivada não corresponde à lista de colunas|\**StatementText* continha uma instrução **CREATE VIEW** e a lista de colunas não qualificadas (o número de colunas especificadas para a exibição nos argumentos *identificadores* de coluna da instrução SQL) continha mais nomes do que o número de colunas na tabela derivada definida pelo argumento *de especificação* de consulta da instrução SQL.|  
|22001|Dados de cordas, truncação direita|A atribuição de um caractere ou valor binário a uma coluna resultou na truncação de dados de caracteres não em branco ou dados binários não nulos.|  
|22002|Variável indicador necessária, mas não fornecida|Os dados NULL estavam vinculados a um parâmetro de saída cuja *StrLen_or_IndPtr* definida pelo **SQLBindParameter** era um ponteiro nulo.|  
|22003|Valor numérico fora do alcance|**StatementText* continha uma declaração SQL que continha um parâmetro numérico vinculado ou literal, e o valor fez com que a parte inteira (em oposição a fracionária) do número fosse truncada quando atribuída à coluna de tabela associada.<br /><br /> Devolver um valor numérico (como numérico ou string) para um ou mais parâmetros de entrada/saída ou de saída teria causado a truncada a parte inteira (em oposição ao fracionado) do número.|  
|22007|Formato de data-hora inválido|**StatementText* continha uma declaração SQL que continha uma estrutura de data, hora ou carimbo de data como parâmetro vinculado, e o parâmetro era, respectivamente, uma data, hora ou carimbo de data inválidos.<br /><br /> Um parâmetro de entrada/saída ou saída foi vinculado a uma estrutura de data, hora ou carimbo de data C, e um valor no parâmetro retornado foi, respectivamente, uma data, hora ou carimbo de data inválido. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|22008|Estouro do campo datetime|**StatementText* continha uma declaração SQL que continha uma expressão de data-hora que, quando calculada, resultava em uma estrutura de data, hora ou carimbo de data que era inválida.<br /><br /> Uma expressão de data-hora calculada para um parâmetro de entrada/saída ou saída resultou em uma estrutura de data, hora ou carimbo de ponto de data C inválida.|  
|22012|Divisão por zero|**StatementText* continha uma declaração SQL que continha uma expressão aritmética que causou divisão por zero.<br /><br /> Uma expressão aritmética calculada para um parâmetro de entrada/saída ou de saída resultou em divisão por zero.|  
|22015|Estouro do campo de intervalo|StatementText continha um parâmetro numérico ou intervalado exato que, quando convertido em um tipo de dados SQL intervalado, causou uma perda de dígitos significativos. * \**<br /><br /> StatementText continha um parâmetro de intervalo com mais de um campo que, quando convertido em um tipo de dados numérico em uma coluna, não tinha representação no tipo de dados numérico. * \**<br /><br /> StatementText continha dados de parâmetros atribuídos a um tipo De SQL de intervalo, e não havia representação do valor do tipo C no tipo SQL de intervalo. * \**<br /><br /> Atribuir um parâmetro de entrada/saída ou saída que era um tipo SQL numérico ou intervalado para um tipo C de intervalo causou uma perda de dígitos significativos.<br /><br /> Quando um parâmetro de entrada/saída ou saída foi atribuído a uma estrutura de intervalo C, não houve representação dos dados na estrutura de dados de intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|StatementText continha um tipo C que era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; * \** o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.<br /><br /> Quando um parâmetro de entrada/saída ou saída foi retornado, o tipo SQL era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo C foi SQL_C_CHAR; e o valor na coluna não era um literal válido do tipo SQL vinculado.|  
|22019|Caractere de fuga inválido|\**StatementText* continha uma declaração SQL que continha um predicado **LIKE** com um **ESCAPE** na cláusula **WHERE,** e o comprimento do caractere de fuga após **ESCAPE** não era igual a 1.|  
|22025|Sequência de fuga inválida|\**StatementText* continha uma declaração SQL que continha "**LIKE** _standard value_ **ESCAPE** _escape character_" na cláusula **WHERE,** e o caractere que seguia o caractere de fuga no valor padrão não era de "%" ou "_".|  
|23000|Violação de restrição de integridade|**StatementText* continha uma declaração SQL que continha um parâmetro ou literal. O valor do parâmetro foi NULO para uma coluna definida como NÃO NULA na coluna de tabela associada, um valor duplicado foi fornecido para uma coluna restrita para conter apenas valores únicos, ou alguma outra restrição de integridade foi violada.|  
|24.000|Estado de cursor inválido|Um cursor foi posicionado no *StatementHandle* por **SQLFetch** ou **SQLFetchScroll**. Esse erro é devolvido pelo Gerenciador de driver se **o SQLFetch** ou **o SQLFetchScroll** não retornarem SQL_NO_DATA e forem devolvidos pelo driver se **o SQLFetch** ou **o SQLFetchScroll** retornarem SQL_NO_DATA.<br /><br /> Um cursor estava aberto, mas não posicionado no *StatementHandle*.<br /><br /> **StatementText* continha uma declaração de atualização ou exclusão posicionada, e o cursor foi posicionado antes do início do conjunto de resultados ou após o término do conjunto de resultados.|  
|34000|Nome de cursor inválido|**StatementText* continha uma declaração de atualização ou exclusão posicionada, e o cursor referenciado pela declaração que estava sendo executada não estava aberto.|  
|3D000|Nome do catálogo inválido|O nome do catálogo especificado no *StatementText* era inválido.|  
|3F000|Nome do esquema inválido|O nome do esquema especificado no *StatementText* era inválido.|  
|40001|Falha na serialização|A transação foi revertida devido a um impasse de recursos com outra transação.|  
|40003|Conclusão de declaração desconhecida|A conexão associada falhou durante a execução desta função, e o estado da transação não pode ser determinado.|  
|42000|Erro de sintaxe ou violação de acesso|\**StatementText* continha uma declaração SQL que não era preparado ou continha um erro de sintaxe.<br /><br /> O usuário não tinha permissão para executar a declaração SQL contida em **StatementText*.|  
|42S01|Tabela base ou visualização já existe|\**StatementText* continha uma **declaração CREATE TABLE** ou **CREATE VIEW,** e o nome da tabela ou nome de exibição especificado já existe.|  
|42S02|Tabela base ou vista não encontrada|\**StatementText* continha uma **TABELA DROP** ou uma declaração **DROP VIEW,** e o nome de exibição da tabela especificado não existia.<br /><br /> \**StatementText* continha uma declaração **ALTER TABLE** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma instrução **CREATE VIEW,** e um nome de tabela ou nome de exibição definido pela especificação da consulta não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE INDEX** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma declaração **GRANT** ou **REVOKE,** e o nome de tabela especificado ou nome de exibição não existia.<br /><br /> \**StatementText* continha uma declaração **SELECT,** e um nome de tabela especificado ou nome de exibição não existia.<br /><br /> \**StatementText* continha uma instrução **DELETE,** **INSERT**ou **UPDATE,** e o nome da tabela especificado não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE TABLE,** e uma tabela especificada em uma restrição (referindo-se a uma tabela diferente da que está sendo criada) não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE SCHEMA,** e um nome de tabela especificado ou nome de exibição não existia.|  
|42S11|Índice já existe|\**StatementText* continha uma declaração **CREATE INDEX** e o nome do índice especificado já existia.<br /><br /> \**StatementText* continha uma declaração **CREATE SCHEMA** e o nome do índice especificado já existia.|  
|42S12|Índice não encontrado|\**StatementText* continha uma declaração **DE ÍNDICE DE QUEDA** e o nome do índice especificado não existia.|  
|42S21|Coluna já existe|\**StatementText* continha uma declaração **ALTER TABLE,** e a coluna especificada na cláusula **ADD** não é única ou identifica uma coluna existente na tabela base.|  
|42S22|Coluna não encontrada|\**StatementText* continha uma declaração **CREATE INDEX,** e um ou mais nomes de coluna especificados na lista de colunas não existiam.<br /><br /> \**StatementText* continha uma declaração **GRANT** ou **REVOKE,** e um nome de coluna especificado não existia.<br /><br /> \**StatementText* continha uma instrução **SELECT,** **DELETE,** **INSERT**ou **UPDATE** e um nome de coluna especificado não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE TABLE,** e uma coluna especificada em uma restrição (referindo-se a uma tabela diferente da que está sendo criada) não existia.<br /><br /> \**StatementText* continha uma declaração **CREATE SCHEMA** e um nome de coluna especificado não existia.|  
|44000|Violação COM OPÇÃO DE VERIFICAÇÃO|A *instrução Declaraçãode* argumentoTexto continha uma instrução **INSERT** realizada em uma tabela visualizada ou uma tabela derivada da tabela visualizada que foi criada especificando **COM OPÇÃO DE VERIFICAÇÃO,** de tal forma que uma ou mais linhas afetadas pela instrução **INSERT** não estarão mais presentes na tabela visualizada.<br /><br /> A *declaração* de argumentoTexto continha uma declaração **UPDATE** realizada em uma tabela visualizada ou uma tabela derivada da tabela visualizada que foi criada especificando **COM OPÇÃO DE VERIFICAÇÃO,** de tal forma que uma ou mais linhas afetadas pela declaração **UPDATE** não estarão mais presentes na tabela visualizada.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY009|Uso inválido do ponteiro nulo|(DM) **StatementText* foi um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLExecDirect** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O argumento *TextLength* era menor ou igual a 0, mas não igual a SQL_NTS.<br /><br /> Um valor de parâmetro, definido com **SQLBindParameter,** era um ponteiro nulo, e o valor do comprimento do parâmetro não era 0, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Um valor de parâmetro, definido com **SQLBindParameter,** não era um ponteiro nulo; o tipo de dados C foi SQL_C_BINARY ou SQL_C_CHAR; e o valor do comprimento do parâmetro foi inferior a 0, mas não foi SQL_NTS, SQL_NULL_DATA, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM ou menor ou igual a SQL_LEN_DATA_AT_EXEC_OFFSET.<br /><br /> Um valor de comprimento de parâmetro vinculado pelo **SQLBindParameter** foi definido como SQL_DATA_AT_EXEC; o tipo SQL foi SQL_LONGVARCHAR, SQL_LONGVARBINARY ou um tipo de dados específico de origem de dados longos; e o SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo** foi "Y".|  
|HY105|Tipo de parâmetro inválido|O valor especificado para o argumento *InputOutputType* no **SQLBindParameter** foi SQL_PARAM_OUTPUT, e o parâmetro foi um parâmetro de entrada.|  
|HY109|Posição do cursor inválido|\**StatementText* continha uma declaração de atualização ou exclusão posicionada, e o cursor foi posicionado (por **SQLSetPos** ou **SQLFetchScroll**) em uma linha que havia sido excluída ou não poderia ser buscada.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A combinação das configurações atuais dos atributos de declaração SQL_ATTR_CONCURRENCY e SQL_ATTR_CURSOR_TYPE não foi suportada pelo driver ou fonte de dados.<br /><br /> O atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE, e o atributo de declaração SQL_ATTR_CURSOR_TYPE foi definido como um tipo de cursor para o qual o motorista não suporta marcadores.|  
|HYT00|Tempo limite esgotado|O período de tempo de consulta expirou antes que a fonte de dados retornasse o conjunto de resultados. O período de tempo é definido através **de SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 O aplicativo chama **o SQLExecDirect** para enviar uma declaração SQL à fonte de dados. Para obter mais informações sobre execução direta, consulte [Execução Direta](../../../odbc/reference/develop-app/direct-execution-odbc.md). O driver modifica a declaração para usar o formulário de SQL usado pela fonte de dados e, em seguida, envia-o à fonte de dados. Em particular, o driver modifica as seqüências de fuga usadas para definir certas características no SQL. Para a sintaxe das seqüências de fuga, consulte [Sequências de Fuga em ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
 O aplicativo pode incluir um ou mais marcadores de parâmetro na declaração SQL. Para incluir um marcador de parâmetro, a aplicação incorpora um ponto de interrogação (?) na declaração SQL na posição apropriada. Para obter informações sobre parâmetros, consulte [Parâmetros de declaração](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Se a declaração SQL for uma declaração **SELECT** e se o aplicativo chamado **SQLSetCursorName** associar um cursor a uma declaração, o driver usará o cursor especificado. Caso contrário, o driver gera um nome de cursor.  
  
 Se a fonte de dados estiver no modo de confirmação manual (que exige início explícito da transação) e uma transação ainda não tiver sido iniciada, o driver iniciará uma transação antes de enviar a instrução SQL. Para obter mais informações, consulte [Modo de confirmação manual](../../../odbc/reference/develop-app/manual-commit-mode.md).  
  
 Se um aplicativo usar **o SQLExecDirect** para enviar uma declaração **COMMIT** ou **ROLLBACK,** ele não será interoperável entre os produtos DBMS. Para cometer ou reverter uma transação, um aplicativo chama **SQLEndTran**.  
  
 Se **o SQLExecDirect** encontrar um parâmetro de dados em execução, ele reatornou SQL_NEED_DATA. O aplicativo envia os dados usando **SQLParamData** e **SQLPutData**. Consulte [SQLBindParameter,](../../../odbc/reference/syntax/sqlbindparameter-function.md) [SQLParamData,](../../../odbc/reference/syntax/sqlparamdata-function.md) [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [Envio de Dados Longos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
 Se **o SQLExecDirect** executar uma instrução pesquisada, inserir ou excluir que não afete nenhuma linha na fonte de dados, a chamada para **SQLExecDirect** retorna SQL_NO_DATA.  
  
 Se o valor do atributo de declaração SQL_ATTR_PARAMSET_SIZE for maior que 1 e a declaração SQL contiver pelo menos um marcador de parâmetro, o **SQLExecDirect** executará a declaração SQL uma vez para cada conjunto de valores de parâmetro sustados dos arrays apontados pelo argumento *ParameterValuePointer* na chamada para **SQLBindParameter**. Para obter mais informações, consulte [Matrizes de Valores de Parâmetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md).  
  
 Se os marcadores forem ligados e uma consulta for executada que não possa suportar marcadores, o driver deve tentar coagir o ambiente a um que suporta marcadores alterando um valor de atributo e retornando SQLSTATE 01S02 (valor da opção alterado). Se o atributo não puder ser alterado, o driver deverá retornar SQLSTATE HY024 (valor de atributo inválido).  
  
> [!NOTE]  
>  Ao usar o pool de conexões, um aplicativo não deve executar instruções SQL que alteram o banco de dados ou o contexto do banco de dados, como a declaração de banco de _dados_ **USE** no SQL Server, que altera o catálogo usado por uma fonte de dados.  
  
## <a name="code-example"></a>Exemplo de código  
 Consulte [SQLBindCol,](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)e [Sample ODBC Program](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma operação de confirmação ou reversão|[Função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Retornando um nome de cursor|[Função SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Buscar parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornando o próximo parâmetro para enviar dados para|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Preparando uma declaração para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Envio de dados de parâmetros na hora da execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Definindo um nome do cursor|[Função SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|Definindo um atributo de declaração|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
