---
title: Função sqlbindparameter | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02f50862bcfb0295c7f098afc6856c91e0249f66
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301356"
---
# <a name="sqlbindparameter-function"></a>Função SQLBindParameter

**Conformidade**  
 Versão introduzida: ODBC 2.0 Normas Conformidade: ODBC  
  
 **Resumo**  
 **SQLBindParameter** liga um buffer a um marcador de parâmetro em uma declaração SQL. **O SQLBindParameter** suporta vinculação a um tipo de dados Unicode C, mesmo que o driver subjacente não suporte dados Unicode.  
  
> [!NOTE]  
>  Esta função substitui a função ODBC 1.0 **SQLSetParam**. Para obter mais informações, consulte "Comentários".  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>Argumentos

 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *Número de parâmetros*  
 [Entrada] Número de parâmetros, ordenado sequencialmente em ordem de parâmetros crescente, a partir de 1.  
  
 *InputOutputType*  
 [Entrada] O tipo do parâmetro. Para obter mais informações, consulte *"InputOutputType* Argument" em "Comentários".  
  
 *Valuetype*  
 [Entrada] O tipo de dados C do parâmetro. Para obter mais informações, consulte *"ValueType* Argument" em "Comentários".  
  
 *Parametertype*  
 [Entrada] O tipo de dados SQL do parâmetro. Para obter mais informações, consulte *"Argumento de parametrídeo"* em "Comentários".  
  
 *ColumnSize*  
 [Entrada] O tamanho da coluna ou expressão do marcador de parâmetro correspondente. Para obter mais informações, consulte *"Argumento de Tamanho* de Coluna" em "Comentários".  
  
 Se o aplicativo for executado em um sistema operacional Windows de 64 bits, consulte [informações de 64 bits da ODBC](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Entrada] Os dígitos decimais da coluna ou expressão do marcador de parâmetro correspondente. Para obter mais informações sobre o tamanho da coluna, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho da Tela](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParâmetroValuePtr*  
 [Entrada diferida] Um ponteiro para um buffer para os dados do parâmetro. Para obter mais informações, consulte *"Argumento paraparâmetroValuePtr"* em "Comentários".  
  
 *BufferLength*  
 [Entrada/saída] Comprimento do buffer *ParameterValuePtr* em bytes. Para obter mais informações, consulte *"BufferLength* Argument" em "Comentários".  
  
 Consulte [As informações de 64 bits do ODBC,](../../../odbc/reference/odbc-64-bit-information.md)se o aplicativo for executado em um sistema operacional de 64 bits.  
  
 *Strlen_or_indptr*  
 [Entrada diferida] Um ponteiro para um buffer para o comprimento do parâmetro. Para obter mais informações, consulte "*StrLen_or_IndPtr* Argument" em "Comentários".  
  
## <a name="returns"></a>Retornos

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos

 Quando **o SQLBindParameter** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados pelo **SQLBindParameter** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  

|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O tipo de dados identificado pelo argumento *ValueType* não pode ser convertido para o tipo de dados identificado pelo argumento *ParameterType.* Observe que esse erro pode ser retornado por **SQLExecDirect,** **SQLExecute**ou **SQLPutData** no momento da execução, em vez de por **SQLBindParameter**.|  
|07009|Índice de descritor inválido|(DM) O valor especificado para o número *de parâmetros de* argumento foi menor que 1.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no buffer **MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY003|Tipo de buffer de aplicativo inválido|O valor especificado pelo argumento *ValueType* não era um tipo de dados C válido ou SQL_C_DEFAULT.|  
|HY004|Tipo de dados SQL inválido|O valor especificado para o *argumente ParameterType* não era nem um identificador de tipo de dados ODBC SQL válido nem um identificador de tipo de dados SQL específico para o driver suportado pelo driver.|  
|HY009|Valor do argumento inválido|(DM) O argumento *ParameterValuePtr* era um ponteiro nulo, o argumento *StrLen_or_IndPtr* era um ponteiro nulo e o argumento *InputOutputType* não foi SQL_PARAM_OUTPUT.<br /><br /> (DM) SQL_PARAM_OUTPUT, onde o argumento *ParameterValuePtr* era um ponteiro nulo, o tipo C era char ou binário, e o BufferLength *(cbValueMax)* era maior que 0.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando **o SQLBindParameter** foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY021|Informações dedescritores inconsistentes|As informações do descritor verificadas durante uma verificação de consistência não foram consistentes. (Consulte a seção "Verificações de consistência" em **SQLSetDescField**.)<br /><br /> O valor especificado para o argumento *DecimalDigits* estava fora do intervalo de valores suportados pela fonte de dados para uma coluna do tipo de dados SQL especificado pelo argumento *ParameterType.*|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor em *BufferLength* foi inferior a 0. (Veja a descrição do campo SQL_DESC_DATA_PTR em **SQLSetDescField**.)|  
|HY104|Valor de precisão ou escala inválido|O valor especificado para o argumento *ColumnSize* ou *DecimalDigits* estava fora do intervalo de valores suportados pela fonte de dados para uma coluna do tipo de dados SQL especificada pelo argumento *ParameterType.*|  
|HY105|Tipo de parâmetro inválido|(DM) O valor especificado para o argumento *InputOutputType* era inválido. (Veja "Comentários".)|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suporta a conversão especificada pela combinação do valor especificado para o argumento *ValueType* e o valor específico do driver especificado para o *argumente ParameterType*.<br /><br /> O valor especificado para o *argumente ParameterType* foi um identificador de tipo de dados ODBC SQL válido para a versão do ODBC suportado pelo driver, mas não foi suportado pelo driver ou fonte de dados.<br /><br /> O driver suporta apenas ODBC 2. *x* e o argumento *ValueType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e todos os tipos de dados do intervalo C listados em [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) no apêndice D: Tipos de dados.<br /><br /> O driver só suporta versões ODBC antes de 3,50, e o argumento *ValueType* foi SQL_C_GUID.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários

 Um aplicativo chama **sqlBindParameter** para vincular cada marcador de parâmetro em uma declaração SQL. As vinculações permanecem em vigor até que o aplicativo chame **SQLBindParameter** novamente, chama **SQLFreeStmt** com a opção SQL_RESET_PARAMS ou chama **SQLSetDescField** para definir o campo de cabeçalho SQL_DESC_COUNT da APD como 0.  
  
 Para obter mais informações sobre parâmetros, consulte [Parâmetros de declaração](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre os tipos de dados dos parâmetros e marcadores de parâmetros, consulte Tipos de dados de [parâmetros](../../../odbc/reference/appendixes/parameter-data-types.md) e [marcadores de parâmetros](../../../odbc/reference/appendixes/parameter-markers.md) no apêndice C: Gramática SQL.  
  
## <a name="parameternumber-argument"></a>Argumento de número de parâmetros  
 Se o *número de parâmetros* na chamada para **SQLBindParameter** for maior do que o valor de SQL_DESC_COUNT, **o SQLSetDescField** é chamado para aumentar o valor de SQL_DESC_COUNT para *O Número de Parâmetros*.  
  
## <a name="inputoutputtype-argument"></a>Argumento do inputoutputtype  
 O argumento *InputOutputType* especifica o tipo do parâmetro. Este argumento define o campo SQL_DESC_PARAMETER_TYPE do IPD. Todos os parâmetros nas instruções SQL que não chamam procedimentos, como instruções **INSERT,** são *parâmetros de entrada**.* Os parâmetros nas chamadas de procedimento podem ser parâmetros de entrada, entrada/saída ou de saída. (Um aplicativo chama **SQLProcedureColumns** para determinar o tipo de parâmetro em uma chamada de procedimento; parâmetros cujo tipo não pode ser determinado são considerados parâmetros de entrada.)  
  
 O argumento *InputOutputType* é um dos seguintes valores:  
  
-   SQL_PARAM_INPUT. O parâmetro marca um parâmetro em uma instrução SQL que não chama um procedimento, como uma instrução **INSERT,** ou marca um parâmetro de entrada em um procedimento. Por exemplo, os parâmetros em **INSERT INTO Employee VALUES (?, ?, ?)** são parâmetros de entrada, enquanto os parâmetros em **{call AddEmp(?, ?, ?)}** podem ser, mas não necessariamente, parâmetros de entrada.  
  
     Quando a declaração é executada, o driver envia dados para o parâmetro para a fonte de dados; o \*buffer *ParameterValuePtr* deve conter um valor de entrada válido, ou o buffer ** StrLen_or_IndPtr* deve conter SQL_NULL_DATA, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC.  
  
     Se um aplicativo não puder determinar o tipo de parâmetro em uma chamada de procedimento, ele definirá *InputOutputType* como SQL_PARAM_INPUT; se a fonte de dados retornar um valor para o parâmetro, o driver o descarta.  
  
-   SQL_PARAM_INPUT_OUTPUT. O parâmetro marca um parâmetro de entrada/saída em um procedimento. Por exemplo, o parâmetro em **{call GetEmpDept(?)}** é um parâmetro de entrada/saída que aceita o nome de um funcionário e retorna o nome do departamento do funcionário.  
  
     Quando a declaração é executada, o driver envia dados para o parâmetro para a fonte de dados; o \*buffer *ParameterValuePtr* deve conter um \*valor de entrada válido, ou o buffer *de StrLen_or_IndPtr* deve conter SQL_NULL_DATA, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. Após a execução da declaração, o motorista retorna os dados do parâmetro para o aplicativo; se a fonte de dados não retornar um valor para um parâmetro de entrada/saída, o driver define o buffer ** StrLen_or_IndPtr* para SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Quando um aplicativo ODBC 1.0 chama **SQLSetParam** em um driver ODBC 2.0, o Gerenciador de driver converte isso em uma chamada para **SQLBindParameter** no qual o argumento *InputOutputType* é definido como SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. O parâmetro marca o valor de retorno de um procedimento ou um parâmetro de saída em um procedimento; em ambos os casos, estes são conhecidos como *parâmetros de saída*. Por exemplo, o parâmetro em **{?=chamada GetNextEmpID}** é um parâmetro de saída que retorna o próximo ID do funcionário.  
  
     Após a execução da declaração, o driver retorna os dados do parâmetro para o aplicativo, a menos que os argumentos *ParameterValuePtr* e *StrLen_or_IndPtr* sejam ambos ponteiros nulos, nesse caso o driver descarta o valor de saída. Se a fonte de dados não retornar um valor para um parâmetro de saída, o driver definirá o buffer ** StrLen_or_IndPtr* para SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica que um parâmetro de entrada/saída deve ser transmitido. **SQLGetData** pode ler valores de parâmetros em partes. *BufferLength* é ignorado porque o comprimento do buffer será determinado na chamada do **SQLGetData**. O valor do tampão *StrLen_or_IndPtr* deve conter SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. Um parâmetro deve ser vinculado como um parâmetro dada-at-execution (DAE) na entrada se for transmitido na saída. *ParameterValuePtr* pode ser qualquer valor de ponteiro não nulo que será devolvido pelo **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr* para entrada e saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. O mesmo que SQL_PARAM_INPUT_OUTPUT_STREAM, para um parâmetro de saída. **StrLen_or_IndPtr* é ignorado na entrada.  
  
 A tabela a seguir lista diferentes combinações de *InputOutputType* e **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**Strlen_or_indptr*|Resultado|Observação sobre ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC*ou*SQL_DATA_AT_EXEC|Entrada em peças|*ParameterValuePtr* pode ser qualquer valor de ponteiro que será devolvido pelo **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Não SQL_LEN_DATA_AT_EXEC*ou*SQL_DATA_AT_EXEC|Buffer vinculado à entrada|*ParâmetroValuePtr* é o endereço do buffer de entrada.|  
|SQL_PARAM_OUTPUT|Ignorado na entrada.|Buffer vinculado à saída|*ParâmetroValuePtr* é o endereço do buffer de saída.|  
|SQL_PARAM_OUTPUT_STREAM|Ignorado na entrada.|Saída transmitida|*ParameterValuePtr* pode ser qualquer valor de ponteiro, que será devolvido pelo **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC*ou*SQL_DATA_AT_EXEC|Entrada em peças e tampão de saída bound|*ParameterValuePtr* é o endereço do buffer de saída, que também será devolvido pelo **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|Não SQL_LEN_DATA_AT_EXEC*ou*SQL_DATA_AT_EXEC|Buffer vinculado à entrada e buffer de saída bound|*ParameterValuePtr* é o endereço do buffer de entrada/saída compartilhado.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC*ou*SQL_DATA_AT_EXEC|Entrada em peças e saída streamed|*ParameterValuePtr* pode ser qualquer valor de ponteiro não nulo, que será devolvido pelo **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr* para entrada e saída.|  
  
> [!NOTE]  
>  O driver deve decidir quais tipos de SQL são permitidos quando um aplicativo vincula um parâmetro de saída ou saída de entrada como transmitido. O gerenciador de driver não gerará um erro para um tipo SQL inválido.  
  
## <a name="valuetype-argument"></a>Argumento valueType

 O argumento *ValueType* especifica o tipo de dados C do parâmetro. Este argumento define os campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE da APD. Este deve ser um dos valores na seção [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) do Apêndice D: Tipos de Dados.  
  
 Se o argumento *ValueType* for um dos tipos de dados de intervalo, o campo SQL_DESC_TYPE do registro Número de *parâmetros* da APD será definido como SQL_INTERVAL, o campo SQL_DESC_CONCISE_TYPE da APD será definido para o tipo de dados de intervalo conciso e o campo SQL_DESC_DATETIME_INTERVAL_CODE do registro Número de *parâmetros* é definido como um subcódigo para o tipo de dados de intervalo específico. (Veja [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).) A precisão de nível de intervalo padrão (2) e a precisão dos segundos de intervalo padrão (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION da APD, respectivamente, são usadas para os dados. Se a precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o argumento *ValueType* for um dos tipos de dados de data-hora, o campo SQL_DESC_TYPE do registro Número de *parâmetros* da APD será definido como SQL_DATETIME, o campo SQL_DESC_CONCISE_TYPE do registro Número de *parâmetros* da APD será definido para o tipo de dados C de data c concisa e o campo SQL_DESC_DATETIME_INTERVAL_CODE do registro Número de *parâmetros* é definido como um subcódigo para o tipo de dados de data específica. (Veja [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Se o argumento *ValueType* for um SQL_C_NUMERIC tipo de dados, a precisão padrão (que é definida pelo driver) e a escala padrão (0), definida nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE da APD, serão usadas para os dados. Se a precisão ou escala padrão não for apropriada, o aplicativo deve definir explicitamente o campo descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 SQL_C_DEFAULT especifica que o valor do parâmetro seja transferido do tipo de dados C padrão para o tipo de dados SQL especificado com *ParameterType*.  
  
 Você também pode especificar um tipo de dados C estendido. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Para obter mais informações, consulte [Tipos de dados C padrão,](../../../odbc/reference/appendixes/default-c-data-types.md) [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)e [convertendo dados de SQL para C Tipos de dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no apêndice D: Tipos de dados.  
  
## <a name="parametertype-argument"></a>Argumento do tipo de parâmetro

 Este deve ser um dos valores listados na seção [SQL Data Types](../../../odbc/reference/appendixes/sql-data-types.md) do Apêndice D: Data Types, ou deve ser um valor específico do driver. Esse argumento define os campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE do IPD.  
  
 Se o argumento *ParameterType* for um dos identificadores de data-hora, o campo SQL_DESC_TYPE do IPD será definido como SQL_DATETIME, o campo SQL_DESC_CONCISE_TYPE do IPD será definido para o tipo de dados SQL data-hora concisa e o campo de SQL_DESC_DATETIME_INTERVAL_CODE é definido para o valor de subcódigo de data ção apropriado.  
  
 Se *ParameterType* for um dos identificadores de intervalo, o campo SQL_DESC_TYPE do IPD é definido como SQL_INTERVAL, o campo SQL_DESC_CONCISE_TYPE do IPD é definido para o tipo de dados de intervalo SQL conciso e o campo SQL_DESC_DATETIME_INTERVAL_CODE do IPD é definido para o subcódigo de intervalo apropriado. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION do IPD é definido para a precisão de liderança de intervalo, e o campo de SQL_DESC_PRECISION é definido para a precisão de segundos de intervalo, se aplicável. Se o valor padrão de SQL_DESC_DATETIME_INTERVAL_PRECISION ou SQL_DESC_PRECISION não for apropriado, o aplicativo deve defini-lo explicitamente ligando para **SQLSetDescField**. Para obter mais informações sobre qualquer um desses campos, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Se o argumento *ValueType* for um SQL_NUMERIC tipo de dados, a precisão padrão (que é definida pelo driver) e a escala padrão (0), definida nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do IPD, serão usadas para os dados. Se a precisão ou escala padrão não for apropriada, o aplicativo deve definir explicitamente o campo descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Para obter informações sobre como os dados são convertidos, consulte [Conversão de dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) e [Conversão de Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice D: Tipos de dados.  
  
## <a name="columnsize-argument"></a>Argumento do Tamanho da Coluna

 O argumento *ColumnSize* especifica o tamanho da coluna ou expressão que corresponde ao marcador de parâmetro, o comprimento desses dados ou ambos. Este argumento define diferentes campos do IPD, dependendo do tipo de dados SQL (o argumento *ParameterType).* As seguintes regras se aplicam a este mapeamento:  
  
-   Se *O ParameterType* for SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um dos tipos de dados de data ou intervalo de SQL concisos, o campo SQL_DESC_LENGTH do IPD será definido como o valor de *ColumnSize*. (Para obter mais informações, consulte a seção Tamanho da [coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.)  
  
-   Se *O ParâmetroType* for SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE, o campo SQL_DESC_PRECISION do IPD será definido como o valor de *ColumnSize*.  
  
-   Para outros tipos de dados, o argumento *ColumnSize* é ignorado.  
  
 Para obter mais informações, consulte "Valores de parâmetro de passagem" e SQL_DATA_AT_EXEC em "*StrLen_or_IndPtr* Argument".  
  
## <a name="decimaldigits-argument"></a>Argumento DecimalDigits

 Se *O ParameterType* for SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND ou SQL_INTERVAL_MINUTE_TO_SECOND, o campo SQL_DESC_PRECISION do IPD será definido como *DecimalDigits*. Se *O ParameterType* for SQL_NUMERIC ou SQL_DECIMAL, o campo SQL_DESC_SCALE do IPD será definido *como DecimalDigits*. Para todos os outros tipos de dados, o argumento *DecimalDigits* é ignorado.  
  
## <a name="parametervalueptr-argument"></a>Argumento parameterValuePtr

 O argumento *ParameterValuePtr* aponta para um buffer que, quando **sQLExecute** ou **SQLExecDirect** é chamado, contém os dados reais para o parâmetro. Os dados devem estar no formulário especificado pelo argumento *ValueType.* Este argumento define o campo SQL_DESC_DATA_PTR da APD. Um aplicativo pode definir o argumento *ParameterValuePtr* como * \** um ponteiro nulo, desde que StrLen_or_IndPtr seja SQL_NULL_DATA ou SQL_DATA_AT_EXEC. (Isso se aplica apenas aos parâmetros de entrada ou entrada/saída.)  
  
 Se \* *StrLen_or_IndPtr* for o resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento)* ou SQL_DATA_AT_EXEC, então *O ParâmetroValuePtr* é um valor de ponteiro definido por aplicativo que está associado ao parâmetro. Ele é devolvido ao aplicativo através **do SQLParamData**. Por exemplo, *O ParameterValuePtr* pode ser um token não-zero, como um número de parâmetro, um ponteiro para dados ou um ponteiro para uma estrutura que o aplicativo usou para vincular parâmetros de entrada. No entanto, observe que se o parâmetro for um parâmetro de entrada/saída, *o ParameterValuePtr* deve ser um ponteiro para um buffer onde o valor de saída será armazenado. Se o valor no atributo de declaração SQL_ATTR_PARAMSET_SIZE for maior que 1, o aplicativo poderá usar o valor apontado pelo atributo de declaração SQL_ATTR_PARAMS_PROCESSED_PTR juntamente com o argumento *ParameterValuePtr.* Por exemplo, *ParameterValuePtr* pode apontar para uma matriz de valores e o aplicativo pode usar o valor apontado por SQL_ATTR_PARAMS_PROCESSED_PTR para recuperar o valor correto da matriz. Para obter mais informações, consulte "Valores de parâmetro de passagem" mais tarde nesta seção.  
  
 Se o argumento *InputOutputType* for SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT, *ParameterValuePtr* será um buffer no qual o driver retorna o valor de saída. Se o procedimento retornar um ou \*mais conjuntos de resultados, o buffer *ParameterValuePtr* não será garantido até que todas as séries de resultados/contagem de linhas tenham sido processadas. Se o buffer não estiver definido até que o processamento esteja concluído, os parâmetros de saída e os valores de retorno não estarão disponíveis até **que o SQLMoreResults** retorne SQL_NO_DATA. Chamar **sqlCloseCursor ou** **SQLFreeStmt** com uma opção de SQL_CLOSE fará com que esses valores sejam descartados.  
  
 Se o valor no atributo de declaração SQL_ATTR_PARAMSET_SIZE for maior que 1, *ParameterValuePtr* será um array. Uma única declaração SQL processa o conjunto completo de valores de entrada para um parâmetro de entrada ou entrada/saída e retorna uma matriz de valores de saída para um parâmetro de entrada/saída ou de saída.  
  
## <a name="bufferlength-argument"></a>Argumento bufferLength

 Para dados de caracteres e c binários, \*o argumento *BufferLength* especifica o comprimento do buffer *ParameterValuePtr* (se for um único elemento) ou o comprimento de um elemento na \*matriz *ParameterValuePtr* (se o valor no atributo de declaração SQL_ATTR_PARAMSET_SIZE for maior que 1). Este argumento define o campo de registro SQL_DESC_OCTET_LENGTH da APD. Se o aplicativo especificar vários valores, *BufferLength* será usado para determinar a localização dos valores na matriz **ParameterValuePtr,* tanto na entrada quanto na saída. Para parâmetros de entrada/saída e saída, ele é usado para determinar se deve truncar dados de caracteres e C binários na saída:  
  
-   Para dados do caractere C, se o número de bytes disponíveis para \*retornar for maior ou igual a *BufferLength,* os dados em *ParameterValuePtr* são truncados para *BufferLength* menos o comprimento de um caractere de rescisão nula e são nulos pelo driver.  
  
-   Para dados c binários, se o número de bytes disponíveis \*para retornar for maior que *BufferLength,* os dados em *ParameterValuePtr* são truncados em *bytes BufferLength.*  
  
 Para todos os outros tipos de dados C, o argumento *BufferLength* é ignorado. O comprimento \*do buffer *ParameterValuePtr* (se for um único elemento) \*ou o comprimento de um elemento na matriz *ParameterValuePtr* (se o aplicativo chamar **SQLSetStmtAttr** com um argumento *de atributo* de SQL_ATTR_PARAMSET_SIZE especificar múltiplos valores para cada parâmetro) é assumido como o comprimento do tipo de dados C.  
  
 Para parâmetros de saída/saída em fluxo ou de saída em fluxo, o argumento *BufferLength* é ignorado porque o comprimento do buffer é especificado no **SQLGetData**.  
  
> [!NOTE]  
>  Quando um aplicativo ODBC 1.0 chama **SQLSetParam** em um ODBC 3. *x* driver, o Gerenciador de driver converte isso em uma chamada para **SQLBindParameter** no qual o argumento *BufferLength* é sempre SQL_SETPARAM_VALUE_MAX. Porque o Gerenciador de driver retorna um erro se um ODBC 3. *x* o aplicativo define *BufferLength* para SQL_SETPARAM_VALUE_MAX, um ODBC 3. *x* driver pode usar isso para determinar quando ele é chamado por um aplicativo ODBC 1.0.  
  
> [!NOTE]  
>  Em **SQLSetParam,** a maneira pela qual um aplicativo especifica o comprimento do buffer **ParameterValuePtr* para que o driver possa retornar dados de caracteres ou binários, e a maneira como um aplicativo envia um conjunto de valores de caracteres ou parâmetros binários para o motorista, são definidos pelo driver.  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr argumento

 O *argumento StrLen_or_IndPtr* aponta para um buffer que, quando **sQLExecute** ou **SQLExecDirect** é chamado, contém um dos seguintes. (Este argumento define os campos de registro SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR dos ponteiros do parâmetro de aplicação.)  
  
-   O comprimento do valor do parâmetro armazenado em **ParameterValuePtr*. Isso é ignorado, exceto por dados de caracteres ou c binários.  
  
-   SQL_NTS. O valor do parâmetro é uma seqüência de seqüência sumida.  
  
-   Sql_null_data. O valor do parâmetro é NULL.  
  
-   Sql_default_param. Um procedimento é usar o valor padrão de um parâmetro, em vez de um valor recuperado do aplicativo. Esse valor é válido apenas em um procedimento chamado de sintaxe canônica ODBC e, em seguida, somente se o argumento *InputOutputType* for SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_INPUT_OUTPUT_STREAM. Quando \* *StrLen_or_IndPtr* é SQL_DEFAULT_PARAM, os argumentos *ValueType*, *ParameterType,* *ColumnSize,* *DecimalDigits,* *BufferLength*e *ParameterValuePtr* são ignorados para parâmetros de entrada e são usados apenas para definir o valor do parâmetro de saída para parâmetros de entrada/saída.  
  
-   O resultado da macro*SQL_LEN_DATA_AT_EXEC(comprimento).* Os dados do parâmetro serão enviados com **SQLPutData**. Se o argumento *ParameterType* for SQL_LONGVARBINARY, SQL_LONGVARCHAR ou um longo tipo de dados específicos da fonte de dados, e o driver retornar "Y" para o SQL_NEED_LONG_DATA_LEN tipo de informação no **SQLGetInfo,** *o comprimento* é o número de bytes de dados a serem enviados para o parâmetro; caso contrário, *o comprimento* deve ser um valor não negativo e é ignorado. Para obter mais informações, consulte "Valores de parâmetro de passagem", mais tarde nesta seção.  
  
     Por exemplo, para especificar que 10.000 bytes de dados serão enviados com **SQLPutData** em uma ou mais chamadas, para um parâmetro de SQL_LONGVARCHAR, um conjunto de aplicativos **StrLen_or_IndPtr* a SQL_LEN_DATA_AT_EXEC(10000).  
  
-   SQL_DATA_AT_EXEC. Os dados do parâmetro serão enviados com **SQLPutData**. Este valor é usado por aplicativos ODBC 1.0 quando eles chamam o ODBC 3. *x* drivers. Para obter mais informações, consulte "Valores de parâmetro de passagem", mais tarde nesta seção.  
  
 Se *StrLen_or_IndPtr* for um ponteiro nulo, o driver assumirá que todos os valores dos parâmetros de entrada não são NUCTOS e que os dados de caracteres e binários são nulos. Se *InputOutputType* for SQL_PARAM_OUTPUT ou SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* e *StrLen_or_IndPtr* forem ponteiros nulos, o driver descartará o valor de saída.  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos estão fortemente desencorajados de especificar um ponteiro nulo para *StrLen_or_IndPtr* quando o tipo de dados do parâmetro é SQL_C_BINARY. Para garantir que um driver não trunque dados SQL_C_BINARY inesperadamente, *StrLen_or_IndPtr* deve conter um ponteiro para um valor de comprimento válido.  
  
 Se o argumento *InputOutputType* for SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* aponta para um buffer no qual \*o driver retorna SQL_NULL_DATA, o número de bytes disponíveis para retornar no *ParameterValuePtr* (excluindo o byte de rescisão nula dos dados de caracteres) ou SQL_NO_TOTAL (se o número de bytes disponíveis para retornar não puder ser determinado). Se o procedimento retornar um ou mais conjuntos de resultados, o tampão*de StrLen_or_IndPtr* * não é garantido para ser definido até que todos os resultados tenham sido obtidos.  
  
 Se o valor no atributo de declaração SQL_ATTR_PARAMSET_SIZE for maior que 1, *StrLen_or_IndPtr* aponta para uma matriz de valores SQLLEN. Estes podem ser qualquer um dos valores listados anteriormente nesta seção e são processados com uma única declaração SQL.  
  
## <a name="passing-parameter-values"></a>Valores dos parâmetros de passagem

 Um aplicativo pode passar o valor para \*um parâmetro no buffer *ParameterValuePtr* ou com uma ou mais chamadas para **SQLPutData**. Parâmetros cujos dados são passados com **SQLPutData** são conhecidos como parâmetros *de data-at-execution.* Estes são normalmente usados para enviar dados para parâmetros SQL_LONGVARBINARY e SQL_LONGVARCHAR, e podem ser misturados com outros parâmetros.  
  
 Para passar valores de parâmetro, um aplicativo executa a seguinte seqüência de etapas:  
  
1.  Chama **SQLBindParameter** para cada parâmetro para vincular buffers para o valor do parâmetro (argumento*ParameterValuePtr)* e comprimento/indicador *(argumento StrLen_or_IndPtr).* Para parâmetros de data-at-execution, *ParameterValuePtr* é um valor de ponteiro definido por aplicativo, como um número de parâmetro ou um ponteiro para dados. O valor será devolvido posteriormente e poderá ser usado para identificar o parâmetro.  
  
2.  Coloca valores para parâmetros de \*entrada e entrada/saída nos buffers *ParameterValuePtr* e ** StrLen_or_IndPtr:*  
  
    -   Para parâmetros normais, a aplicação coloca \*o valor do parâmetro no buffer *ParameterValuePtr* e o comprimento desse valor no buffer ** StrLen_or_IndPtr.* Para obter mais informações, consulte [Definir valores de parâmetro](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Para parâmetros de data-at-execution, o aplicativo coloca o resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento)*(ao chamar um driver ODBC 2.0) no buffer ** StrLen_or_IndPtr.*  
  
3.  Chama **SQLExecute** ou **SQLExecDirect** para executar a declaração SQL.  
  
    -   Se não houver parâmetros de execução de dados, o processo será concluído.  
  
    -   Se houver parâmetros de data-at-execution, a função retorna SQL_NEED_DATA.  
  
4.  Chama **SQLParamData** para recuperar o valor definido pelo aplicativo especificado no argumento *ParameterValuePtr* do **SQLBindParameter** para que o primeiro parâmetro de dados em execução seja processado. **SQLParamData** retorna SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Embora os parâmetros de data-at-execution se assemelham às colunas de dados em execução, o valor retornado pelo **SQLParamData** é diferente para cada um. Os parâmetros de data-at-execution são parâmetros em uma declaração SQL para a qual os dados serão enviados com **sQLPutData** quando a declaração for executada com **SQLExecDirect** ou **SQLExecute**. Eles estão vinculados ao **SQLBindParameter**. O valor retornado por **SQLParamData** é um valor de ponteiro passado para **SQLBindParameter** no argumento *ParameterValuePtr.* As colunas de dados em execução são colunas em um conjunto de linhas para os quais os dados serão enviados com **o SQLPutData** quando uma linha é atualizada ou adicionada com **SQLBulkOperations** ou atualizada com **SQLSetPos**. Eles estão ligados ao **SQLBindCol**. O valor retornado pelo **SQLParamData** é o endereço da linha no buffer ** TargetValuePtr* (definido por uma chamada para **SQLBindCol**) que está sendo processado.  
  
5.  Chama **sqlPutData** uma ou mais vezes para enviar dados para o parâmetro. Mais de uma chamada é necessária se \*o valor de dados for maior do que o buffer *ParameterValuePtr* especificado no **SQLPutData;** várias chamadas para **SQLPutData** para o mesmo parâmetro são permitidas apenas ao enviar dados c de caracteres para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados ou ao enviar dados c binários para uma coluna com um tipo de dados específico de origem de caracteres, binários ou de origem de dados.  
  
6.  Chama **sqlParamData** novamente para sinalizar que todos os dados foram enviados para o parâmetro.  
  
    -   Se houver mais parâmetros de data-at-execution, **o SQLParamData** retorna SQL_NEED_DATA e o valor definido pelo aplicativo para o próximo parâmetro de dados em execução a ser processado. O aplicativo repete as etapas 4 e 5.  
  
    -   Se não houver mais parâmetros de data-at-execution, o processo será concluído. Se a declaração foi executada com sucesso, **o SQLParamData** reatornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ela retorna SQL_ERROR. Neste ponto, **o SQLParamData** pode retornar qualquer SQLSTATE que possa ser devolvido pela função usada para executar a declaração **(SQLExecDirect** ou **SQLExecute).**  
  
         Os valores de saída para quaisquer parâmetros de entrada/saída ou de saída estão disponíveis nos \*buffers *ParameterValuePtr* e **StrLen_or_IndPtr* após o aplicativo recuperar todos os conjuntos de resultados gerados pela declaração.  
  
 Chamar **SQLExecute** ou **SQLExecDirect** coloca a declaração em um estado SQL_NEED_DATA. Neste ponto, o aplicativo pode chamar apenas **SQLCancel,** **SQLGetDiagField,** **SQLGetDiagRec,** **SQLGetFunctions,** **SQLParamData**ou **SQLPutData** com a declaração ou o *cabo de conexão* associado à declaração. Se ele chamar qualquer outra função com a declaração ou a conexão associada à declaração, a função retorna SQLSTATE HY010 (erro de seqüência de função). A declaração deixa o estado SQL_NEED_DATA quando **SQLParamData** ou **SQLPutData** retornar um erro, **o SQLParamData** retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO ou a declaração for cancelada.  
  
 Se o aplicativo chamar **o SQLCancel** enquanto o driver ainda precisar de dados para parâmetros de data-at-execution, o driver cancelará a execução da declaração; o aplicativo pode então chamar **SQLExecute** ou **SQLExecDirect** novamente.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída em fluxo

 Quando um aplicativo define *InputOutputType* para SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, o valor do parâmetro de saída deve ser recuperado por uma ou mais chamadas para **SQLGetData**. Quando o driver tiver um valor de parâmetro de saída transmitido para retornar ao aplicativo, ele retornará SQL_PARAM_DATA_AVAILABLE em resposta a uma chamada para as seguintes funções: **SQLMoreResults,** **SQLExecute**e **SQLExecDirect**. Um aplicativo chama **SQLParamData** para determinar qual valor de parâmetro está disponível.  
  
 Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída transmitidos, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Usar matrizes de parâmetros

 Quando um aplicativo prepara uma declaração com marcadores de parâmetros e passa em uma matriz de parâmetros, há duas maneiras diferentes de ser executada. Uma maneira é o driver confiar nas capacidades de processamento de matriz do back-end, nesse caso toda a declaração com o conjunto de parâmetros é tratada como uma unidade atômica. O Oracle é um exemplo de uma fonte de dados que suporta recursos de processamento de array. Outra maneira de implementar esse recurso é que o driver gere um lote de instruções SQL, uma instrução SQL para cada conjunto de parâmetros no array de parâmetros e execute o lote. Os arrays de parâmetros não podem ser usados com uma **atualização onde a corrente da** declaração.  
  
 Quando um conjunto de parâmetros é processado, conjuntos de resultados individuais/contagem de linhas (um para cada conjunto de parâmetros) podem estar disponíveis ou as contagens de conjuntos/linhas de resultados podem ser enroladas em uma. A opção SQL_PARAM_ARRAY_ROW_COUNTS no **SQLGetInfo** indica se as contagens de linha estão disponíveis para cada conjunto de parâmetros (SQL_PARC_BATCH) ou apenas uma contagem de linhas está disponível (SQL_PARC_NO_BATCH).  
  
 A opção SQL_PARAM_ARRAY_SELECTS no **SQLGetInfo** indica se um conjunto de resultados está disponível para cada conjunto de parâmetros (SQL_PAS_BATCH) ou apenas um conjunto de resultados está disponível (SQL_PAS_NO_BATCH). Se o driver não permitir que uma declaração de geração de resultados seja executada com uma matriz de parâmetros, SQL_PARAM_ARRAY_SELECTS retorna SQL_PAS_NO_SELECT.  
  
 Para obter mais informações, consulte [SQLGetInfo Function](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Para suportar matrizes de parâmetros, o atributo de declaração SQL_ATTR_PARAMSET_SIZE é definido para especificar o número de valores para cada parâmetro. Se o campo for maior que 1, os campos de SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR da APD devem apontar para matrizes. A cardinalidade de cada matriz é igual ao valor de SQL_ATTR_PARAMSET_SIZE.  
  
 O campo SQL_DESC_ROWS_PROCESSED_PTR da APD aponta para um buffer que contém o número de conjuntos de parâmetros que foram processados, incluindo conjuntos de erros. À medida que cada conjunto de parâmetros é processado, o driver armazena um novo valor no buffer. Nenhum número será devolvido se este for um ponteiro nulo. Quando os arrays de parâmetros são usados, o valor apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR da APD é preenchido mesmo que SQL_ERROR seja devolvido pela função de configuração. Se SQL_NEED_DATA for devolvido, o valor apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR da APD é definido para o conjunto de parâmetros que está sendo processado.  
  
 O que ocorre quando uma matriz de parâmetros é vinculada e uma **atualização onde a declaração ATUAL da** declaração é executada é definida pelo driver.  
  
## <a name="column-wise-parameter-binding"></a>Vinculação do parâmetro column-wise

 Na vinculação em termos de coluna, o aplicativo vincula os parâmetros separados e as matrizes de comprimento/indicador a cada parâmetro.  
  
 Para usar a vinculação em termos de coluna, o aplicativo define primeiro o atributo de declaração SQL_ATTR_PARAM_BIND_TYPE a SQL_PARAM_BIND_BY_COLUMN. (Este é o padrão.) Para cada coluna ser vinculada, o aplicativo executa as seguintes etapas:  
  
1.  Aloca uma matriz de buffer de parâmetros.  
  
2.  Aloca uma matriz de buffers de comprimento/indicador.  
  
    > [!NOTE]  
    >  Se o aplicativo for escrito diretamente aos descritores quando a vinculação em termos de coluna for usada, matrizes separadas poderão ser usadas para dados de comprimento e indicador.  
  
3.  Chama **sqlBindParameter** com os seguintes argumentos:  
  
    -   *ValueType* é o tipo C de um único elemento na matriz de buffer de parâmetros.  
  
    -   *ParameterType* é o tipo SQL do parâmetro.  
  
    -   *ParâmetroValuePtr* é o endereço do conjunto de buffer de parâmetros.  
  
    -   *BufferLength* é o tamanho de um único elemento na matriz de buffer de parâmetros. O argumento *BufferLength* é ignorado quando os dados são dados de comprimento fixo.  
  
    -   *StrLen_or_IndPtr* é o endereço da matriz comprimento/indicador.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "Argumento ParameterValuePtr" em "Comentários", mais tarde nesta seção. Para obter mais informações sobre a vinculação de parâmetros em termos de coluna, consulte [Matrizes de vinculação de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>Encadernação do parâmetro row-wise

 Em vinculação em termos de linha, o aplicativo define uma estrutura que contém parâmetros e buffers de comprimento/indicador para cada parâmetro a ser vinculado.  
  
 Para usar a vinculação em termos de linha, o aplicativo executa as seguintes etapas:  
  
1.  Define uma estrutura para manter um único conjunto de parâmetros (incluindo parâmetros e buffers de comprimento/indicador) e aloca uma matriz dessas estruturas.  
  
    > [!NOTE]  
    >  Se o aplicativo for escrito diretamente aos descritores quando a vinculação em termos de linha for usada, campos separados poderão ser usados para dados de comprimento e indicador.  
  
2.  Define o atributo de declaração SQL_ATTR_PARAM_BIND_TYPE ao tamanho da estrutura que contém um único conjunto de parâmetros ou ao tamanho de uma instância de um buffer no qual os parâmetros serão vinculados. O comprimento deve incluir espaço para todos os parâmetros encadernados, e qualquer preenchimento da estrutura ou tampão, para garantir que quando o endereço de um parâmetro bound for incrementado com o comprimento especificado, o resultado apontará para o início do mesmo parâmetro na próxima linha. Quando você usa o *tamanho do operador* no ANSI C, esse comportamento é garantido.  
  
3.  Chama **sqlBindParameter** com os seguintes argumentos para que cada parâmetro seja vinculado:  
  
    -   *ValueType* é o tipo de membro tampão de parâmetro a ser vinculado à coluna.  
  
    -   *ParameterType* é o tipo SQL do parâmetro.  
  
    -   *ParâmetroValuePtr* é o endereço do membro buffer de parâmetro no primeiro elemento de matriz.  
  
    -   *BufferLength* é o tamanho do membro tampão de parâmetros.  
  
    -   *StrLen_or_IndPtr* é o endereço do membro de comprimento/indicador a ser vinculado.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "*ParameterValuePtr* Argument", mais tarde nesta seção. Para obter mais informações sobre a vinculação em termos de linha de parâmetros, consulte os [Arrays of Parameters de vinculação](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Informações sobre erros

 Se um driver não implementar matrizes de parâmetros como lotes (a opção SQL_PARAM_ARRAY_ROW_COUNTS é igual a SQL_PARC_NO_BATCH), as situações de erro são tratadas como se uma declaração fosse executada. Se o driver implementar matrizes de parâmetros como lotes, um aplicativo pode usar o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR do IPD para determinar qual parâmetro de uma declaração SQL ou qual parâmetro em uma matriz de parâmetros fez com que **SQLExecDirect** ou **SQLExecute** retornassem um erro. Este campo contém informações de status para cada linha de valores de parâmetros. Se o campo indicar que ocorreu um erro, os campos na estrutura de dados diagnósticos indicarão o número de linha e parâmetro do parâmetro que falhou. O número de elementos na matriz será definido pelo campo de cabeçalho SQL_DESC_ARRAY_SIZE na APD, que pode ser definido pelo atributo de declaração SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  O campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR na APD é usado para ignorar parâmetros. Para obter mais informações sobre ignorar parâmetros, consulte a próxima seção, "Ignorando um conjunto de parâmetros".  
  
 Quando **o SQLExecute** ou **o SQLExecDirect** retornarem SQL_ERROR, os elementos na matriz apontados pelo campo SQL_DESC_ARRAY_STATUS_PTR no IPD conterão SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED ou SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Para cada elemento nesta matriz, a estrutura de dados de diagnóstico contém um ou mais registros de status. O SQL_DIAG_ROW_NUMBER campo da estrutura indica o número da linha dos valores dos parâmetros que causaram o erro. Se for possível determinar o parâmetro particular em uma linha de parâmetros que causaram o erro, o número de parâmetroserá inserido no campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED é inserida quando um parâmetro não foi usado porque ocorreu um erro em um parâmetro anterior que forçou **o SQLExecute** ou **o SQLExecDirect** a abortar. Por exemplo, se houver 50 parâmetros e ocorrer um erro durante a execução do conjunto de parâmetros que fez com que **o SQLExecute** ou **o SQLExecDirect** abortassem, então SQL_PARAM_UNUSED é inserida na matriz de status para os parâmetros 41 a 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE é inserida quando o driver trata matrizes de parâmetros como uma unidade monolítica, de modo que não gera esse nível de parâmetro individual de informações de erro.  
  
 Alguns erros no processamento de um único conjunto de parâmetros causam o processamento dos conjuntos subseqüentes de parâmetros na matriz para parar. Outros erros não afetam o processamento dos parâmetros subseqüentes. Quais erros pararão o processamento é definido pelo driver. Se o processamento não for interrompido, todos os parâmetros do array serão processados, SQL_SUCCESS_WITH_INFO é devolvido como resultado do erro, e o buffer definido por SQL_ATTR_PARAMS_PROCESSED_PTR é definido para o número total de conjuntos de parâmetros processados (conforme definido pelo atributo de declaração SQL_ATTR_PARAMSET_SIZE), que inclui conjuntos de erros.  
  
> [!CAUTION]  
>  O comportamento oDBC quando ocorre um erro no processamento de um conjunto de parâmetros é diferente no ODBC 3. *x* do que era em ODBC 2. *x*. Em ODBC 2. *x*, a função retornou SQL_ERROR e o processamento cessou. O buffer apontado pelo argumento *pirow* do **SQLParamOptions** continha o número da linha de erro. Em ODBC 3. *x*, a função retorna SQL_SUCCESS_WITH_INFO e o processamento pode parar ou continuar. Se continuar, o buffer especificado por SQL_ATTR_PARAMS_PROCESSED_PTR será definido como o valor de todos os parâmetros processados, incluindo aqueles que resultaram em um erro. Essa mudança de comportamento pode causar problemas para os aplicativos existentes.  
  
 Quando **sQLExecute** ou **SQLExecDirect** retorna antes de concluir o processamento de todos os conjuntos de parâmetros em uma matriz de parâmetros, como quando SQL_ERROR ou SQL_NEED_DATA é retornado, a matriz de status contém status para os parâmetros que já foram processados. A localização apontada pelo campo SQL_DESC_ROWS_PROCESSED_PTR no IPD contém o número da linha na matriz de parâmetros que causou o código de erro SQL_ERROR ou SQL_NEED_DATA. Quando um conjunto de parâmetros é enviado para uma declaração SELECT, a disponibilidade de valores de matriz de status é definida pelo driver; eles podem estar disponíveis depois que a declaração for executada ou como conjuntos de resultados são buscados.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorando um conjunto de parâmetros

 O campo SQL_DESC_ARRAY_STATUS_PTR da APD (conforme definido pelo atributo de declaração SQL_ATTR_PARAM_STATUS_PTR) pode ser usado para indicar que um conjunto de parâmetros vinculados em uma declaração SQL deve ser ignorado. Para orientar o driver a ignorar um ou mais conjuntos de parâmetros durante a execução, um aplicativo deve seguir estas etapas:  
  
1.  Ligue para **sqlsetdescField** para definir o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR da APD para apontar para uma matriz de valores SQLUSMALLINT para conter informações de status. Este campo também pode ser definido chamando **SQLSetStmtAttr** com um *Atributo* de SQL_ATTR_PARAM_OPERATION_PTR, que permite que um aplicativo defina o campo sem obter uma alça descritor.  
  
2.  Defina cada elemento da matriz definido pelo campo SQL_DESC_ARRAY_STATUS_PTR da APD como um dos dois valores:  
  
    -   SQL_PARAM_IGNORE, para indicar que a linha está excluída da execução da declaração.  
  
    -   SQL_PARAM_PROCEED, para indicar que a linha está incluída na execução da declaração.  
  
3.  Ligue para **SQLExecDirect** ou **SQLExecute** para executar a declaração preparada.  
  
 As seguintes regras se aplicam à matriz definida pelo campo SQL_DESC_ARRAY_STATUS_PTR da APD:  
  
-   O ponteiro está definido como nulo por padrão.  
  
-   Se o ponteiro for nulo, todos os conjuntos de parâmetros serão usados, como se todos os elementos fossem definidos para SQL_ROW_PROCEED.  
  
-   Definir um elemento para SQL_PARAM_PROCEED não garante que a operação use esse conjunto específico de parâmetros.  
  
-   SQL_PARAM_PROCEED é definido como 0 no arquivo de cabeçalho.  
  
 Um aplicativo pode definir o campo SQL_DESC_ARRAY_STATUS_PTR no APD para apontar para o mesmo conjunto que o apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR no IRD. Isso é útil quando vincula parâmetros aos dados de linha. Os parâmetros podem então ser ignorados de acordo com o status dos dados da linha. Além de SQL_PARAM_IGNORE, os seguintes códigos fazem com que um parâmetro em uma declaração SQL seja ignorado: SQL_ROW_DELETED, SQL_ROW_UPDATED e SQL_ROW_ERROR. Além de SQL_PARAM_PROCEED, os seguintes códigos fazem com que uma declaração SQL prossiga: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO e SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Parâmetros de revinculação

 Um aplicativo pode executar qualquer uma das duas operações para alterar uma vinculação:  
  
-   Ligue para **o SQLBindParameter** para especificar uma nova vinculação para uma coluna que já esteja vinculada. O motorista substitui a antiga ligação com a nova.  
  
-   Especifique uma compensação a ser adicionada ao endereço buffer especificado pela chamada vinculante ao **SQLBindParameter**. Para obter mais informações, consulte a próxima seção, "Revinculação com Deslocamentos".  
  
## <a name="rebinding-with-offsets"></a>Revinculação com Deslocamentos

 A revinculação de parâmetros é especialmente útil quando um aplicativo tem uma configuração de área de buffer que pode conter muitos parâmetros, mas uma chamada para **SQLExecDirect** ou **SQLExecute** usa apenas alguns dos parâmetros. O espaço restante na área de buffer pode ser usado para o próximo conjunto de parâmetros modificando a vinculação existente por um deslocamento.  
  
 O campo de cabeçalho SQL_DESC_BIND_OFFSET_PTR no APD aponta para a compensação de vinculação. Se o campo não for nulo, o driver desfaz o ponteiro e, se nenhum dos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR for um ponteiro nulo, adicione o valor desreferenciado a esses campos nos registros do descritor no momento da execução. Os novos valores de ponteiro são usados quando as instruções SQL são executadas. O deslocamento permanece válido após a revinculação. Como SQL_DESC_BIND_OFFSET_PTR é um ponteiro para o deslocamento em vez do deslocamento em si, um aplicativo pode alterar o deslocamento diretamente, sem ter que chamar [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) para alterar o campo descritor. O ponteiro está definido como nulo por padrão. O campo SQL_DESC_BIND_OFFSET_PTR do ARD pode ser definido por uma chamada para [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou por uma chamada para [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)com um *fAttribute* de SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 A compensação vinculante é sempre adicionada diretamente aos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se a compensação for alterada para um valor diferente, o novo valor ainda será adicionado diretamente ao valor em cada campo descritor. O novo deslocamento não é adicionado à soma do valor de campo e a quaisquer compensações anteriores.  
  
## <a name="descriptors"></a>Descritores

 Como um parâmetro é vinculado é determinado por campos de APDs e IPDs. Os argumentos no **SQLBindParameter** são usados para definir esses campos descritores. Os campos também podem ser definidos pelas funções **SQLSetDescField,** embora **o SQLBindParameter** seja mais eficiente de usar porque o aplicativo não precisa obter uma alça de descritor para chamar **SQLBindParameter**.  
  
> [!CAUTION]  
>  Chamar **sqlBindParameter** para uma instrução pode afetar outras instruções. Isso ocorre quando o ARD associado à declaração é explicitamente alocado e também está associado a outras declarações. Como **o SQLBindParameter** modifica os campos da APD, as modificações se aplicam a todas as instruções com as quais este descritor está associado. Se este não for o comportamento necessário, o aplicativo deve dissociar este descritor das outras instruções antes de chamar **SQLBindParameter**.  
  
 Conceitualmente, **o SQLBindParameter** executa as seguintes etapas em seqüência:  
  
1.  Chama [sqlGetstmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obter o cabo APD.  
  
2.  Chama [o SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obter o campo SQL_DESC_COUNT da APD e se o valor do argumento *ColunaNúmero* exceder o valor de SQL_DESC_COUNT, chama **SQLSetDescField** para aumentar o valor de SQL_DESC_COUNT para O Número de *Colunas*.  
  
3.  Chama [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) várias vezes para atribuir valores aos seguintes campos da APD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE ao valor do *ValueType,* exceto que se *ValueType* for um dos identificadores concisos de um subtipo de data ou intervalo, ele define SQL_DESC_TYPE para SQL_DATETIME ou SQL_INTERVAL, respectivamente, define SQL_DESC_CONCISE_TYPE para o identificador conciso e define SQL_DESC_DATETIME_INTERVAL_CODE para o subcódigo de data ou intervalo correspondente.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH para o valor de *BufferLength*.  
  
    -   Define o campo SQL_DESC_DATA_PTR ao valor de *ParameterValue*.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH_PTR ao valor de *StrLen_or_Ind*.  
  
    -   Define o campo SQL_DESC_INDICATOR_PTR também para o valor de *StrLen_or_Ind*.  
  
     O *parâmetro StrLen_or_Ind* especifica tanto as informações do indicador quanto o comprimento do valor do parâmetro.  
  
4.  Chama [sqlGetstmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obter o cabo IPD.  
  
5.  Chama [o SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obter o campo SQL_DESC_COUNT do IPD e se o valor do argumento *ColunaNúmero* exceder o valor de SQL_DESC_COUNT, chama **SQLSetDescField** para aumentar o valor de SQL_DESC_COUNT para Número de *Colunas*.  
  
6.  Chama [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) várias vezes para atribuir valores aos seguintes campos do IPD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE ao valor de *ParameterType,* exceto que se *ParameterType* for um dos identificadores concisos de um subtipo de data ou intervalo, ele define SQL_DESC_TYPE para SQL_DATETIME ou SQL_INTERVAL, respectivamente, define SQL_DESC_CONCISE_TYPE para o identificador conciso e define SQL_DESC_DATETIME_INTERVAL_CODE para o subcódigo de data ou intervalo correspondente.  
  
    -   Define um ou mais de SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION, conforme apropriado para *ParameterType*.  
  
    -   Define SQL_DESC_SCALE ao valor de *DecimalDigits*.  
  
 Se a chamada para **SQLBindParameter** falhar, o conteúdo dos campos de descritor que ele teria definido na APD será indefinido e o campo SQL_DESC_COUNT da APD será inalterado. Além disso, os campos SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_TYPE do registro apropriado no IPD estão indefinidos e o campo SQL_DESC_COUNT do IPD é inalterado.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversão de chamadas para e de SQLSetParam

 Quando um aplicativo ODBC 1.0 chama **SQLSetParam** em um ODBC 3. *x* driver, o ODBC 3. *x* Driver Manager mapeia a chamada conforme mostrado na tabela a seguir.  
  
|Chamada por aplicativo ODBC 1.0|Ligue para o ODBC 3. *x* motorista|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize,* *DecimalDigits,* ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo prepara uma instrução SQL para inserir dados na tabela ORDERS. Para cada parâmetro na declaração, o aplicativo chama **SQLBindParameter** para especificar o tipo de dados ODBC C e o tipo de dados SQL do parâmetro e para vincular um buffer a cada parâmetro. Para cada linha de dados, o aplicativo atribui valores de dados a cada parâmetro e chama **SQLExecute** para executar a declaração.  
  
 A amostra a seguir pressupõe que você tem uma fonte de dados ODBC em seu computador chamada Northwind que está associada ao banco de dados Northwind.  
  
 Para obter mais exemplos de código, consulte [SQLBulkOperations Function,](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLProcedures Function,](../../../odbc/reference/syntax/sqlprocedures-function.md) [SQLPutData Function](../../../odbc/reference/syntax/sqlputdata-function.md)e [SQLSetPos Function](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>Exemplo de código

 No exemplo a seguir, um aplicativo executa um procedimento armazenado no SQL Server usando um parâmetro nomeado.  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando informações sobre um parâmetro em uma declaração|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executando uma declaração SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberação de buffers de parâmetros na declaração|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando o número de parâmetros de declaração|[Função SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Retornando o próximo parâmetro para enviar dados para|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Especificando múltiplos valores de parâmetros|[Função SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Envio de dados de parâmetros na hora da execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também

 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
