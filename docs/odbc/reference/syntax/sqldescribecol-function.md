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
manager: craigg
ms.openlocfilehash: 0240d5fe1f701715f11adc4f68e80abed896d704
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47742684"
---
# <a name="sqldescribecol-function"></a>Função SQLDescribeCol
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 1.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLDescribeCol** retorna o descritor de resultado — nome da coluna, tipo, tamanho da coluna, dígitos decimais e nulidade — para uma coluna no resultado definido. Essas informações também estão disponíveis nos campos do IRD.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução.  
  
 *ColumnNumber*  
 [Entrada] Número da coluna de dados de resultado sequencialmente ordenados em ordem crescente de coluna, começando em 1. O *ColumnNumber* argumento também pode ser definido como 0 para descrever a coluna de indicador.  
  
 *ColumnName*  
 [Saída] Ponteiro para um buffer de terminação nula no qual retornar o nome da coluna. Esse valor é lido do campo SQL_DESC_NAME do IRD. Se a coluna for sem nome ou o nome da coluna não pode ser determinado, o driver retornará uma cadeia de caracteres vazia.  
  
 Se *ColumnName* for NULL, *NameLengthPtr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por *ColumnName*.  
  
 *BufferLength*  
 [Entrada] Comprimento do **ColumnName* buffer em caracteres.  
  
 *NameLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo a terminação nula) disponíveis para retornar na \* *ColumnName*. Se o número de caracteres disponíveis para retornar for maior que ou igual a *BufferLength*, o nome da coluna na \* *ColumnName* será truncado para *BufferLength*menos o comprimento de um caractere nulo de terminação.  
  
 *DataTypePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tipo de dados SQL da coluna. Esse valor é lido do campo SQL_DESC_CONCISE_TYPE do IRD. Isso será um dos valores na [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md), ou um tipo de dados SQL específica do driver. Se o tipo de dados não puder ser determinado, o driver retornará SQL_UNKNOWN_TYPE.  
  
 Em ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP é retornado na  *\*DataTypePtr* para data, hora ou dados de carimbo de hora, respectivamente; no ODBC 2. *x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP é retornado. O Gerenciador de Driver executa os mapeamentos necessários quando um ODBC 2. *x* aplicativo está funcionando com um ODBC 3. *x* driver ou quando um ODBC 3. *x* aplicativo está funcionando com um ODBC 2. *x* driver.  
  
 Quando *ColumnNumber* é igual a 0 (para uma coluna de indicador), SQL_BINARY é retornado na  *\*DataTypePtr* para indicadores de comprimento variável. (SQL_INTEGER é retornada se os indicadores são usados por um ODBC 3. *x* aplicativo trabalhar com um ODBC 2. *x* driver ou por um ODBC 2. *x* aplicativo trabalhar com um ODBC 3. *x* driver.)  
  
 Para obter mais informações sobre esses tipos de dados, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) apêndice d: tipos de dados. Para obter informações sobre tipos de dados SQL específico do driver, consulte a documentação do driver.  
  
 *ColumnSizePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tamanho (em caracteres) da coluna na fonte de dados. Se o tamanho da coluna não puder ser determinado, o driver retornará 0. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) apêndice d: tipos de dados.  
  
 *DecimalDigitsPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna na fonte de dados. Se o número de dígitos decimais não pode ser determinado ou não é aplicável, o driver retornará 0. Para obter mais informações sobre os dígitos decimais, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto de transferência e o tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) apêndice d: tipos de dados.  
  
 *NullablePtr*  
 [Saída] Ponteiro para um buffer no qual retornar um valor que indica se a coluna permite valores nulos. Esse valor é lido do campo SQL_DESC_NULLABLE do IRD. O valor é um dos seguintes:  
  
 SQL_NO_NULLS: A coluna não permite valores nulos.  
  
 SQL_NULLABLE: A coluna permite valores nulos.  
  
 SQL_NULLABLE_UNKNOWN: O driver não pode determinar se a coluna permite valores nulos.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLDescribeCol** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType*sql_handle_stmt e uma *manipular* dos *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDescribeCol** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *ColumnName* não era grande o suficiente para retornar o nome da coluna inteira, portanto, o nome da coluna foi truncado. O comprimento do nome da coluna completo será retornado no **NameLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07005|Instrução preparada não um *especificação de cursor*|A instrução associada a *StatementHandle* não retornou um conjunto de resultados. Não havia nenhuma coluna para descrever.|  
|07009|Índice de descritor inválido|(DM) o valor especificado para o argumento *ColumnNumber* era igual a 0, e a opção de instrução SQL_ATTR_USE_BOOKMARKS era SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *ColumnNumber* era maior que o número de colunas no conjunto de resultados.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Falha de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando **SQLDescribeCol** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM), a função foi chamada antes de chamar **SQLPrepare**, **SQLExecute**, ou uma função de catálogo no identificador da instrução.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *BufferLength* foi menor que 0.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
 **SQLDescribeCol** pode retornar qualquer SQLSTATE que pode ser retornado por **SQLPrepare** ou **SQLExecute** quando chamado depois **SQLPrepare** e antes **SQLExecute**, dependendo de quando a fonte de dados avalia a instrução SQL associada com o identificador de instrução.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLDescribeCol** antes de executar uma instrução.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLDescribeCol** após uma chamada para **SQLPrepare** e antes ou depois da chamada associada ao **SQLExecute**. Um aplicativo também pode chamar **SQLDescribeCol** após uma chamada para **SQLExecDirect**. Para obter mais informações, consulte [metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera o nome da coluna, tipo e comprimento gerados por um **selecione** instrução. Se a coluna for uma expressão **ColumnName* é uma cadeia de caracteres vazia ou um nome definido pelo driver.  
  
> [!NOTE]  
>  ODBC dá suporte a SQL_NULLABLE_UNKNOWN como uma extensão, mesmo que a especificação do Open Group e chamar Interface nível de grupo de acesso SQL não especificar a opção para **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Buscar várias linhas de dados|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Colunas de conjunto de retorno do número de resultados|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Como preparar uma instrução para execução|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
