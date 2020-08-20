---
description: Função SQLBindParameter
title: Função SQLBindParameter | Microsoft Docs
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
ms.openlocfilehash: e6866f7c35dbf38f25cf854368053ffd46c74baa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461218"
---
# <a name="sqlbindparameter-function"></a>Função SQLBindParameter

**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 2,0: ODBC  
  
 **Resumo**  
 **SQLBindParameter** associa um buffer a um marcador de parâmetro em uma instrução SQL. O **SQLBindParameter** dá suporte à associação a um tipo de dados C Unicode, mesmo que o driver subjacente não ofereça suporte a dados Unicode.  
  
> [!NOTE]  
>  Essa função substitui a função **SQLSetParam**do ODBC 1,0. Para obter mais informações, consulte "Comentários".  
  
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
 Entrada Identificador de instrução.  
  
 *ParameterNumber*  
 Entrada Número do parâmetro, ordenado sequencialmente no aumento da ordem do parâmetro, começando em 1.  
  
 *InputOutputType*  
 Entrada O tipo do parâmetro. Para obter mais informações, consulte "*InputOutputType* Argument" em "comments".  
  
 *ValueType*  
 Entrada O tipo de dados C do parâmetro. Para obter mais informações, consulte "argumento*ValueType* " em "Comentários".  
  
 *ParameterType*  
 Entrada O tipo de dados SQL do parâmetro. Para obter mais informações, consulte "*ParameterType* Argument" em "comments".  
  
 *ColumnSize*  
 Entrada O tamanho da coluna ou expressão do marcador de parâmetro correspondente. Para obter mais informações, consulte o argumento "*colunasize* " em "Comentários".  
  
 Se seu aplicativo for executado em um sistema operacional Windows de 64 bits, confira [informações ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 Entrada Os dígitos decimais da coluna ou expressão do marcador de parâmetro correspondente. Para obter mais informações sobre o tamanho da coluna, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Entrada adiada] Um ponteiro para um buffer para os dados do parâmetro. Para obter mais informações, consulte "*ParameterValuePtr* Argument" em "comments".  
  
 *BufferLength*  
 [Entrada/saída] Comprimento do buffer *ParameterValuePtr* em bytes. Para obter mais informações, consulte "*BufferLength* Argument" em "comments".  
  
 Consulte [informações de ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md), se seu aplicativo for executado em um sistema operacional de 64 bits.  
  
 *StrLen_or_IndPtr*  
 [Entrada adiada] Um ponteiro para um buffer para o comprimento do parâmetro. Para obter mais informações, consulte "argumento*StrLen_or_IndPtr* " em "Comentários".  
  
## <a name="returns"></a>Retornos

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos

 Quando **SQLBindParameter** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBindParameter** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  

|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O tipo de dados identificado pelo argumento *ValueType* não pode ser convertido para o tipo de dados identificado pelo argumento *ParameterType* . Observe que esse erro pode ser retornado por **SQLExecDirect**, **SQLExecute**ou **SQLPutData** no momento da execução, em vez de por **SQLBindParameter**.|  
|07009|Índice de descritor inválido|(DM) o valor especificado para o argumento *ParameterNumber* era menor que 1.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer **MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY003|Tipo de buffer de aplicativo inválido|O valor especificado pelo argumento *ValueType* não era um tipo de dados C ou SQL_C_DEFAULT válido.|  
|HY004|Tipo de dados SQL inválido|O valor especificado para o argumento *ParameterType* não era um identificador de tipo de dados SQL ODBC válido nem um identificador de tipo de dados SQL específico do driver suportado pelo driver.|  
|HY009|Valor de argumento inválido|(DM) o argumento *ParameterValuePtr* era um ponteiro NULL, o argumento *StrLen_or_IndPtr* era um ponteiro nulo e o argumento *InputOutputType* não foi SQL_PARAM_OUTPUT.<br /><br /> (DM) SQL_PARAM_OUTPUT, em que o argumento *ParameterValuePtr* era um ponteiro nulo, o tipo C era char ou Binary e BufferLength (*cbValueMax*) era maior que 0.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando **SQLBindParameter** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY021|Informações de descritor inconsistentes|As informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. (Consulte a seção "verificações de consistência" em **SQLSetDescField**.)<br /><br /> O valor especificado para o argumento *DecimalDigits* estava fora do intervalo de valores com suporte pela fonte de dados para uma coluna do tipo de dados SQL especificado pelo argumento *ParameterType* .|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor em *BufferLength* era menor que 0. (Consulte a descrição do campo SQL_DESC_DATA_PTR em **SQLSetDescField**.)|  
|HY104|Precisão ou valor de escala inválido|O valor especificado para o argumento *ColumnSize* ou *DecimalDigits* estava fora do intervalo de valores aceitos pela fonte de dados para uma coluna do tipo de dados SQL especificada pelo argumento *ParameterType* .|  
|HY105|Tipo de parâmetro inválido|(DM) o valor especificado para o argumento *InputOutputType* era inválido. (Consulte "Comentários".)|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à conversão especificada pela combinação do valor especificado para o argumento *ValueType* e o valor específico do driver especificado para o argumento *ParameterType*.<br /><br /> O valor especificado para o argumento *ParameterType* era um identificador de tipo de dados SQL ODBC válido para a versão do ODBC com suporte do driver, mas não era suportado pelo driver ou pela fonte de dados.<br /><br /> O driver dá suporte apenas ao ODBC 2. *x* e o argumento *ValueType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e todos os tipos de dados do intervalo C listados em [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice D: tipos de dados.<br /><br /> O driver só dá suporte a versões ODBC anteriores a 3,50 e o argumento *ValueType* foi SQL_C_GUID.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários

 Um aplicativo chama **SQLBindParameter** para associar cada marcador de parâmetro em uma instrução SQL. As associações permanecem em vigor até que o aplicativo chame **SQLBindParameter** novamente, chama **SQLFreeStmt** com a opção SQL_RESET_PARAMS ou chama **SQLSetDescField** para definir o campo de cabeçalho SQL_DESC_COUNT do APD como 0.  
  
 Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre tipos de dados de parâmetro e marcadores de parâmetro, consulte [tipos de dados de parâmetro](../../../odbc/reference/appendixes/parameter-data-types.md) e marcadores de [parâmetro](../../../odbc/reference/appendixes/parameter-markers.md) no Apêndice C: gramática SQL.  
  
## <a name="parameternumber-argument"></a>Argumento ParameterNumber  
 Se *ParameterNumber* na chamada para **SQLBindParameter** for maior que o valor de SQL_DESC_COUNT, **SQLSetDescField** será chamado para aumentar o valor de SQL_DESC_COUNT para *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argumento InputOutputType  
 O argumento *InputOutputType* especifica o tipo do parâmetro. Esse argumento define o campo SQL_DESC_PARAMETER_TYPE do IPD. Todos os parâmetros em instruções SQL que não chamam procedimentos, como instruções **Insert** , são *parâmetros de entrada * **. Parâmetros em chamadas de procedimento podem ser parâmetros de entrada, entrada/saída ou saída. (Um aplicativo chama **SQLProcedureColumns** para determinar o tipo de um parâmetro em uma chamada de procedimento; os parâmetros cujo tipo não pode ser determinado são considerados parâmetros de entrada.)  
  
 O argumento *InputOutputType* é um dos seguintes valores:  
  
-   SQL_PARAM_INPUT. O parâmetro marca um parâmetro em uma instrução SQL que não chama um procedimento, como uma instrução **Insert** , ou marca um parâmetro de entrada em um procedimento. Por exemplo, os parâmetros em **inserir em valores de funcionário (?,?,?)** são parâmetros de entrada, enquanto os parâmetros em **{call AddEmp (?,?,?)}** podem ser, mas não necessariamente, parâmetros de entrada.  
  
     Quando a instrução é executada, o driver envia dados para o parâmetro para a fonte de dados; o \* buffer *ParameterValuePtr* deve conter um valor de entrada válido ou o buffer **StrLen_or_IndPtr* deve conter SQL_NULL_DATA, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC.  
  
     Se um aplicativo não puder determinar o tipo de um parâmetro em uma chamada de procedimento, ele definirá *InputOutputType* como SQL_PARAM_INPUT; se a fonte de dados retornar um valor para o parâmetro, o driver o descartará.  
  
-   SQL_PARAM_INPUT_OUTPUT. O parâmetro marca um parâmetro de entrada/saída em um procedimento. Por exemplo, o parâmetro em **{Call GetEmpDept (?)}** é um parâmetro de entrada/saída que aceita o nome de um funcionário e retorna o nome do departamento do funcionário.  
  
     Quando a instrução é executada, o driver envia dados para o parâmetro para a fonte de dados; o \* buffer *ParameterValuePtr* deve conter um valor de entrada válido ou o \* buffer de *StrLen_or_IndPtr* deve conter SQL_NULL_DATA, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. Depois que a instrução é executada, o driver retorna dados para o parâmetro para o aplicativo; se a fonte de dados não retornar um valor para um parâmetro de entrada/saída, o driver definirá o buffer **StrLen_or_IndPtr* como SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Quando um aplicativo ODBC 1,0 chama **SQLSetParam** em um driver ODBC 2,0, o Gerenciador de driver converte isso em uma chamada para **SQLBindParameter** na qual o argumento *InputOutputType* é definido como SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. O parâmetro marca o valor de retorno de um procedimento ou um parâmetro de saída em um procedimento; em ambos os casos, eles são conhecidos como *parâmetros de saída*. Por exemplo, o parâmetro em **{? = Call GetNextEmpID}** é um parâmetro de saída que retorna a próxima ID de funcionário.  
  
     Depois que a instrução é executada, o driver retorna dados para o parâmetro para o aplicativo, a menos que os argumentos *ParameterValuePtr* e *StrLen_or_IndPtr* sejam ambos ponteiros nulos; nesse caso, o driver descarta o valor de saída. Se a fonte de dados não retornar um valor para um parâmetro de saída, o driver definirá o buffer **StrLen_or_IndPtr* como SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica que um parâmetro de entrada/saída deve ser transmitido. **SQLGetData** pode ler valores de parâmetro em partes. *BufferLength* é ignorado porque o comprimento do buffer será determinado na chamada de **SQLGetData**. O valor do buffer de *StrLen_or_IndPtr* deve conter SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. Um parâmetro deve ser associado como um parâmetro de data em execução (DAE) na entrada se ele for transmitido na saída. *ParameterValuePtr* pode ser qualquer valor de ponteiro não nulo que será retornado por **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr* para entrada e saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. O mesmo que SQL_PARAM_INPUT_OUTPUT_STREAM, para um parâmetro de saída. **StrLen_or_IndPtr* é ignorado na entrada.  
  
 A tabela a seguir lista diferentes combinações de *InputOutputType* e **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Resultado|Comentário em ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*Len*) ou SQL_DATA_AT_EXEC|Entrada em partes|*ParameterValuePtr* pode ser qualquer valor de ponteiro que será retornado por **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|Não SQL_LEN_DATA_AT_EXEC (*Len*) ou SQL_DATA_AT_EXEC|Buffer associado de entrada|*ParameterValuePtr* é o endereço do buffer de entrada.|  
|SQL_PARAM_OUTPUT|Ignorado na entrada.|Buffer associado de saída|*ParameterValuePtr* é o endereço do buffer de saída.|  
|SQL_PARAM_OUTPUT_STREAM|Ignorado na entrada.|Saída em fluxo|*ParameterValuePtr* pode ser qualquer valor de ponteiro, que será retornado por **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*Len*) ou SQL_DATA_AT_EXEC|Entrada em partes e buffer associado de saída|*ParameterValuePtr* é o endereço do buffer de saída, que também será retornado por **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|Não SQL_LEN_DATA_AT_EXEC (*Len*) ou SQL_DATA_AT_EXEC|Buffer vinculado de entrada e buffer associado de saída|*ParameterValuePtr* é o endereço do buffer de entrada/saída compartilhado.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*Len*) ou SQL_DATA_AT_EXEC|Entrada em partes e saída em fluxo|*ParameterValuePtr* pode ser qualquer valor de ponteiro não nulo, que será retornado por **SQLParamData** como o token definido pelo usuário cujo valor foi passado com *ParameterValuePtr* para entrada e saída.|  
  
> [!NOTE]  
>  O driver deve decidir quais tipos SQL são permitidos quando um aplicativo associa um parâmetro de saída ou saída de entrada como transmitido. O Gerenciador de driver não gerará um erro para um tipo SQL inválido.  
  
## <a name="valuetype-argument"></a>Argumento ValueType

 O argumento *ValueType* especifica o tipo de dados C do parâmetro. Esse argumento define os campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE do APD. Isso deve ser um dos valores na seção [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) do Apêndice D: tipos de dados.  
  
 Se o argumento *ValueType* for um dos tipos de dados Interval, o campo SQL_DESC_TYPE do registro *ParameterNumber* de APD será definido como SQL_INTERVAL, o campo SQL_DESC_CONCISE_TYPE de APD será definido como o tipo de dados de intervalo conciso e o campo SQL_DESC_DATETIME_INTERVAL_CODE do registro *ParameterNumber* será definido como um subcódigo para o tipo de dados intervalo específico. (Consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).) A precisão inicial do intervalo padrão (2) e a precisão do intervalo padrão de segundos (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION do APD, respectivamente, são usados para os dados. Se a precisão padrão não for apropriada, o aplicativo deverá definir explicitamente o campo de descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se o argumento *ValueType* for um dos tipos de dados DateTime, o campo SQL_DESC_TYPE do registro *ParameterNumber* de APD será definido como SQL_DATETIME, o campo SQL_DESC_CONCISE_TYPE do registro *ParameterNumber* de APD será definido como o tipo de dados datetime conciso C e o campo SQL_DESC_DATETIME_INTERVAL_CODE do registro *ParameterNumber* será definido como um subcódigo para o tipo de dados DateTime específico. (Consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Se o argumento *ValueType* for um tipo de dados SQL_C_NUMERIC, a precisão padrão (que é definida pelo driver) e a escala padrão (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do APD, serão usados para os dados. Se a precisão ou escala padrão não for apropriada, o aplicativo deverá definir explicitamente o campo de descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 SQL_C_DEFAULT especifica que o valor do parâmetro seja transferido do tipo de dados C padrão para o tipo de dados SQL especificado com *ParameterType*.  
  
 Você também pode especificar um tipo de dados C estendido. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Para obter mais informações, consulte [tipos de dados padrão do c](../../../odbc/reference/appendixes/default-c-data-types.md), [convertendo dados de tipos de dados do c em SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)e [convertendo dados de tipos de dados SQL para C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice D: tipos de dados.  
  
## <a name="parametertype-argument"></a>Argumento ParameterType

 Deve ser um dos valores listados na seção tipos de [dados SQL](../../../odbc/reference/appendixes/sql-data-types.md) do Apêndice D: tipos de dados ou deve ser um valor específico do driver. Esse argumento define os campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE do IPD.  
  
 Se o argumento *ParameterType* for um dos identificadores DateTime, o campo SQL_DESC_TYPE do IPD será definido como SQL_DATETIME, o campo SQL_DESC_CONCISE_TYPE do IPD será definido como o tipo de dados SQL DateTime conciso e o campo SQL_DESC_DATETIME_INTERVAL_CODE será definido como o valor de subcódigo datetime apropriado.  
  
 Se *ParameterType* for um dos identificadores de intervalo, o campo SQL_DESC_TYPE do IPD será definido como SQL_INTERVAL, o campo SQL_DESC_CONCISE_TYPE do IPD será definido como o tipo de dados de intervalo SQL conciso e o campo SQL_DESC_DATETIME_INTERVAL_CODE do IPD será definido como o subcódigo do intervalo apropriado. O campo SQL_DESC_DATETIME_INTERVAL_PRECISION do IPD é definido como a precisão à esquerda do intervalo e o campo SQL_DESC_PRECISION é definido como a precisão do intervalo de segundos, se aplicável. Se o valor padrão de SQL_DESC_DATETIME_INTERVAL_PRECISION ou SQL_DESC_PRECISION não for apropriado, o aplicativo deverá defini-lo explicitamente chamando **SQLSetDescField**. Para obter mais informações sobre qualquer um desses campos, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Se o argumento *ValueType* for um tipo de dados SQL_NUMERIC, a precisão padrão (que é definida pelo driver) e a escala padrão (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do IPD, serão usadas para os dados. Se a precisão ou escala padrão não for apropriada, o aplicativo deverá definir explicitamente o campo de descritor por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Para obter informações sobre como os dados são convertidos, consulte [convertendo dados dos tipos de dados C para SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) e [convertendo dados de tipos de dados SQL para C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice D: tipos de dados.  
  
## <a name="columnsize-argument"></a>Argumento ColumnSize

 O argumento *ColumnSize* especifica o tamanho da coluna ou expressão que corresponde ao marcador de parâmetro, ao comprimento desses dados ou a ambos. Esse argumento define campos diferentes do IPD, dependendo do tipo de dados SQL (o argumento *ParameterType* ). As regras a seguir se aplicam a este mapeamento:  
  
-   Se *ParameterType* for SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um dos tipos de dados conciso SQL DateTime ou Interval, o campo SQL_DESC_LENGTH do IPD será definido como o valor de *colunasize*. (Para obter mais informações, consulte a seção [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.)  
  
-   Se *ParameterType* for SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL ou SQL_DOUBLE, o campo SQL_DESC_PRECISION do IPD será definido como o valor de *colunasize*.  
  
-   Para outros tipos de dados, o argumento *ColumnSize* é ignorado.  
  
 Para obter mais informações, consulte "passando valores de parâmetro" e SQL_DATA_AT_EXEC em "argumento*StrLen_or_IndPtr* ".  
  
## <a name="decimaldigits-argument"></a>Argumento DecimalDigits

 Se *ParameterType* for SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND ou SQL_INTERVAL_MINUTE_TO_SECOND, o campo SQL_DESC_PRECISION do IPD será definido como *DecimalDigits*. Se *ParameterType* for SQL_NUMERIC ou SQL_DECIMAL, o campo SQL_DESC_SCALE do IPD será definido como *DecimalDigits*. Para todos os outros tipos de dados, o argumento *DecimalDigits* é ignorado.  
  
## <a name="parametervalueptr-argument"></a>Argumento ParameterValuePtr

 O argumento *ParameterValuePtr* aponta para um buffer que, quando **SQLExecute** ou **SQLExecDirect** é chamado, contém os dados reais para o parâmetro. Os dados devem estar no formato especificado pelo argumento *ValueType* . Esse argumento define o campo SQL_DESC_DATA_PTR do APD. Um aplicativo pode definir o argumento *ParameterValuePtr* como um ponteiro NULL, desde que * \* StrLen_or_IndPtr* seja SQL_NULL_DATA ou SQL_DATA_AT_EXEC. (Isso se aplica somente aos parâmetros de entrada/entrada/saída.)  
  
 Se \* *StrLen_or_IndPtr* for o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) ou SQL_DATA_AT_EXEC, *ParameterValuePtr* será um valor de ponteiro definido pelo aplicativo que está associado ao parâmetro. Ele é retornado para o aplicativo por meio de **SQLParamData**. Por exemplo, *ParameterValuePtr* pode ser um token diferente de zero, como um número de parâmetro, um ponteiro para dados ou um ponteiro para uma estrutura que o aplicativo usou para associar parâmetros de entrada. No entanto, observe que, se o parâmetro for um parâmetro de entrada/saída, *ParameterValuePtr* deverá ser um ponteiro para um buffer em que o valor de saída será armazenado. Se o valor no atributo da instrução SQL_ATTR_PARAMSET_SIZE for maior que 1, o aplicativo poderá usar o valor apontado pelo atributo instrução SQL_ATTR_PARAMS_PROCESSED_PTR junto com o argumento *ParameterValuePtr* . Por exemplo, *ParameterValuePtr* pode apontar para uma matriz de valores e o aplicativo pode usar o valor apontado por SQL_ATTR_PARAMS_PROCESSED_PTR para recuperar o valor correto da matriz. Para obter mais informações, consulte "passando valores de parâmetro" mais adiante nesta seção.  
  
 Se o argumento *InputOutputType* for SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT, o *ParameterValuePtr* apontará para um buffer no qual o driver retorna o valor de saída. Se o procedimento retornar um ou mais conjuntos de resultados, o \* buffer *ParameterValuePtr* não terá garantia de ser definido até que todos os conjuntos de resultados/contagens de linhas tenham sido processados. Se o buffer não estiver definido até que o processamento seja concluído, os parâmetros de saída e os valores de retorno não estarão disponíveis até que **SQLMoreResults** retorne SQL_NO_DATA. Chamar **SQLCloseCursor** ou **SQLFreeStmt** com uma opção de SQL_CLOSE fará com que esses valores sejam descartados.  
  
 Se o valor no atributo da instrução SQL_ATTR_PARAMSET_SIZE for maior que 1, *ParameterValuePtr* apontará para uma matriz. Uma única instrução SQL processa a matriz completa de valores de entrada para um parâmetro de entrada ou entrada/saída e retorna uma matriz de valores de saída para um parâmetro de entrada/saída ou saída.  
  
## <a name="bufferlength-argument"></a>Argumento BufferLength

 Para dados de caractere e binário C, o argumento *BufferLength* especifica o comprimento do \* buffer *ParameterValuePtr* (se for um único elemento) ou o comprimento de um elemento na \* matriz *ParameterValuePtr* (se o valor no atributo da instrução SQL_ATTR_PARAMSET_SIZE for maior que 1). Esse argumento define o SQL_DESC_OCTET_LENGTH campo de registro do APD. Se o aplicativo especificar vários valores, *BufferLength* será usado para determinar o local dos valores na matriz **ParameterValuePtr* , tanto na entrada quanto na saída. Para parâmetros de entrada/saída e saída, ele é usado para determinar se deve truncar dados de caracteres e C binários na saída:  
  
-   Para dados de caractere C, se o número de bytes disponíveis para retornar for maior ou igual a *BufferLength*, os dados em \* *ParameterValuePtr* serão truncados para *BufferLength* menos o comprimento de um caractere de terminação nula e serão terminados em nulo pelo driver.  
  
-   Para dados binários C, se o número de bytes disponíveis para retornar for maior que *BufferLength*, os dados em \* *ParameterValuePtr* serão truncados para *BufferLength* bytes.  
  
 Para todos os outros tipos de dados C, o argumento *BufferLength* é ignorado. O comprimento do buffer \* *ParameterValuePtr* (se for um único elemento) ou o comprimento de um elemento na \* matriz *ParameterValuePtr* (se o aplicativo chamar **SQLSetStmtAttr** com um argumento de *atributo* de SQL_ATTR_PARAMSET_SIZE para especificar vários valores para cada parâmetro) será considerado o comprimento do tipo de dados C.  
  
 Para saída em fluxo ou parâmetros de entrada/saída em fluxo, o argumento *BufferLength* é ignorado porque o comprimento do buffer é especificado em **SQLGetData**.  
  
> [!NOTE]  
>  Quando um aplicativo ODBC 1,0 chama **SQLSetParam** em um ODBC 3. *x* Driver, o Gerenciador de driver converte isso em uma chamada para **SQLBindParameter** , na qual o argumento *BufferLength* sempre é SQL_SETPARAM_VALUE_MAX. Porque o Gerenciador de driver retornará um erro se um ODBC 3. *x* Application define *BufferLength* como SQL_SETPARAM_VALUE_MAX, um ODBC 3. o driver *x* pode usar isso para determinar quando ele é chamado por um aplicativo ODBC 1,0.  
  
> [!NOTE]  
>  No **SQLSetParam**, a maneira como um aplicativo especifica o tamanho do buffer **ParameterValuePtr* para que o driver possa retornar dados de caracteres ou binários, e a maneira como um aplicativo envia uma matriz de valores de parâmetros binários ou de caracteres para o driver, são definidas pelo driver.  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr argumento

 O argumento *StrLen_or_IndPtr* aponta para um buffer que, quando **SQLExecute** ou **SQLExecDirect** é chamado, contém um dos seguintes. (Esse argumento define os campos de registro SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR dos ponteiros de parâmetro do aplicativo.)  
  
-   O comprimento do valor do parâmetro armazenado em **ParameterValuePtr*. Isso é ignorado, exceto para dados de caractere ou binário C.  
  
-   SQL_NTS. O valor do parâmetro é uma cadeia de caracteres terminada em nulo.  
  
-   SQL_NULL_DATA. O valor do parâmetro é NULL.  
  
-   SQL_DEFAULT_PARAM. Um procedimento é usar o valor padrão de um parâmetro, em vez de um valor recuperado do aplicativo. Esse valor é válido somente em um procedimento chamado na sintaxe canônica ODBC e, em seguida, somente se o argumento *InputOutputType* for SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_INPUT_OUTPUT_STREAM. Quando \* *StrLen_or_IndPtr* é SQL_DEFAULT_PARAM, os *argumentos ValueType*, *ParameterType*, *ColumnSize*, *DecimalDigits*, *BufferLength*e *ParameterValuePtr* são ignorados para os parâmetros de entrada e são usados apenas para definir o valor do parâmetro de saída para parâmetros de entrada/saída.  
  
-   O resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*). Os dados para o parâmetro serão enviados com **SQLPutData**. Se o argumento *ParameterType* for SQL_LONGVARBINARY, SQL_LONGVARCHAR, ou um tipo longo de dados específico da fonte de dados, e o driver retornar "Y" para o tipo de informação SQL_NEED_LONG_DATA_LEN em **SQLGetInfo**, *Length* será o número de bytes de dados a serem enviados para o parâmetro; caso contrário, *Length* deverá ser um valor não negativo e será ignorado. Para obter mais informações, consulte "passando valores de parâmetro", mais adiante nesta seção.  
  
     Por exemplo, para especificar que 10.000 bytes de dados serão enviados com **SQLPutData** em uma ou mais chamadas, para um parâmetro SQL_LONGVARCHAR, um aplicativo define **StrLen_or_IndPtr* como SQL_LEN_DATA_AT_EXEC (10000).  
  
-   SQL_DATA_AT_EXEC. Os dados para o parâmetro serão enviados com **SQLPutData**. Esse valor é usado por aplicativos ODBC 1,0 quando eles chamam o ODBC 3. drivers *x* . Para obter mais informações, consulte "passando valores de parâmetro", mais adiante nesta seção.  
  
 Se *StrLen_or_IndPtr* for um ponteiro nulo, o driver assumirá que todos os valores de parâmetro de entrada são não nulos e que os dados de caractere e binário serão encerrados em nulo. Se *InputOutputType* for SQL_PARAM_OUTPUT ou SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* e *StrLen_or_IndPtr* forem ambos ponteiros nulos, o driver descartará o valor de saída.  
  
> [!NOTE]  
>  Os desenvolvedores de aplicativos são fortemente desencorajados de especificar um ponteiro nulo para *StrLen_or_IndPtr* quando o tipo de dados do parâmetro é SQL_C_BINARY. Para certificar-se de que um driver não trunca inesperadamente SQL_C_BINARY dados, *StrLen_or_IndPtr* deve conter um ponteiro para um valor de comprimento válido.  
  
 Se o argumento *InputOutputType* for SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, o *StrLen_or_IndPtr* apontará para um buffer no qual o driver retorna SQL_NULL_DATA, o número de bytes disponíveis para retornar em \* *ParameterValuePtr* (excluindo o byte de terminação nula de dados de caracteres) ou SQL_NO_TOTAL (se o número de bytes disponíveis para retorno não puder ser determinado). Se o procedimento retornar um ou mais conjuntos de resultados, o buffer **StrLen_or_IndPtr* não terá garantia de ser definido até que todos os resultados tenham sido buscados.  
  
 Se o valor no atributo da instrução SQL_ATTR_PARAMSET_SIZE for maior que 1, *StrLen_or_IndPtr* apontará para uma matriz de valores SQLLEN. Esses podem ser qualquer um dos valores listados anteriormente nesta seção e são processados com uma única instrução SQL.  
  
## <a name="passing-parameter-values"></a>Passando valores de parâmetro

 Um aplicativo pode passar o valor para um parâmetro no \* buffer *ParameterValuePtr* ou com uma ou mais chamadas para **SQLPutData**. Parâmetros cujos dados são passados com **SQLPutData** são conhecidos como parâmetros de *dados em execução* . Normalmente, eles são usados para enviar dados para SQL_LONGVARBINARY e SQL_LONGVARCHAR parâmetros e podem ser misturados com outros parâmetros.  
  
 Para passar valores de parâmetro, um aplicativo executa a seguinte sequência de etapas:  
  
1.  Chama **SQLBindParameter** para cada parâmetro para associar buffers para o valor do parâmetro (argumento*ParameterValuePtr* ) e comprimento/indicador (argumento de*StrLen_or_IndPtr* ). Para parâmetros de dados em execução, *ParameterValuePtr* é um valor de ponteiro definido pelo aplicativo, como um número de parâmetro ou um ponteiro para dados. O valor será retornado mais tarde e poderá ser usado para identificar o parâmetro.  
  
2.  Coloca valores para os parâmetros de entrada e entrada/saída nos \* buffers de *ParameterValuePtr* e **StrLen_or_IndPtr* :  
  
    -   Para parâmetros normais, o aplicativo coloca o valor do parâmetro no \* buffer *ParameterValuePtr* e o comprimento desse valor no buffer **StrLen_or_IndPtr* . Para obter mais informações, consulte [definindo valores de parâmetro](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Para parâmetros de dados em execução, o aplicativo coloca o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) (ao chamar um driver ODBC 2,0) no buffer **StrLen_or_IndPtr* .  
  
3.  Chama **SQLExecute** ou **SQLExecDirect** para executar a instrução SQL.  
  
    -   Se não houver parâmetros de dados em execução, o processo será concluído.  
  
    -   Se houver parâmetros de dados em execução, a função retornará SQL_NEED_DATA.  
  
4.  Chama **SQLParamData** para recuperar o valor definido pelo aplicativo especificado no argumento *ParameterValuePtr* de **SQLBindParameter** para o primeiro parâmetro de dados em execução a ser processado. **SQLParamData** retorna SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Embora os parâmetros de dados em execução se assemelham a colunas de dados em execução, o valor retornado por **SQLParamData** é diferente para cada um. Os parâmetros de dados em execução são parâmetros em uma instrução SQL para a qual os dados serão enviados com **SQLPutData** quando a instrução for executada com **SQLExecDirect** ou **SQLExecute**. Eles são associados a **SQLBindParameter**. O valor retornado por **SQLParamData** é um valor de ponteiro passado para **SQLBindParameter** no argumento *ParameterValuePtr* . As colunas de dados em execução são colunas em um conjunto de linhas para o qual os dados serão enviados com **SQLPutData** quando uma linha é atualizada ou adicionada com **SQLBulkOperations** ou atualizada com **SQLSetPos**. Eles são associados a **SQLBindCol**. O valor retornado por **SQLParamData** é o endereço da linha no buffer **TargetValuePtr* (definido por uma chamada para **SQLBindCol**) que está sendo processada.  
  
5.  Chama **SQLPutData** uma ou mais vezes para enviar dados para o parâmetro. Mais de uma chamada será necessária se o valor dos dados for maior do que o \* buffer *ParameterValuePtr* especificado em **SQLPutData**; várias chamadas para **SQLPutData** para o mesmo parâmetro são permitidas somente ao enviar dados de caracteres c para uma coluna com um tipo de dados específico de caractere, binário ou de fonte de dados ou ao enviar dados binários c para uma coluna com um tipo de dados específico de fonte de dados, binário  
  
6.  Chama **SQLParamData** novamente para sinalizar que todos os dados foram enviados para o parâmetro.  
  
    -   Se houver mais parâmetros de dados em execução, **SQLParamData** retornará SQL_NEED_DATA e o valor definido pelo aplicativo para o próximo parâmetro de dados em execução a ser processado. O aplicativo repete as etapas 4 e 5.  
  
    -   Se não houver mais parâmetros de dados em execução, o processo será concluído. Se a instrução tiver sido executada com êxito, **SQLParamData** retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO; se a execução falhar, ela retornará SQL_ERROR. Neste ponto, **SQLParamData** pode retornar qualquer SQLSTATE que possa ser retornado pela função usada para executar a instrução (**SQLExecDirect** ou **SQLExecute**).  
  
         Os valores de saída para quaisquer parâmetros de entrada/saída ou saída estão disponíveis nos \* buffers *ParameterValuePtr* e **StrLen_or_IndPtr* depois que o aplicativo recupera todos os conjuntos de resultados gerados pela instrução.  
  
 Chamar **SQLExecute** ou **SQLExecDirect** coloca a instrução em um estado SQL_NEED_DATA. Neste ponto, o aplicativo pode chamar apenas **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**ou **SQLPutData** com a instrução ou o identificador de *conexão* associado à instrução. Se ele chamar qualquer outra função com a instrução ou a conexão associada à instrução, a função retornará SQLSTATE HY010 (erro de sequência de função). A instrução deixa o estado de SQL_NEED_DATA quando **SQLParamData** ou **SQLPutData** retorna um erro, **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO ou a instrução é cancelada.  
  
 Se o aplicativo chamar **SQLCancel** enquanto o driver ainda precisar de dados para parâmetros de dados em execução, o driver cancelará a execução da instrução; o aplicativo pode então chamar **SQLExecute** ou **SQLExecDirect** novamente.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída em fluxo

 Quando um aplicativo define *InputOutputType* como SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM, o valor do parâmetro de saída deve ser recuperado por uma ou mais chamadas para **SQLGetData**. Quando o driver tem um valor de parâmetro de saída em fluxo para retornar ao aplicativo, ele retornará SQL_PARAM_DATA_AVAILABLE em resposta a uma chamada para as seguintes funções: **SQLMoreResults**, **SQLExecute**e **SQLExecDirect**. Um aplicativo chama **SQLParamData** para determinar qual valor de parâmetro está disponível.  
  
 Para obter mais informações sobre SQL_PARAM_DATA_AVAILABLE e parâmetros de saída em fluxo, consulte [recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Usar matrizes de parâmetros

 Quando um aplicativo prepara uma instrução com marcadores de parâmetro e passa em uma matriz de parâmetros, há duas maneiras diferentes de executar. Uma maneira é o driver se basear nos recursos de processamento de matriz do back-end; nesse caso, a instrução inteira com a matriz de parâmetros é tratada como uma unidade atômica. Oracle é um exemplo de uma fonte de dados que oferece suporte a recursos de processamento de matriz. Outra maneira de implementar esse recurso é o driver gerar um lote de instruções SQL, uma instrução SQL para cada conjunto de parâmetros na matriz de parâmetros e executar o lote. Matrizes de parâmetros não podem ser usadas com uma **atualização em que** a instrução atual.  
  
 Quando uma matriz de parâmetros é processada, os conjuntos de resultados individuais/contagens de linhas (um para cada conjunto de parâmetros) podem estar disponíveis ou as contagens de conjuntos/linhas de resultados podem ser acumuladas em uma. A opção SQL_PARAM_ARRAY_ROW_COUNTS em **SQLGetInfo** indica se as contagens de linha estão disponíveis para cada conjunto de parâmetros (SQL_PARC_BATCH) ou se apenas uma contagem de linhas está disponível (SQL_PARC_NO_BATCH).  
  
 A opção SQL_PARAM_ARRAY_SELECTS em **SQLGetInfo** indica se um conjunto de resultados está disponível para cada conjunto de parâmetros (SQL_PAS_BATCH) ou apenas um conjunto de resultados está disponível (SQL_PAS_NO_BATCH). Se o driver não permitir que uma instrução de geração de conjunto de resultados seja executada com uma matriz de parâmetros, SQL_PARAM_ARRAY_SELECTS retornará SQL_PAS_NO_SELECT.  
  
 Para obter mais informações, consulte [função SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Para dar suporte a matrizes de parâmetros, o atributo de instrução SQL_ATTR_PARAMSET_SIZE é definido para especificar o número de valores para cada parâmetro. Se o campo for maior que 1, os campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR do APD deverão apontar para matrizes. A cardinalidade de cada matriz é igual ao valor de SQL_ATTR_PARAMSET_SIZE.  
  
 O campo SQL_DESC_ROWS_PROCESSED_PTR do APD aponta para um buffer que contém o número de conjuntos de parâmetros que foram processados, incluindo conjuntos de erros. Como cada conjunto de parâmetros é processado, o driver armazena um novo valor no buffer. Nenhum número será retornado se esse for um ponteiro nulo. Quando são usadas matrizes de parâmetros, o valor apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR de APD é populado mesmo que SQL_ERROR seja retornada pela função de configuração. Se SQL_NEED_DATA for retornado, o valor apontado pelo SQL_DESC_ROWS_PROCESSED_PTR campo de APD será definido como o conjunto de parâmetros que está sendo processado.  
  
 O que ocorre quando uma matriz de parâmetros é associada e uma **atualização em que Current of** Statement é executada é definida pelo driver.  
  
## <a name="column-wise-parameter-binding"></a>Associação de parâmetro de coluna

 Na associação de coluna, o aplicativo associa o parâmetro separado e matrizes de comprimento/indicador a cada parâmetro.  
  
 Para usar a associação de coluna, o aplicativo primeiro define o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE como SQL_PARAM_BIND_BY_COLUMN. (Esse é o padrão.) Para cada coluna a ser associada, o aplicativo executa as seguintes etapas:  
  
1.  Aloca uma matriz de buffer de parâmetro.  
  
2.  Aloca uma matriz de buffers de comprimento/indicador.  
  
    > [!NOTE]  
    >  Se o aplicativo gravar diretamente nos descritores quando a associação de coluna for usada, matrizes separadas poderão ser usadas para dados de comprimento e indicador.  
  
3.  Chama **SQLBindParameter** com os seguintes argumentos:  
  
    -   *ValueType* é o tipo C de um único elemento na matriz de buffer de parâmetro.  
  
    -   *ParameterType* é o tipo SQL do parâmetro.  
  
    -   *ParameterValuePtr* é o endereço da matriz de buffer de parâmetro.  
  
    -   *BufferLength* é o tamanho de um único elemento na matriz de buffer de parâmetro. O argumento *BufferLength* é ignorado quando os dados são de comprimento fixo.  
  
    -   *StrLen_or_IndPtr* é o endereço da matriz de comprimento/indicador.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "ParameterValuePtr Argument" em "comments", mais adiante nesta seção. Para obter mais informações sobre a associação por coluna de parâmetros, consulte [associando matrizes de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>Associação de parâmetro de linha

 Na associação de linha, o aplicativo define uma estrutura que contém buffers de parâmetro e comprimento/indicador para cada parâmetro a ser associado.  
  
 Para usar a associação de linha, o aplicativo executa as seguintes etapas:  
  
1.  Define uma estrutura para manter um único conjunto de parâmetros (incluindo buffers de parâmetro e comprimento/indicador) e aloca uma matriz dessas estruturas.  
  
    > [!NOTE]  
    >  Se o aplicativo gravar diretamente nos descritores quando a associação de linha for usada, campos separados poderão ser usados para dados de comprimento e indicador.  
  
2.  Define o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE como o tamanho da estrutura que contém um único conjunto de parâmetros ou o tamanho de uma instância de um buffer no qual os parâmetros serão associados. O comprimento deve incluir espaço para todos os parâmetros associados e qualquer preenchimento da estrutura ou do buffer, para garantir que quando o endereço de um parâmetro associado for incrementado com o comprimento especificado, o resultado apontará para o início do mesmo parâmetro na próxima linha. Quando você usa o operador *sizeof* no ANSI C, esse comportamento é garantido.  
  
3.  Chama **SQLBindParameter** com os seguintes argumentos para cada parâmetro a ser associado:  
  
    -   *ValueType* é o tipo do membro de buffer de parâmetro a ser associado à coluna.  
  
    -   *ParameterType* é o tipo SQL do parâmetro.  
  
    -   *ParameterValuePtr* é o endereço do membro de buffer de parâmetro no primeiro elemento de matriz.  
  
    -   *BufferLength* é o tamanho do membro do buffer de parâmetro.  
  
    -   *StrLen_or_IndPtr* é o endereço do membro de comprimento/indicador a ser associado.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "argumento*ParameterValuePtr* ", mais adiante nesta seção. Para obter mais informações sobre associação de parâmetros de linha, consulte as [matrizes de associação de parâmetros](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Informações do erro

 Se um driver não implementa matrizes de parâmetros como lotes (a opção SQL_PARAM_ARRAY_ROW_COUNTS é igual a SQL_PARC_NO_BATCH), as situações de erro são tratadas como se uma instrução fosse executada. Se o driver implementar matrizes de parâmetro como lotes, um aplicativo poderá usar o campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR do IPD para determinar qual parâmetro de uma instrução SQL ou qual parâmetro em uma matriz de parâmetros fez **SQLExecDirect** ou **SQLExecute** para retornar um erro. Este campo contém informações de status para cada linha de valores de parâmetro. Se o campo indicar que ocorreu um erro, os campos na estrutura de dados de diagnóstico indicarão o número da linha e do parâmetro do parâmetro que falhou. O número de elementos na matriz será definido pelo campo de cabeçalho SQL_DESC_ARRAY_SIZE no APD, que pode ser definido pelo atributo de instrução SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  O campo de cabeçalho SQL_DESC_ARRAY_STATUS_PTR no APD é usado para ignorar parâmetros. Para obter mais informações sobre como ignorar parâmetros, consulte a próxima seção, "ignorando um conjunto de parâmetros".  
  
 Quando **SQLExecute** ou **SQLExecDirect** retorna SQL_ERROR, os elementos na matriz apontados pelo campo SQL_DESC_ARRAY_STATUS_PTR no IPD conterão SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED ou SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Para cada elemento nessa matriz, a estrutura de dados de diagnóstico contém um ou mais registros de status. O campo SQL_DIAG_ROW_NUMBER da estrutura indica o número de linha dos valores de parâmetro que causaram o erro. Se for possível determinar o parâmetro específico em uma linha de parâmetros que causou o erro, o número do parâmetro será inserido no campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED é inserido quando um parâmetro não foi usado porque ocorreu um erro em um parâmetro anterior que forçava a anulação de **SQLExecute** ou **SQLExecDirect** . Por exemplo, se houver parâmetros 50 e um erro ocorreu ao executar o conjunto de parâmetros fortieth que causou a anulação de **SQLExecute** ou **SQLExecDirect** , SQL_PARAM_UNUSED será inserido na matriz de status dos parâmetros 41 a 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE é inserido quando o driver trata as matrizes de parâmetros como uma unidade monolítica, portanto, ele não gera esse nível de parâmetro individual de informações de erro.  
  
 Alguns erros no processamento de um único conjunto de parâmetros fazem com que o processamento dos conjuntos subsequentes de parâmetros na matriz pare. Outros erros não afetam o processamento de parâmetros subsequentes. Quais erros irão parar o processamento é definido pelo driver. Se o processamento não for interrompido, todos os parâmetros na matriz serão processados, SQL_SUCCESS_WITH_INFO será retornado como resultado do erro e o buffer definido por SQL_ATTR_PARAMS_PROCESSED_PTR será definido como o número total de conjuntos de parâmetros processados (conforme definido pelo atributo de instrução SQL_ATTR_PARAMSET_SIZE), que inclui conjuntos de erros.  
  
> [!CAUTION]  
>  O comportamento do ODBC quando ocorre um erro no processamento de uma matriz de parâmetros é diferente no ODBC 3. *x* do que era no ODBC 2. *x*. No ODBC 2. *x*, a função retornou SQL_ERROR e o processamento foi interrompido. O buffer apontado pelo argumento *pirow* de **sqlparamoptions** continha o número da linha de erro. No ODBC 3. *x*, a função retornará SQL_SUCCESS_WITH_INFO e o processamento poderá ser interrompido ou continuado. Se continuar, o buffer especificado pelo SQL_ATTR_PARAMS_PROCESSED_PTR será definido como o valor de todos os parâmetros processados, incluindo aqueles que resultaram em um erro. Essa alteração no comportamento pode causar problemas para os aplicativos existentes.  
  
 Quando **SQLExecute** ou **SQLExecDirect** retorna antes de concluir o processamento de todos os conjuntos de parâmetros em uma matriz de parâmetros, como quando SQL_ERROR ou SQL_NEED_DATA é retornado, a matriz de status contém status para os parâmetros que já foram processados. O local apontado pelo campo SQL_DESC_ROWS_PROCESSED_PTR no IPD contém o número da linha na matriz de parâmetros que causou o SQL_ERROR ou SQL_NEED_DATA código de erro. Quando uma matriz de parâmetros é enviada a uma instrução SELECT, a disponibilidade dos valores de matriz de status é definida pelo driver; Eles podem estar disponíveis depois que a instrução for executada ou conforme os conjuntos de resultados forem buscados.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorando um conjunto de parâmetros

 O campo SQL_DESC_ARRAY_STATUS_PTR do APD (conforme definido pelo atributo da instrução SQL_ATTR_PARAM_STATUS_PTR) pode ser usado para indicar que um conjunto de parâmetros associados em uma instrução SQL deve ser ignorado. Para instruir o driver a ignorar um ou mais conjuntos de parâmetros durante a execução, um aplicativo deve seguir estas etapas:  
  
1.  Chame **SQLSetDescField** para definir o campo de cabeçalho de SQL_DESC_ARRAY_STATUS_PTR do APD para apontar para uma matriz de valores de SQLUSMALLINT para conter informações de status. Esse campo também pode ser definido chamando **SQLSetStmtAttr** com um *atributo* de SQL_ATTR_PARAM_OPERATION_PTR, que permite que um aplicativo defina o campo sem obter um identificador de descritor.  
  
2.  Defina cada elemento da matriz definido pelo SQL_DESC_ARRAY_STATUS_PTR campo de APD como um dos dois valores:  
  
    -   SQL_PARAM_IGNORE, para indicar que a linha foi excluída da execução da instrução.  
  
    -   SQL_PARAM_PROCEED, para indicar que a linha está incluída na execução da instrução.  
  
3.  Chame **SQLExecDirect** ou **SQLExecute** para executar a instrução preparada.  
  
 As regras a seguir se aplicam à matriz definida pelo campo SQL_DESC_ARRAY_STATUS_PTR do APD:  
  
-   O ponteiro é definido como NULL por padrão.  
  
-   Se o ponteiro for nulo, todos os conjuntos de parâmetros serão usados, como se todos os elementos fossem definidos como SQL_ROW_PROCEED.  
  
-   Definir um elemento como SQL_PARAM_PROCEED não garante que a operação usará esse conjunto específico de parâmetros.  
  
-   SQL_PARAM_PROCEED é definido como 0 no arquivo de cabeçalho.  
  
 Um aplicativo pode definir o campo SQL_DESC_ARRAY_STATUS_PTR no APD para apontar para a mesma matriz que apontada pelo campo SQL_DESC_ARRAY_STATUS_PTR no IRD. Isso é útil ao associar parâmetros a dados de linha. Os parâmetros podem ser ignorados de acordo com o status dos dados da linha. Além de SQL_PARAM_IGNORE, os códigos a seguir fazem com que um parâmetro em uma instrução SQL seja ignorado: SQL_ROW_DELETED, SQL_ROW_UPDATED e SQL_ROW_ERROR. Além de SQL_PARAM_PROCEED, os códigos a seguir fazem com que uma instrução SQL prossiga: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO e SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Reassociando parâmetros

 Um aplicativo pode executar uma das duas operações para alterar uma associação:  
  
-   Chame **SQLBindParameter** para especificar uma nova associação para uma coluna que já está associada. O driver substitui a associação antiga por uma nova.  
  
-   Especifique um deslocamento a ser adicionado ao endereço de buffer que foi especificado pela chamada de associação para **SQLBindParameter**. Para obter mais informações, consulte a próxima seção, "reassociando com deslocamentos".  
  
## <a name="rebinding-with-offsets"></a>Reassociando com deslocamentos

 A reassociação de parâmetros é especialmente útil quando um aplicativo tem uma configuração de área de buffer que pode conter muitos parâmetros, mas uma chamada para **SQLExecDirect** ou **SQLExecute** usa apenas alguns dos parâmetros. O espaço restante na área de buffer pode ser usado para o próximo conjunto de parâmetros, modificando a associação existente por um deslocamento.  
  
 O campo de cabeçalho SQL_DESC_BIND_OFFSET_PTR no APD aponta para o deslocamento de associação. Se o campo não for nulo, o driver desreferenciará o ponteiro e, se nenhum dos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR for um ponteiro nulo, o adicionará o valor de referência a esses campos nos registros do descritor em tempo de execução. Os novos valores de ponteiro são usados quando as instruções SQL são executadas. O deslocamento permanece válido após a reassociação. Como SQL_DESC_BIND_OFFSET_PTR é um ponteiro para o deslocamento em vez do deslocamento em si, um aplicativo pode alterar o deslocamento diretamente, sem precisar chamar [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) para alterar o campo do descritor. O ponteiro é definido como NULL por padrão. O campo SQL_DESC_BIND_OFFSET_PTR do ARD pode ser definido por uma chamada para [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ou por uma chamada para [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)com um *fAttribute* de SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 O deslocamento de associação sempre é adicionado diretamente aos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se o deslocamento for alterado para um valor diferente, o novo valor ainda será adicionado diretamente ao valor em cada campo de descritor. O novo deslocamento não é adicionado à soma do valor do campo e a quaisquer deslocamentos anteriores.  
  
## <a name="descriptors"></a>Descritores

 Como um parâmetro é associado é determinado pelos campos de APDs e IPDs. Os argumentos em **SQLBindParameter** são usados para definir esses campos de descritor. Os campos também podem ser definidos pelas funções **SQLSetDescField** , embora o **SQLBindParameter** seja mais eficiente para ser usado porque o aplicativo não precisa obter um identificador de descritor para chamar **SQLBindParameter**.  
  
> [!CAUTION]  
>  Chamar **SQLBindParameter** para uma instrução pode afetar outras instruções. Isso ocorre quando o ARD associado à instrução é explicitamente alocado e também está associado a outras instruções. Como **SQLBindParameter** modifica os campos de APD, as modificações se aplicam a todas as instruções com as quais este descritor está associado. Se esse não for o comportamento necessário, o aplicativo deverá dissociar esse descritor das outras instruções antes de chamar **SQLBindParameter**.  
  
 Conceitualmente, o **SQLBindParameter** executa as seguintes etapas em sequência:  
  
1.  Chama [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obter o identificador APD.  
  
2.  Chama [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obter o campo de SQL_DESC_COUNT do APD e, se o valor do argumento *ColumnNumber* exceder o valor de SQL_DESC_COUNT, o chamará **SQLSetDescField** para aumentar o valor de SQL_DESC_COUNT para *ColumnNumber*.  
  
3.  Chama [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) várias vezes para atribuir valores aos seguintes campos do APD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE como o valor de *ValueType*, exceto que, se *ValueType* for um dos identificadores concisos de um subtipo DateTime ou Interval, ele definirá SQL_DESC_TYPE como SQL_DATETIME ou SQL_INTERVAL, respectivamente, definirá SQL_DESC_CONCISE_TYPE como o identificador conciso e definirá SQL_DESC_DATETIME_INTERVAL_CODE para o subcódigo datetime ou interval correspondente.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH como o valor de *BufferLength*.  
  
    -   Define o campo SQL_DESC_DATA_PTR como o valor de *ParameterValue*.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH_PTR como o valor de *StrLen_or_Ind*.  
  
    -   Define o campo SQL_DESC_INDICATOR_PTR também para o valor de *StrLen_or_Ind*.  
  
     O parâmetro *StrLen_or_Ind* especifica as informações do indicador e o comprimento do valor do parâmetro.  
  
4.  Chama [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obter o identificador de IPD.  
  
5.  Chama [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obter o campo de SQL_DESC_COUNT do IPD e, se o valor do argumento *ColumnNumber* exceder o valor de SQL_DESC_COUNT, o chamará **SQLSetDescField** para aumentar o valor de SQL_DESC_COUNT para *ColumnNumber*.  
  
6.  Chama [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) várias vezes para atribuir valores aos seguintes campos do IPD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE ao valor de *ParameterType*, exceto que se *ParameterType* for um dos identificadores concisos de um subtipo DateTime ou Interval, ele definirá SQL_DESC_TYPE como SQL_DATETIME ou SQL_INTERVAL, respectivamente, definirá SQL_DESC_CONCISE_TYPE para o identificador conciso e definirá SQL_DESC_DATETIME_INTERVAL_CODE para o subcódigo datetime ou interval correspondente.  
  
    -   Define um ou mais SQL_DESC_LENGTH, SQL_DESC_PRECISION e SQL_DESC_DATETIME_INTERVAL_PRECISION, conforme apropriado para *ParameterType*.  
  
    -   Define SQL_DESC_SCALE como o valor de *DecimalDigits*.  
  
 Se a chamada para **SQLBindParameter** falhar, o conteúdo dos campos de descritor que ele teria definido em APD será indefinido e o campo SQL_DESC_COUNT de APD será inalterado. Além disso, os campos SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_TYPE do registro apropriado no IPD são indefinidos e o campo SQL_DESC_COUNT do IPD não é alterado.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversão de chamadas de e para SQLSetParam

 Quando um aplicativo ODBC 1,0 chama **SQLSetParam** em um ODBC 3. *x* Driver, o ODBC 3. *x* Driver Manager mapeia a chamada conforme mostrado na tabela a seguir.  
  
|Chamar por aplicativo ODBC 1,0|Chame para ODBC 3. Driver *x*|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType,      *colunasize*,      *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo prepara uma instrução SQL para inserir dados na tabela ORDERs. Para cada parâmetro na instrução, o aplicativo chama **SQLBindParameter** para especificar o tipo de dados ODBC C e o tipo de dados SQL do parâmetro e associar um buffer a cada parâmetro. Para cada linha de dados, o aplicativo atribui valores de dados a cada parâmetro e chama **SQLExecute** para executar a instrução.  
  
 O exemplo a seguir pressupõe que você tenha uma fonte de dados ODBC em seu computador chamada Northwind que está associada ao banco de dado Northwind.  
  
 Para obter mais exemplos de código, consulte função [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [função sqlprocedimentos](../../../odbc/reference/syntax/sqlprocedures-function.md), [função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)e [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
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

 No exemplo a seguir, um aplicativo executa um procedimento armazenado SQL Server usando um parâmetro nomeado.  
  
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
|Retornando informações sobre um parâmetro em uma instrução|[Função SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Executando uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberando buffers de parâmetro na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Retornando o número de parâmetros de instrução|[Função SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Retornando o próximo parâmetro para o qual enviar dados|[Função SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Especificando vários valores de parâmetro|[Função SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Enviando dados de parâmetro em tempo de execução|[Função SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte Também

 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
