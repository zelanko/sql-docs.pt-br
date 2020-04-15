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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301166"
---
# <a name="sqldescribecol-function"></a>Função SQLDescribeCol
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLDescribeCol** retorna o descritor de resultado - nome da coluna, tipo, tamanho da coluna, dígitos decimais e nulidade - para uma coluna no conjunto de resultados. Essas informações também estão disponíveis nos campos do IRD.  
  
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
 [Entrada] Alça de declaração.  
  
 *ColumnNumber*  
 [Entrada] Número da coluna de dados de resultados, ordenado sequencialmente em ordem de coluna crescente, a partir de 1. O argumento *ColunaNúmero* também pode ser definido como 0 para descrever a coluna marcadores.  
  
 *ColumnName*  
 [Saída] Ponteiro para um buffer com término nulo no qual retornar o nome da coluna. Este valor é lido a partir do campo SQL_DESC_NAME do IRD. Se a coluna não tiver nome ou o nome da coluna não puder ser determinado, o driver reaposso uma seqüência vazia.  
  
 Se *O Nome da Coluna for* NULO, *NameLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado por *ColumnName*.  
  
 *BufferLength*  
 [Entrada] Comprimento do buffer ** ColumnName,* em caracteres.  
  
 *NameLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres \*(excluindo a rescisão nula) disponível para retornar em *ColumnName*. Se o número de caracteres disponíveis para retornar for maior \*ou igual a *BufferLength,* o nome da coluna em *ColumnName* será truncado para *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
 *DataTypePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tipo de dados SQL da coluna. Este valor é lido a partir do campo SQL_DESC_CONCISE_TYPE do IRD. Este será um dos valores em Tipos de [Dados SQL](../../../odbc/reference/appendixes/sql-data-types.md)ou um tipo de dados SQL específico para driver. Se o tipo de dados não puder ser determinado, o motorista retorna SQL_UNKNOWN_TYPE.  
  
 Em ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP é devolvido no * \*DataTypePtr* para dados de data, hora ou carimbo de data, respectivamente; em ODBC 2. *x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP é devolvido. O Driver Manager executa os mapeamentos necessários quando um ODBC 2. *x* aplicativo está trabalhando com um ODBC 3. *x* driver ou quando um ODBC 3. *x* aplicativo está trabalhando com um ODBC 2. *x* driver.  
  
 Quando *O Número de Colunas* é igual a 0 (para uma coluna de marcadores), SQL_BINARY é retornado no * \*DataTypePtr* para marcadores de comprimento variável. (SQL_INTEGER é devolvido se os marcadores forem usados por um ODBC 3. *x* aplicação trabalhando com um ODBC 2. *x* driver ou por um ODBC 2. *x* aplicação trabalhando com um ODBC 3. *x* driver.)  
  
 Para obter mais informações sobre esses tipos de dados, consulte [Tipos de Dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no apêndice D: Tipos de dados. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.  
  
 *ColumnSizePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tamanho (em caracteres) da coluna na fonte de dados. Se o tamanho da coluna não puder ser determinado, o driver retorna 0. Para obter mais informações sobre o tamanho da coluna, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.  
  
 *Digitsptr decimal*  
 [Saída] Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna na fonte de dados. Se o número de dígitos decimais não puder ser determinado ou não for aplicável, o motorista retorna 0. Para obter mais informações sobre dígitos decimais, consulte Tamanho da [coluna, Dígitos Decimais, Comprimento do Octeto de Transferência e Tamanho de Exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.  
  
 *AnuladoPtr*  
 [Saída] Ponteiro para um buffer no qual retornar um valor que indique se a coluna permite valores NULL. Este valor é lido a partir do campo SQL_DESC_NULLABLE do IRD. O valor é um dos seguintes:  
  
 SQL_NO_NULLS: A coluna não permite valores NULAS.  
  
 SQL_NULLABLE: A coluna permite valores NULA.  
  
 SQL_NULLABLE_UNKNOWN: O driver não pode determinar se a coluna permite valores NULOS.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLDescribeCol** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados por **SQLDescribeCol** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *ColumnName* não era grande o suficiente para retornar o nome da coluna inteira, de modo que o nome da coluna foi truncado. O comprimento do nome da coluna não truncado é retornado em **NameLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07005|Declaração preparada não uma *especificação do cursor*|A declaração associada ao *StatementHandle* não retornou um conjunto de resultados. Não havia colunas para descrever.|  
|07009|Índice de descritor inválido|(DM) O valor especificado para o argumento *ColumnNumber* era igual a 0, e a opção de declaração SQL_ATTR_USE_BOOKMARKS era SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *ColumnNumber* foi maior do que o número de colunas no conjunto de resultados.|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Falha na alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando **SQLDescribeCol** foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) A função foi chamada antes de chamar **SQLPrepare,** **SQLExecute**ou uma função de catálogo na alça da declaração.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para *o argumento BufferLength* foi inferior a 0.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 **SQLDescribeCol** pode retornar qualquer SQLSTATE que possa ser devolvido por **SQLPrepare** ou **SQLExecute** quando chamado após **o SQLPrepare** e antes **do SQLExecute,** dependendo de quando a fonte de dados avaliar a declaração SQL associada à alça da declaração.  
  
 Por razões de desempenho, um aplicativo não deve chamar **SQLDescribeCol** antes de executar uma declaração.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLDescribeCol** após uma chamada para **SQLPrepare** e antes ou depois da chamada associada ao **SQLExecute**. Um aplicativo também pode chamar **SQLDescribeCol** após uma chamada para **SQLExecDirect**. Para obter mais informações, consulte [Metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLDescribeCol** recupera o nome da coluna, o tipo e o comprimento gerados por uma declaração **SELECT.** Se a coluna for uma expressão, **ColumnName* é uma seqüência de string vazia ou um nome definido pelo driver.  
  
> [!NOTE]  
>  O ODBC suporta SQL_NULLABLE_UNKNOWN como uma extensão, embora a especificação de interface de nível de chamada do Grupo Aberto e do SQL Não especifique a opção para **SQLDescribeCol**.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|Buscando várias linhas de dados|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Retornando o número de colunas de conjunto de resultados|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Preparando uma declaração para execução|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
