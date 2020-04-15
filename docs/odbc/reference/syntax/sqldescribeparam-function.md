---
title: Função SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be6d076ca121923a4b6769c7dad5269c3fd642ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301156"
---
# <a name="sqldescribeparam-function"></a>Função SQLDescribeParam
**Conformidade**  
 Versão introduzida: ODBC 1.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLDescribeParam** retorna a descrição de um marcador de parâmetro associado a uma declaração SQL preparada. Essas informações também estão disponíveis nos campos do IPD.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>Argumento  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *Número de parâmetros*  
 [Entrada] Número de marcadores de parâmetroordenado sequencialmente na ordem de parâmetros crescente, começando em 1.  
  
 *DataTypePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tipo de dados SQL do parâmetro. Este valor é lido a partir do campo de registro SQL_DESC_CONCISE_TYPE do IPD. Este será um dos valores na seção [SQL Data Types](../../../odbc/reference/appendixes/sql-data-types.md) do Apêndice D: Data Types ou um tipo de dados SQL específico para driver.  
  
 Em ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME ou SQL_TYPE_TIMESTAMP serão devolvidos no * \*DataTypePtr* para dados de data, hora ou carimbo de data, respectivamente; em ODBC 2. *x*, SQL_DATE, SQL_TIME ou SQL_TIMESTAMP serão devolvidos. O Driver Manager executa os mapeamentos necessários quando um ODBC 2. *x* aplicativo está trabalhando com um ODBC 3. *x* driver ou quando um ODBC 3. *x* aplicativo está trabalhando com um ODBC 2. *x* driver.  
  
 Quando *O Número de Colunas* é igual a 0 (para uma coluna de marcadores), SQL_BINARY é retornado no * \*DataTypePtr* para marcadores de comprimento variável. (SQL_INTEGER é devolvido se os marcadores forem usados por um ODBC 3. *x* aplicação trabalhando com um ODBC 2. *x* driver ou por um ODBC 2. *x* aplicação trabalhando com um ODBC 3. *x* driver.)  
  
 Para obter mais informações, consulte [Tipos de Dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) no apêndice D: Tipos de dados. Para obter informações sobre os tipos de dados SQL específicos do driver, consulte a documentação do motorista.  
  
 *ParâmetroSizePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o tamanho, em caracteres, da coluna ou expressão do marcador de parâmetro correspondente, conforme definido pela fonte de dados. Para obter mais informações sobre o tamanho da coluna, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho da Tela](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *Digitsptr decimal*  
 [Saída] Ponteiro para um buffer no qual retornar o número de dígitos decimais da coluna ou expressão do parâmetro correspondente conforme definido pela fonte de dados. Para obter mais informações sobre dígitos decimais, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *AnuladoPtr*  
 [Saída] Ponteiro para um buffer no qual retornar um valor que indique se o parâmetro permite valores NULL. Este valor é lido a partir do campo SQL_DESC_NULLABLE do IPD. Um dos seguintes:  
  
-   SQL_NO_NULLS: O parâmetro não permite valores NULAS (este é o valor padrão).  
  
-   SQL_NULLABLE: O parâmetro permite valores NULA.  
  
-   SQL_NULLABLE_UNKNOWN: O driver não pode determinar se o parâmetro permite valores NULOS.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLDescribeParam** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLDescribeParam** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|(DM) O valor especificado para o número *de parâmetros* de argumento é menor que 1.<br /><br /> O valor especificado para o argumento *ParameterNumber* foi maior do que o número de parâmetros na declaração SQL associada.<br /><br /> O marcador de parâmetro era parte de uma declaração não-DML.<br /><br /> O marcador de parâmetro satisfez-se de uma lista **SELECT.**|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|21S01|Inserir lista de valores não corresponde à lista de colunas|O número de parâmetros na instrução **INSERT** não correspondia ao número de colunas na tabela nomeada na declaração.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) A função foi chamada antes de ligar para **SQLPrepare** ou **SQLExecDirect** para o *StatementHandle*.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLDescribeParam** foi chamada.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 Os marcadores de parâmetro saem numerados na ordem de parâmetros crescentes, começando com 1, na ordem em que aparecem na declaração SQL.  
  
 **SQLDescribeParam** não retorna o tipo (entrada, entrada/saída ou saída) de um parâmetro em uma declaração SQL. Exceto nas chamadas para procedimentos, todos os parâmetros nas instruções SQL são parâmetros de entrada. Para determinar o tipo de parâmetro de cada parâmetro em uma chamada para um procedimento, um aplicativo chama **SQLProcedureColumns**.  
  
 Para obter mais informações, consulte [Desdescrever parâmetros](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Exemplo de código  
 O exemplo a seguir solicita ao usuário uma instrução SQL e, em seguida, prepara essa instrução. Em seguida, ele chama **SQLNumParams** para determinar se a declaração contém quaisquer parâmetros. Se a declaração contiver parâmetros, ela chama **SQLDescribeParam** para descrever esses parâmetros e **SQLBindParameter** para vinculá-los. Finalmente, ele solicita ao usuário os valores de quaisquer parâmetros e, em seguida, executa a instrução.  
  
```cpp  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparando uma declaração para execução|[Função SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
