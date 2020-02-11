---
title: Função SQLDescribeCol | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63982d87f0dbbe0c8ab1a540185e298d9943f630
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68104791"
---
# <a name="sqldescribecol-function"></a>Função SQLDescribeCol
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 **SQLDescribeCol** retorna o descritor de resultado-nome da coluna, tipo, tamanho da coluna, dígitos decimais e nulidade-para uma coluna no conjunto de resultados. Essas informações também estão disponíveis nos campos do IRD.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *ColumnNumber*  
 Entrada Número de coluna de dados de resultado, ordenados sequencialmente no aumento da ordem das colunas, começando em 1. O argumento *ColumnNumber* também pode ser definido como 0 para descrever a coluna de indicadores.  
  
 *ColumnName*  
 Der Ponteiro para um buffer terminado em nulo no qual retornar o nome da coluna. Esse valor é lido no campo SQL_DESC_NAME do IRD. Se a coluna não tiver nome ou o nome da coluna não puder ser determinado, o driver retornará uma cadeia de caracteres vazia.  
  
 Se *ColumnName* for NULL, *NameLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *ColumnName*.  
  
 *BufferLength*  
 Entrada Comprimento do buffer **ColumnName* , em caracteres.  
  
 *NameLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo a terminação nula) disponíveis para retornar \*em *ColumnName*. Se o número de caracteres disponíveis para retornar for maior ou igual a *BufferLength*, o nome da coluna em \* *ColumnName* será truncado para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
 *DataTypePtr*  
 Der Ponteiro para um buffer no qual retornar o tipo de dados SQL da coluna. Esse valor é lido no campo SQL_DESC_CONCISE_TYPE do IRD. Esse será um dos valores em tipos de [dados SQL](../../../odbc/reference/appendixes/sql-data-types.md)ou um tipo de dados SQL específico do driver. Se o tipo de dados não puder ser determinado, o driver retornará SQL_UNKNOWN_TYPE.  
  
 No ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP é retornado em * \*DataTypePtr* para dados de data, hora ou timestamp, respectivamente; no ODBC 2. *x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP é retornado. O Gerenciador de driver executa os mapeamentos necessários quando um ODBC 2. o aplicativo *x* está trabalhando com um ODBC 3. *x* driver ou quando um ODBC 3. o aplicativo *x* está funcionando com um ODBC 2. Driver *x* .  
  
 Quando *ColumnNumber* é igual a 0 (para uma coluna de indicador), SQL_BINARY é retornado em * \*DataTypePtr* para indicadores de comprimento variável. (SQL_INTEGER será retornado se os indicadores forem usados por um ODBC 3. *x* aplicativo trabalhando com um ODBC 2. Driver *x* ou por um ODBC 2. *x* aplicativo trabalhando com um ODBC 3. Driver *x* .)  
  
 Para obter mais informações sobre esses tipos de dados, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre tipos de dados do SQL específicos do driver, consulte a documentação do driver.  
  
 *ColumnSizePtr*  
 Der Ponteiro para um buffer no qual retornar o tamanho (em caracteres) da coluna na fonte de dados. Se o tamanho da coluna não puder ser determinado, o driver retornará 0. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.  
  
 *DecimalDigitsPtr*  
 Der Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna na fonte de dados. Se o número de dígitos decimais não puder ser determinado ou não for aplicável, o driver retornará 0. Para obter mais informações sobre dígitos decimais, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.  
  
 *NullablePtr*  
 Der Ponteiro para um buffer no qual retornar um valor que indica se a coluna permite valores nulos. Esse valor é lido no campo SQL_DESC_NULLABLE do IRD. O valor é um dos seguintes:  
  
 SQL_NO_NULLS: a coluna não permite valores nulos.  
  
 SQL_NULLABLE: a coluna permite valores nulos.  
  
 SQL_NULLABLE_UNKNOWN: o driver não pode determinar se a coluna permite valores nulos.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **SQLDescribeCol** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDescribeCol** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|DESCRIÇÃO|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O buffer \* *ColumnName* não era grande o suficiente para retornar o nome inteiro da coluna, portanto, o nome da coluna estava truncado. O comprimento do nome de coluna não truncado é retornado em **NameLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07005|Instrução preparada não é uma *especificação de cursor*|A instrução associada ao *StatementHandle* não retornou um conjunto de resultados. Não havia colunas para descrever.|  
|07009|Índice de descritor inválido|(DM) o valor especificado para o argumento *ColumnNumber* era igual a 0 e a opção de instrução SQL_ATTR_USE_BOOKMARKS foi SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *ColumnNumber* era maior que o número de colunas no conjunto de resultados.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Falha de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando **SQLDescribeCol** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) a função foi chamada antes de chamar **SQLPrepare**, **SQLExecute**ou uma função de catálogo no identificador de instrução.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *BufferLength* era menor que 0.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
 **SQLDescribeCol** pode retornar qualquer SQLSTATE que possa ser retornado por **SQLPrepare** ou **SQLExecute** quando chamado após **SQLPrepare** e before **SQLExecute**, dependendo de quando a fonte de dados avaliar a instrução SQL associada ao identificador de instrução.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLDescribeCol** antes de executar uma instrução.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLDescribeCol** após uma chamada para **SQLPrepare** e antes ou depois da chamada associada para **SQLExecute**. Um aplicativo também pode chamar **SQLDescribeCol** após uma chamada para **SQLExecDirect**. Para obter mais informações, consulte [metadados do conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera o nome da coluna, o tipo e o comprimento gerados por uma instrução **Select** . Se a coluna for uma expressão, **ColumnName* será uma cadeia de caracteres vazia ou um nome definido pelo driver.  
  
> [!NOTE]  
>  O ODBC oferece suporte a SQL_NULLABLE_UNKNOWN como uma extensão, mesmo que a especificação de interface de nível de chamada do grupo aberto e do SQL Access não especifique a opção para **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Buscando várias linhas de dados|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando o número de colunas do conjunto de resultados|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparando uma instrução para execução|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
