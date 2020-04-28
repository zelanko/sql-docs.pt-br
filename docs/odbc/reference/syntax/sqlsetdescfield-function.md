---
title: Função SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 122d4b26d1d75811d4a8e252378ce8f81ca2c66b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299546"
---
# <a name="sqlsetdescfield-function"></a>Função SQLSetDescField

**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLSetDescField** define o valor de um único campo de um registro de descritor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 Entrada Identificador do descritor.  
  
 *RecNumber*  
 Entrada Indica o registro do descritor que contém o campo que o aplicativo busca definir. Os registros de descritores são numerados de 0, com o número de registro 0 sendo o registro de indicador. O argumento *RecNumber* é ignorado para os campos de cabeçalho.  
  
 *FieldIdentifier*  
 Entrada Indica o campo do descritor cujo valor deve ser definido. Para obter mais informações, consulte "*FieldIdentifier* Argument" na seção "comments".  
  
 *ValuePtr*  
 Entrada Ponteiro para um buffer que contém as informações do descritor ou um valor inteiro. O tipo de dados depende do valor de *FieldIdentifier*. Se *ValuePtr* for um valor inteiro, ele poderá ser considerado como 8 bytes (SQLLEN), 4 bytes (sqlinteiro) ou 2 bytes (SQLSMALLINT), dependendo do valor do argumento *FieldIdentifier* .  
  
 *BufferLength*  
 Entrada Se *FieldIdentifier* for um campo definido pelo ODBC e *ValuePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *FieldIdentifier* for um campo definido pelo ODBC e *ValuePtr* for um inteiro, *BufferLength* será ignorado.  
  
 Se *FieldIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength* . *BufferLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* for um ponteiro para uma cadeia de caracteres, *BufferLength* será o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *ValuePtr* for um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, *BufferLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e um *identificador* de *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetDescField** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não oferecia suporte ao valor especificado em * \*ValuePtr* (se *ValuePtr* era um ponteiro) ou o valor em *ValuePtr* (se *ValuePtr* era um valor inteiro) ou * \*ValuePtr* era inválido devido a condições de funcionamento de implementação, portanto, o driver substituiu um valor semelhante. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O argumento *FieldIdentifier* era um campo de registro, o argumento *RecNumber* era 0 e o argumento *DescriptorHandle* se referia a um identificador de IPD.<br /><br /> O argumento *RecNumber* era menor que 0 e o argumento *DescriptorHandle* se referiu a um ARD ou a um APD.<br /><br /> O argumento *RecNumber* era maior que o número máximo de colunas ou parâmetros para os quais a fonte de dados pode dar suporte e o argumento *DescriptorHandle* referido a um APD ou ARD.<br /><br /> (DM) o argumento *FieldIdentifier* foi SQL_DESC_COUNT e * \** o argumento ValuePtr era menor que 0.<br /><br /> O argumento *RecNumber* era igual a 0 e o argumento *DescriptorHandle* se referiu a um APD alocado implicitamente. (Esse erro não ocorre com um descritor de aplicativo explicitamente alocado, pois não é conhecido se um descritor de aplicativo explicitamente alocado é um APD ou ARD até o tempo de execução.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado falhou antes da função concluir o processamento.|  
|22001|Dados de cadeia de caracteres, truncados à direita|O argumento *FieldIdentifier* foi SQL_DESC_NAME e o argumento *BufferLength* era um valor maior que SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** no buffer * \*MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY010|Erro de sequência de função|(DM) o *DescriptorHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* com o qual o *DescriptorHandle* estava associado e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *DescriptorHandle*. Esta função assíncrona ainda estava em execução quando a função **SQLSetDescField** foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para um dos identificadores de instrução associados ao *DescriptorHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY016|Não é possível modificar um descritor de linha de implementação|O argumento *DescriptorHandle* foi associado a um IRD, e o argumento *FieldIdentifier* não foi SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Informações de descritor inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo ODBC SQL válido ou um tipo SQL específico de driver válido (para IPDs) ou um tipo ODBC C válido (para APDs ou ARDs).<br /><br /> As informações de descritor verificadas durante uma verificação de consistência não estavam consistentes. (Consulte "verificação de consistência" em **SQLSetDescRec**.)|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) * \*ValuePtr* é uma cadeia de caracteres e *BufferLength* era menor que zero, mas não era igual a SQL_NTS.<br /><br /> (DM) o driver era um driver ODBC 2 *. x* , o descritor era um ARD, o argumento *ColumnNumber* foi definido como 0 e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY091|Identificador de campo de descritor inválido|O valor especificado para o argumento *FieldIdentifier* não era um campo definido pelo ODBC e não era um valor definido pela implementação.<br /><br /> O argumento *FieldIdentifier* era inválido para o argumento *DescriptorHandle* .<br /><br /> O argumento *FieldIdentifier* era um campo somente leitura definido pelo ODBC.|  
|HY092|Identificador de atributo/opção inválido|O valor em * \*ValuePtr* não era válido para o argumento *FieldIdentifier* .<br /><br /> O argumento *FieldIdentifier* foi SQL_DESC_UNNAMED e *ValuePtr* foi SQL_NAMED.|  
|HY105|Tipo de parâmetro inválido|(DM) o valor especificado para o campo de SQL_DESC_PARAMETER_TYPE era inválido. (Para obter mais informações, consulte a seção "argumento*InputOutputType* " em **SQLBindParameter**.)|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [novidades no ODBC 3,8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *DescriptorHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetDescField** para definir qualquer campo de descritor, um de cada vez. Uma chamada para **SQLSetDescField** define um único campo em um único descritor. Essa função pode ser chamada para definir qualquer campo em qualquer tipo de descritor, desde que o campo possa ser definido. (Consulte a tabela mais adiante nesta seção.)  
  
> [!NOTE]  
>  Se uma chamada para **SQLSetDescField** falhar, o conteúdo do registro de descritor identificado pelo argumento *RecNumber* será indefinido.  
  
 Outras funções podem ser chamadas para definir vários campos de descritor com uma única chamada da função. A função **SQLSetDescRec** define uma variedade de campos que afetam o tipo de dados e o buffer associado a uma coluna ou parâmetro (os campos SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR). **SQLBindCol** ou **SQLBindParameter** pode ser usado para fazer uma especificação completa para a associação de uma coluna ou parâmetro. Essas funções definem um grupo específico de campos de descritor com uma chamada de função.  
  
 **SQLSetDescField** pode ser chamado para alterar os buffers de associação adicionando um deslocamento aos ponteiros de associação (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR ou SQL_DESC_OCTET_LENGTH_PTR). Isso altera os buffers de associação sem chamar **SQLBindCol** ou **SQLBindParameter**, o que permite que um aplicativo altere SQL_DESC_DATA_PTR sem alterar outros campos, como SQL_DESC_DATA_TYPE.  
  
 Se um aplicativo chamar **SQLSetDescField** para definir qualquer campo que não seja SQL_DESC_COUNT ou os campos adiados SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR ou SQL_DESC_INDICATOR_PTR, o registro se tornará desassociado.  
  
 Os campos de cabeçalho do descritor são definidos chamando **SQLSetDescField** com o *FieldIdentifier*apropriado. Muitos campos de cabeçalho também são atributos de instrução, portanto, eles também podem ser definidos por uma chamada para **SQLSetStmtAttr**. Isso permite que os aplicativos definam um campo de descritor sem primeiro obter um identificador de descritor. Quando **SQLSetDescField** é chamado para definir um campo de cabeçalho, o argumento *RecNumber* é ignorado.  
  
 Um *RecNumber* de 0 é usado para definir campos de indicador.  
  
> [!NOTE]  
>  O atributo de instrução SQL_ATTR_USE_BOOKMARKS sempre deve ser definido antes de chamar **SQLSetDescField** para definir campos de indicador. Embora isso não seja obrigatório, é altamente recomendável.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Sequência de campos de descritor de configuração  
 Ao definir campos de descritor chamando **SQLSetDescField**, o aplicativo deve seguir uma sequência específica:  
  
1.  O aplicativo deve primeiro definir o SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE ou SQL_DESC_DATETIME_INTERVAL_CODE campo.  
  
2.  Depois que um desses campos tiver sido definido, o aplicativo poderá definir um atributo de um tipo de dados e o driver definirá campos de atributo de tipo de dados para os valores padrão apropriados para o tipo de dados. O padrão automático de campos de atributo de tipo garante que o descritor esteja sempre pronto para uso depois que o aplicativo tiver especificado um tipo de dados. Se o aplicativo definir explicitamente um atributo de tipo de dados, ele está substituindo o atributo padrão.  
  
3.  Depois que um dos campos listados na etapa 1 tiver sido definido, e os atributos de tipo de dados tiverem sido definidos, o aplicativo poderá definir SQL_DESC_DATA_PTR. Isso solicita uma verificação de consistência dos campos de descritor. Se o aplicativo alterar o tipo de dados ou atributos depois de definir o campo SQL_DESC_DATA_PTR, o driver definirá SQL_DESC_DATA_PTR como um ponteiro nulo, desvinculando o registro. Isso força o aplicativo a concluir as etapas apropriadas em sequência, antes que o registro do descritor seja utilizável.  
  
## <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor  
 Quando um descritor é alocado, os campos no descritor podem ser inicializados com um valor padrão, ser inicializados sem um valor padrão ou ser indefinido para o tipo de descritor. As tabelas a seguir indicam a inicialização de cada campo para cada tipo de descritor, com "D" indicando que o campo é inicializado com um padrão e "ND" que indica que o campo é inicializado sem um padrão. Se um número for mostrado, o valor padrão do campo será esse número. As tabelas também indicam se um campo é de leitura/gravação (R/W) ou de somente leitura (R).  
  
 Os campos de um IRD têm um valor padrão somente depois que a instrução tiver sido preparada ou executada e o IRD tiver sido populado, não quando o identificador ou descritor de instrução tiver sido alocado. Até que o IRD tenha sido populado, qualquer tentativa de obter acesso a um campo de um IRD retornará um erro.  
  
 Alguns campos de descritor são definidos para um ou mais, mas não todos, dos tipos de descritor (ARDs e IRDs, e APDs e IPDs). Quando um campo é indefinido para um tipo de descritor, ele não é necessário para nenhuma das funções que usam esse descritor.  
  
 Os campos que podem ser acessados pelo **SQLGetDescField** não podem necessariamente ser definidos por **SQLSetDescField**. Os campos que podem ser definidos por **SQLSetDescField** são listados nas tabelas a seguir.  
  
 A inicialização dos campos de cabeçalho é descrita na tabela a seguir.  
  
|Nome do campo de cabeçalho|Type|R/W|Padrão|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: SQL_DESC_ALLOC_AUTO para implícita ou SQL_DESC_ALLOC_USER para Explicit<br /><br /> APD: SQL_DESC_ALLOC_AUTO para implícita ou SQL_DESC_ALLOC_USER para Explicit<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD: R/W APD: R/W IRD: IPD não utilizado: não utilizado|ARD: [1] APD: [1] IRD: IPD não utilizado: não utilizado|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD: R/W APD: R/W IRD: R/W IPD: R/W|ARD: NULL PTR APD: NULL PTR IRD: NULL PTR IPD: NULL PTR|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN|ARD: R/W APD: R/W IRD: IPD não utilizado: não utilizado|ARD: NULL PTR APD: NULL PTR IRD: não utilizado, IPD: não utilizado|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: IPD não utilizado: não utilizado|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: não usado<br /><br /> IPD: não usado|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN|ARD: APD não utilizado: IRD não utilizado: R/W IPD: R/W|ARD: APD não utilizado: IRD não utilizado: NULL PTR IPD: ptr NULL|  
  
 [1] esses campos são definidos somente quando o IPD é preenchido automaticamente pelo driver. Caso contrário, eles serão indefinidos. Se um aplicativo tentar definir esses campos, SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado.  
  
 A inicialização dos campos de registro é mostrada na tabela a seguir.  
  
|Nome do campo de registro|Type|R/W|Padrão|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_ APD PADRÃO: SQL_C_ IRD PADRÃO: D IPD: ND|  
|SQL_DESC_DATA_PTR|Sqlpointr|ARD: R/W APD: R/W IRD: IPD não utilizado: não utilizado|ARD: NULL PTR APD: NULL PTR IRD: IPD não utilizado: não utilizado [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN|ARD: R/W APD: R/W IRD: IPD não utilizado: não utilizado|ARD: NULL PTR APD: NULL PTR IRD: não utilizado, IPD: não utilizado|  
|SQL_DESC_LABEL|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_LENGTH|SQLULEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D [1]|  
|SQL_DESC_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN|ARD: R/W APD: R/W IRD: IPD não utilizado: não utilizado|ARD: NULL PTR APD: NULL PTR IRD: não utilizado, IPD: não utilizado|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: IPD não utilizado: R/W|ARD: APD não utilizado: IRD não utilizado: IPD não utilizado: D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: não usado<br /><br /> APD: não usado<br /><br /> IRD: R<br /><br /> IPD: R|ARD: não usado<br /><br /> APD: não usado<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_TABLE_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: não usado|ARD: APD não utilizado: IRD não utilizado: D IPD: não usado|  
  
 [1] esses campos são definidos somente quando o IPD é preenchido automaticamente pelo driver. Caso contrário, eles serão indefinidos. Se um aplicativo tentar definir esses campos, SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado.  
  
 [2] o campo SQL_DESC_DATA_PTR no IPD pode ser definido para forçar uma verificação de consistência. Em uma chamada subsequente para **SQLGetDescField** ou **SQLGetDescRec**, o driver não é necessário para retornar o valor que SQL_DESC_DATA_PTR foi definido como.  
  
## <a name="fieldidentifier-argument"></a>Argumento FieldIdentifier  
 O argumento *FieldIdentifier* indica o campo de descritor a ser definido. Um descritor contém o *cabeçalho do descritor,* que consiste nos campos de cabeçalho descritos na próxima seção, "campos de cabeçalho" e zero ou mais *registros de descritor,* consistindo nos campos de registro descritos na seção após a seção "campos de cabeçalho".  
  
## <a name="header-fields"></a>Campos de cabeçalho  
 Cada descritor tem um cabeçalho que consiste nos seguintes campos:  
  
 **SQL_DESC_ALLOC_TYPE [todos]**  
 Este campo de cabeçalho SQLSMALLINT somente leitura especifica se o descritor foi alocado automaticamente pelo driver ou explicitamente pelo aplicativo. O aplicativo pode obter, mas não modificar, esse campo. O campo será definido como SQL_DESC_ALLOC_AUTO pelo driver se o descritor tiver sido alocado automaticamente pelo driver. Ele será definido como SQL_DESC_ALLOC_USER pelo driver se o descritor tiver sido explicitamente alocado pelo aplicativo.  
  
 **SQL_DESC_ARRAY_SIZE [descritores de aplicativo]**  
 Em ARDs, esse campo de cabeçalho SQLULEN especifica o número de linhas no conjunto de linhas. Este é o número de linhas a serem retornadas por uma chamada para **SQLFetch** ou **SQLFetchScroll** ou para ser operado por uma chamada para **SQLBulkOperations** ou **SQLSetPos**.  
  
 Em APDs, esse campo de cabeçalho SQLULEN especifica o número de valores para cada parâmetro.  
  
 O valor padrão deste campo é 1. Se SQL_DESC_ARRAY_SIZE for maior que 1, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR do ponto de APD ou ARD para matrizes. A cardinalidade de cada matriz é igual ao valor desse campo.  
  
 Esse campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_ARRAY_SIZE. Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAMSET_SIZE.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [todos]**  
 Para cada tipo de descritor, esse campo de cabeçalho SQLUSMALLINT * aponta para uma matriz de valores de SQLUSMALLINT. Essas matrizes são nomeadas da seguinte maneira: matriz de status de linha (IRD), matriz de status de parâmetro (IPD), matriz de operação de linha (ARD) e matriz de operação de parâmetro (APD).  
  
 No IRD, esse campo de cabeçalho aponta para uma matriz de status de linha que contém valores de status após uma chamada para **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos**. A matriz tem tantos elementos quanto há linhas no conjunto de linhas. O aplicativo deve alocar uma matriz de SQLUSMALLINTs e definir esse campo para apontar para a matriz. O campo é definido como um ponteiro NULL por padrão. O driver preencherá a matriz-a menos que o campo SQL_DESC_ARRAY_STATUS_PTR seja definido como um ponteiro NULL; nesse caso, nenhum valor de status será gerado e a matriz não será preenchida.  
  
> [!CAUTION]  
>  O comportamento do driver será indefinido se o aplicativo definir os elementos da matriz de status de linha apontada pelo campo SQL_DESC_ARRAY_STATUS_PTR do IRD.  
  
 A matriz é inicialmente populada por uma chamada para **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos**. Se a chamada não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo da matriz apontada por esse campo será indefinido. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_ROW_SUCCESS: a linha foi buscada com êxito e não foi alterada desde a última busca.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: a linha foi buscada com êxito e não foi alterada desde a última busca. No entanto, um aviso foi retornado sobre a linha.  
  
-   SQL_ROW_ERROR: ocorreu um erro ao buscar a linha.  
  
-   SQL_ROW_UPDATED: a linha foi buscada com êxito e foi atualizada desde a última busca. Se a linha for buscada novamente, seu status será SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: a linha foi excluída desde a última busca.  
  
-   SQL_ROW_ADDED: a linha foi inserida por **SQLBulkOperations**. Se a linha for buscada novamente, seu status será SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: o conjunto de linhas sobreposto ao final do conjunto de resultados e nenhuma linha foi retornada correspondente a esse elemento da matriz de status de linha.  
  
 Esse campo no IRD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_STATUS_PTR.  
  
 O campo SQL_DESC_ARRAY_STATUS_PTR de IRD é válido somente depois que SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO foi retornado. Se o código de retorno não for um desses, o local apontado por SQL_DESC_ROWS_PROCESSED_PTR será indefinido.  
  
 No IPD, esse campo de cabeçalho aponta para uma matriz de status de parâmetro que contém informações de status para cada conjunto de valores de parâmetro após uma chamada para **SQLExecute** ou **SQLExecDirect**. Se a chamada para **SQLExecute** ou **SQLExecDirect** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo da matriz apontada por esse campo será indefinido. O aplicativo deve alocar uma matriz de SQLUSMALLINTs e definir esse campo para apontar para a matriz. O driver preencherá a matriz-a menos que o campo SQL_DESC_ARRAY_STATUS_PTR seja definido como um ponteiro NULL; nesse caso, nenhum valor de status será gerado e a matriz não será preenchida. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_PARAM_SUCCESS: a instrução SQL foi executada com êxito para este conjunto de parâmetros.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: a instrução SQL foi executada com êxito para este conjunto de parâmetros; no entanto, as informações de aviso estão disponíveis na estrutura de dados de diagnóstico.  
  
-   SQL_PARAM_ERROR: ocorreu um erro ao processar esse conjunto de parâmetros. Informações de erro adicionais estão disponíveis na estrutura de dados de diagnóstico.  
  
-   SQL_PARAM_UNUSED: esse conjunto de parâmetros não foi usado, possivelmente devido ao fato de que algum conjunto de parâmetros anterior causou um erro que anulava o processamento adicional ou porque SQL_PARAM_IGNORE foi definido para esse conjunto de parâmetros na matriz especificada pelo campo SQL_DESC_ARRAY_STATUS_PTR do APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: as informações de diagnóstico não estão disponíveis. Um exemplo disso é quando o driver trata as matrizes de parâmetros como uma unidade monolítica e, portanto, não gera esse nível de informações de erro.  
  
 Esse campo no IPD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 No ARD, esse campo de cabeçalho aponta para uma matriz de operação de linha de valores que podem ser definidos pelo aplicativo para indicar se essa linha deve ser ignorada para operações **SQLSetPos** . Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_ROW_PROCEED: a linha é incluída na operação em massa usando **SQLSetPos**. (Essa configuração não garante que a operação ocorra na linha. Se a linha tiver o status SQL_ROW_ERROR na matriz de status de linha IRD, o driver poderá não ser capaz de executar a operação na linha.)  
  
-   SQL_ROW_IGNORE: a linha é excluída da operação em massa usando **SQLSetPos**.  
  
 Se nenhum elemento da matriz for definido, todas as linhas serão incluídas na operação em massa. Se o valor no campo SQL_DESC_ARRAY_STATUS_PTR de ARD for um ponteiro nulo, todas as linhas serão incluídas na operação em massa; a interpretação é a mesma de se o ponteiro apontar para uma matriz válida e todos os elementos da matriz foram SQL_ROW_PROCEED. Se um elemento na matriz for definido como SQL_ROW_IGNORE, o valor na matriz de status de linha para a linha ignorada não será alterado.  
  
 Esse campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 No APD, esse campo de cabeçalho aponta para uma matriz de operação de parâmetro de valores que podem ser definidos pelo aplicativo para indicar se esse conjunto de parâmetros deve ser ignorado quando **SQLExecute** ou **SQLExecDirect** é chamado. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_PARAM_PROCEED: o conjunto de parâmetros é incluído na chamada **SQLExecute** ou **SQLExecDirect** .  
  
-   SQL_PARAM_IGNORE: o conjunto de parâmetros é excluído da chamada **SQLExecute** ou **SQLExecDirect** .  
  
 Se nenhum elemento da matriz for definido, todos os conjuntos de parâmetros na matriz serão usados nas chamadas **SQLExecute** ou **SQLExecDirect** . Se o valor no campo SQL_DESC_ARRAY_STATUS_PTR de APD for um ponteiro nulo, todos os conjuntos de parâmetros serão usados; a interpretação é a mesma de se o ponteiro apontar para uma matriz válida e todos os elementos da matriz foram SQL_PARAM_PROCEED.  
  
 Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [descritores de aplicativo]**  
 Este campo de cabeçalho SQLLEN * aponta para o deslocamento de associação. Ele é definido como um ponteiro NULL por padrão. Se esse campo não for um ponteiro nulo, o driver desreferenciará o ponteiro e adicionará o valor de referência a cada um dos campos adiados que tem um valor não nulo no registro do descritor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) no momento da busca e usará os novos valores de ponteiro ao ligar.  
  
 O deslocamento de associação sempre é adicionado diretamente aos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se o deslocamento for alterado para um valor diferente, o novo valor ainda será adicionado diretamente ao valor em cada campo de descritor. O novo deslocamento não é adicionado ao valor do campo, além de qualquer deslocamento anterior.  
  
 Este campo é um *campo adiado*: ele não é usado no momento em que é definido, mas é usado posteriormente pelo driver quando ele precisa determinar endereços para buffers de dados.  
  
 Esse campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_BIND_OFFSET_PTR. Esse campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Para obter mais informações, consulte a descrição da Associação de linha em [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) e [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [descritores de aplicativo]**  
 Este campo de cabeçalho SQLUINTEGER define a orientação de associação a ser usada para a associação de colunas ou parâmetros.  
  
 Em ARDs, esse campo especifica a orientação de associação quando **SQLFetchScroll** ou **SQLFetch** é chamado no identificador de instrução associado.  
  
 Para selecionar a associação por coluna para colunas, esse campo é definido como SQL_BIND_BY_COLUMN (o padrão).  
  
 Esse campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o *atributo*SQL_ATTR_ROW_BIND_TYPE.  
  
 No APDs, esse campo especifica a orientação de associação a ser usada para parâmetros dinâmicos.  
  
 Para selecionar a associação de coluna para parâmetros, esse campo é definido como SQL_BIND_BY_COLUMN (o padrão).  
  
 Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o *atributo*SQL_ATTR_PARAM_BIND_TYPE.  
  
 **SQL_DESC_COUNT [todos]**  
 Este campo de cabeçalho SQLSMALLINT especifica o índice de base 1 do registro de numeração mais alto que contém dados. Quando o driver define a estrutura de dados para o descritor, ele também deve definir o campo SQL_DESC_COUNT para mostrar quantos registros são significativos. Quando um aplicativo aloca uma instância dessa estrutura de dados, ele não precisa especificar quantos registros para reservar espaço. Como o aplicativo especifica o conteúdo dos registros, o driver executa qualquer ação necessária para garantir que o identificador do descritor se refira a uma estrutura de dados do tamanho adequado.  
  
 SQL_DESC_COUNT não é uma contagem de todas as colunas de dados que estão associadas (se o campo estiver em um ARD) ou de todos os parâmetros que estão associados (se o campo estiver em um APD), mas o número do registro de número mais alto. Se a coluna mais numerada ou o parâmetro for desassociado, SQL_DESC_COUNT será alterado para o número da próxima coluna ou parâmetro de maior numeração. Se uma coluna ou um parâmetro com um número menor que o número da coluna de maior número for desassociado (chamando **SQLBindCol** com o argumento *TargetValuePtr* definido como um ponteiro nulo ou **SQLBindParameter** com o argumento *ParameterValuePtr* definido como um ponteiro nulo), SQL_DESC_COUNT não será alterado. Se colunas ou parâmetros adicionais estiverem associados a números maiores que o registro de numeração mais alto que contém dados, o driver aumentará automaticamente o valor no campo SQL_DESC_COUNT. Se todas as colunas forem desassociadas chamando **SQLFreeStmt** com a opção SQL_UNBIND, os campos de SQL_DESC_COUNT em ARD e IRD serão definidos como 0. Se **SQLFreeStmt** for chamado com a opção SQL_RESET_PARAMS, os campos de SQL_DESC_COUNT no APD e IPD serão definidos como 0.  
  
 O valor em SQL_DESC_COUNT pode ser definido explicitamente por um aplicativo chamando **SQLSetDescField**. Se o valor em SQL_DESC_COUNT for explicitamente diminuído, todos os registros com números maiores do que o novo valor em SQL_DESC_COUNT serão efetivamente removidos. Se o valor em SQL_DESC_COUNT estiver explicitamente definido como 0 e o campo estiver em um ARD, todos os buffers de dados, exceto uma coluna de indicador acoplada, serão liberados.  
  
 A contagem de registros nesse campo de um ARD não inclui uma coluna de indicador associado. A única maneira de desassociar uma coluna de indicador é definir o campo SQL_DESC_DATA_PTR como um ponteiro nulo.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [descritores de implementação]**  
 Em um IRD, esse campo \* de cabeçalho SQLULEN aponta para um buffer que contém o número de linhas buscadas após uma chamada para **SQLFetch** ou **SQLFetchScroll**, ou o número de linhas afetadas em uma operação em massa executada por uma chamada para **SQLBulkOperations** ou **SQLSetPos**, incluindo linhas de erro.  
  
 Em um IPD, este campo de cabeçalho SQLUINTEGER * aponta para um buffer que contém o número de conjuntos de parâmetros que foram processados, incluindo conjuntos de erros. Nenhum número será retornado se esse for um ponteiro nulo.  
  
 SQL_DESC_ROWS_PROCESSED_PTR é válido somente depois que SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO foi retornado após uma chamada para **SQLFetch** ou **SQLFetchScroll** (para um campo IRD) ou **SQLExecute**, **SQLEXECDIRECT**ou **SQLParamData** (para um campo IPD). Se a chamada que preenche o buffer apontado por este campo não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido, a menos que ele retorne SQL_NO_DATA; nesse caso, o valor no buffer será definido como 0.  
  
 Esse campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROWS_FETCHED_PTR. Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAMS_PROCESSED_PTR.  
  
 O buffer apontado por esse campo é alocado pelo aplicativo. É um buffer de saída adiado que é definido pelo driver. Ele é definido como um ponteiro NULL por padrão.  
  
## <a name="record-fields"></a>Campos de registro  
 Cada descritor contém um ou mais registros que consistem em campos que definem dados de coluna ou parâmetros dinâmicos, dependendo do tipo de descritor. Cada registro é uma definição completa de uma única coluna ou parâmetro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 Esse campo de registro SQLINTEGER somente leitura contém SQL_TRUE se a coluna for uma coluna de incremento automático ou SQL_FALSE se a coluna não for uma coluna de incremento automático. Este campo é somente leitura, mas a coluna de incremento automático subjacente não é necessariamente somente leitura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome da coluna base para a coluna do conjunto de resultados. Se um nome de coluna base não existir (como no caso de colunas que são expressões), essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome da tabela base para a coluna do conjunto de resultados. Se um nome de tabela base não puder ser definido ou não for aplicável, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_CASE_SENSITIVE [descritores de implementação]**  
 Esse campo de registro SQLINTEGER somente leitura contém SQL_TRUE se a coluna ou o parâmetro é tratado como diferenciação de maiúsculas e minúsculas para agrupamentos e comparações, ou SQL_FALSE se a coluna não for tratada como diferenciação de maiúsculas e minúsculas para agrupamentos e comparações ou se for uma coluna que não seja de caractere.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o catálogo da tabela base que contém a coluna. O valor de retorno será dependente de driver se a coluna for uma expressão ou se a coluna fizer parte de uma exibição. Se a fonte de dados não oferecer suporte a catálogos ou se o catálogo não puder ser determinado, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_CONCISE_TYPE [todos]**  
 Este campo de cabeçalho SQLSMALLINT especifica o tipo de dados conciso para todos os tipos de dados, incluindo os tipos de dados DateTime e Interval.  
  
 Os valores nos campos SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE são interdependentes. Cada vez que um dos campos é definido, o outro também deve ser definido. SQL_DESC_CONCISE_TYPE pode ser definido por uma chamada para **SQLBindCol** ou **SQLBindParameter**, ou **SQLSetDescField**. SQL_DESC_TYPE pode ser definido por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se SQL_DESC_CONCISE_TYPE for definido como um tipo de dados conciso diferente de um tipo de dados de intervalo ou DateTime, o campo SQL_DESC_TYPE será definido com o mesmo valor e o campo SQL_DESC_DATETIME_INTERVAL_CODE será definido como 0.  
  
 Se SQL_DESC_CONCISE_TYPE for definido como o tipo de dados conciso DateTime ou Interval, o campo SQL_DESC_TYPE será definido como o tipo detalhado correspondente (SQL_DATETIME ou SQL_INTERVAL) e o campo SQL_DESC_DATETIME_INTERVAL_CODE será definido como o subcódigo apropriado.  
  
 **SQL_DESC_DATA_PTR [descritores de aplicativos e IPDs]**  
 Este campo de registro sqlpointr aponta para uma variável que conterá o valor do parâmetro (para APDs) ou o valor da coluna (para ARDs). Este campo é um *campo adiado*. Ele não é usado no momento em que é definido, mas é usado posteriormente pelo driver para recuperar dados.  
  
 A coluna especificada pelo campo SQL_DESC_DATA_PTR de ARD será desassociada se o argumento *TargetValuePtr* em uma chamada para **SQLBindCol** for um ponteiro nulo ou se o campo SQL_DESC_DATA_PTR no ARD for definido por uma chamada para **SQLSetDescField** ou **SQLSetDescRec** para um ponteiro nulo. Outros campos não serão afetados se o campo SQL_DESC_DATA_PTR for definido como um ponteiro nulo.  
  
 Se a chamada para **SQLFetch** ou **SQLFetchScroll** que preenche o buffer apontado por esse campo não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido.  
  
 Sempre que o campo SQL_DESC_DATA_PTR de um APD, ARD ou IPD é definido, o driver verifica se o valor no campo SQL_DESC_TYPE contém um dos tipos de dados ODBC C válidos ou um tipo de dados específico de driver, e se todos os outros campos que afetam os tipos de dados são consistentes. A solicitação de uma verificação de consistência é o único uso do campo SQL_DESC_DATA_PTR de um IPD. Especificamente, se um aplicativo definir o SQL_DESC_DATA_PTR campo de um IPD e depois chamar **SQLGetDescField** nesse campo, não será necessariamente retornado o valor que ele tinha definido. Para obter mais informações, consulte "verificações de consistência" em [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [todos]**  
 Este campo de registro SQLSMALLINT contém o subcódigo para o tipo de dados DateTime ou interval específico quando o campo SQL_DESC_TYPE é SQL_DATETIME ou SQL_INTERVAL. Isso é verdadeiro para os tipos de dados SQL e C. O código consiste no nome do tipo de dados com "CODE" substituído por "TYPE" ou "C_TYPE" (para tipos DateTime) ou "CODE" substituído por "INTERVAL" ou "C_INTERVAL" (para tipos de intervalo).  
  
 Se SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE em um descritor de aplicativo forem definidos como SQL_C_DEFAULT e o descritor não estiver associado a um identificador de instrução, o conteúdo de SQL_DESC_DATETIME_INTERVAL_CODE será indefinido.  
  
 Esse campo pode ser definido para os tipos de dados DateTime listados na tabela a seguir.  
  
|Tipos de DateTime|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Esse campo pode ser definido para os tipos de dados de intervalo listados na tabela a seguir.  
  
|Tipo de intervalo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Para obter mais informações sobre os intervalos de dados e esse campo, consulte [identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [todos]**  
 Esse campo de registro SQLINTEGER contém a precisão de intervalo inicial se o campo SQL_DESC_TYPE for SQL_INTERVAL. Quando o campo de SQL_DESC_DATETIME_INTERVAL_CODE é definido como um tipo de dados de intervalo, esse campo é definido como a precisão inicial do intervalo padrão.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 Este campo de registro SQLINTEGER somente leitura contém o número máximo de caracteres necessários para exibir os dados da coluna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [descritores de implementação]**  
 Esse campo de registro SQLSMALLINT somente leitura será definido como SQL_TRUE se a coluna for uma coluna numérica exata e tiver uma precisão fixa e uma escala diferente de zero ou para SQL_FALSE se a coluna não for uma coluna numérica exata com precisão e escala fixas.  
  
 **SQL_DESC_INDICATOR_PTR [descritores de aplicativo]**  
 Em ARDs, esse campo de registro SQLLEN * aponta para a variável de indicador. Essa variável contém SQL_NULL_DATA se o valor da coluna for NULL. Para APDs, a variável de indicador é definida como SQL_NULL_DATA para especificar argumentos dinâmicos nulos. Caso contrário, a variável será zero (a menos que os valores em SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR sejam o mesmo ponteiro).  
  
 Se o campo SQL_DESC_INDICATOR_PTR em um ARD for um ponteiro nulo, o driver será impedido de retornar informações sobre se a coluna é nula ou não. Se a coluna for nula e SQL_DESC_INDICATOR_PTR for um ponteiro NULL, SQLSTATE 22002 (variável de indicador necessária, mas não fornecida) será retornado quando o driver tentar preencher o buffer após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Se a chamada para **SQLFetch** ou **SQLFetchScroll** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido.  
  
 O campo SQL_DESC_INDICATOR_PTR determina se o campo apontado por SQL_DESC_OCTET_LENGTH_PTR está definido. Se o valor de dados de uma coluna for nulo, o driver definirá a variável de indicador como SQL_NULL_DATA. O campo apontado por SQL_DESC_OCTET_LENGTH_PTR, em seguida, não é definido. Se um valor nulo não for encontrado durante a busca, o buffer apontado por SQL_DESC_INDICATOR_PTR será definido como zero e o buffer apontado por SQL_DESC_OCTET_LENGTH_PTR será definido como o comprimento dos dados.  
  
 Se o campo SQL_DESC_INDICATOR_PTR em um APD for um ponteiro nulo, o aplicativo não poderá usar esse registro de descritor para especificar argumentos nulos.  
  
 Este campo é um *campo adiado*: ele não é usado no momento em que é definido, mas é usado posteriormente pelo driver para indicar a nulidade (para ARDs) ou para determinar a nulidade (para APDS).  
  
 **SQL_DESC_LABEL [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o rótulo ou o título da coluna. Se a coluna não tiver um rótulo, essa variável conterá o nome da coluna. Se a coluna não tiver nome e não rotulada, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_LENGTH [todos]**  
 Esse campo de registro SQLULEN é o comprimento máximo ou real de uma cadeia de caracteres em caracteres ou um tipo de dados binário em bytes. É o comprimento máximo de um tipo de dados de comprimento fixo ou o comprimento real para um tipo de dados de comprimento variável. Seu valor sempre exclui o caractere de terminação nula que termina a cadeia de caracteres. Para valores cujo tipo é SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP ou um dos tipos de dados SQL Interval, esse campo tem o comprimento em caracteres da representação de cadeia de caracteres do valor DateTime ou Interval.  
  
 O valor nesse campo pode ser diferente do valor de "Length", conforme definido no ODBC 2 *. x*. Para obter mais informações, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o caractere ou caracteres que o driver reconhece como um prefixo para um literal desse tipo de dados. Essa variável contém uma cadeia de caracteres vazia para um tipo de dados para o qual um prefixo literal não é aplicável.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o caractere ou caracteres que o driver reconhece como um sufixo para um literal desse tipo de dados. Essa variável contém uma cadeia de caracteres vazia para um tipo de dados para o qual um sufixo literal não é aplicável.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [descritores de implementação]**  
 Este campo de registro SQLCHAR * somente leitura contém qualquer nome localizado (idioma nativo) para o tipo de dados que pode ser diferente do nome regular do tipo de dados. Se não houver nenhum nome localizado, uma cadeia de caracteres vazia será retornada. Este campo é apenas para fins de exibição.  
  
 **SQL_DESC_NAME [descritores de implementação]**  
 Esse campo de registro SQLCHAR * em um descritor de linha contém o alias da coluna, se aplicável. Se o alias da coluna não se aplicar, o nome da coluna será retornado. Em ambos os casos, o driver define o campo SQL_DESC_UNNAMED como SQL_NAMED ao definir o campo SQL_DESC_NAME. Se não houver nenhum nome de coluna ou um alias de coluna, o driver retornará uma cadeia de caracteres vazia no campo SQL_DESC_NAME e definirá o campo SQL_DESC_UNNAMED como SQL_UNNAMED.  
  
 Um aplicativo pode definir o SQL_DESC_NAME campo de um IPD para um nome de parâmetro ou alias para especificar parâmetros de procedimento armazenado por nome. (Para obter mais informações, consulte [parâmetros de associação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) O campo SQL_DESC_NAME de um IRD é um campo somente leitura; SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado se um aplicativo tentar defini-lo.  
  
 No IPDs, esse campo será indefinido se o driver não oferecer suporte a parâmetros nomeados. Se o driver oferecer suporte a parâmetros nomeados e for capaz de descrever os parâmetros, o nome do parâmetro será retornado nesse campo.  
  
 **SQL_DESC_NULLABLE [descritores de implementação]**  
 No IRDs, esse campo de registro SQLSMALLINT somente leitura será SQL_NULLABLE se a coluna puder ter valores nulos, SQL_NO_NULLS se a coluna não tiver valores nulos ou SQL_NULLABLE_UNKNOWN se não for conhecida se a coluna aceita valores nulos. Esse campo pertence à coluna do conjunto de resultados, não à coluna base.  
  
 No IPDs, esse campo é sempre definido como SQL_NULLABLE porque os parâmetros dinâmicos são sempre anuláveis e não podem ser definidos por um aplicativo.  
  
 **SQL_DESC_NUM_PREC_RADIX [todos]**  
 Esse campo SQLINTEGER contém um valor de 2 se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico aproximado, porque o campo SQL_DESC_PRECISION contém o número de bits. Esse campo contém um valor de 10 se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico exato, porque o campo SQL_DESC_PRECISION contém o número de dígitos decimais. Esse campo é definido como 0 para todos os tipos de dados não numéricos.  
  
 **SQL_DESC_OCTET_LENGTH [todos]**  
 Este campo de registro SQLLEN contém o comprimento, em bytes, de uma cadeia de caracteres ou tipo de dados Binary. Para tipos de caracteres de comprimento fixo ou binários, esse é o comprimento real em bytes. Para tipos de caracteres de comprimento variável ou binários, esse é o comprimento máximo em bytes. Esse valor sempre exclui o espaço para o caractere de terminação nula para descritores de implementação e sempre inclui espaço para o caractere de terminação nula para descritores de aplicativo. Para dados de aplicativo, esse campo contém o tamanho do buffer. Para APDs, esse campo é definido somente para parâmetros de saída ou entrada/saída.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [descritores de aplicativo]**  
 Este campo de registro SQLLEN * aponta para uma variável que conterá o comprimento total em bytes de um argumento dinâmico (para descritores de parâmetro) ou de um valor de coluna associada (para descritores de linha).  
  
 Para um APD, esse valor é ignorado para todos os argumentos, exceto a cadeia de caracteres e o binário; Se esse campo apontar para SQL_NTS, o argumento dinâmico deverá ser finalizado com nulo. Para indicar que um parâmetro associado será um parâmetro de dados em execução, um aplicativo define esse campo no registro apropriado do APD para uma variável que, em tempo de execução, conterá o valor SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC. Se houver mais de um campo, SQL_DESC_DATA_PTR poderá ser definido como um valor que identifica exclusivamente o parâmetro para ajudar o aplicativo a determinar qual parâmetro está sendo solicitado.  
  
 Se o campo OCTET_LENGTH_PTR de um ARD for um ponteiro nulo, o driver não retornará informações de comprimento para a coluna. Se o campo SQL_DESC_OCTET_LENGTH_PTR de um APD for um ponteiro NULL, o driver assumirá que as cadeias de caracteres e os valores binários são terminados em nulo. (Os valores binários não devem ser terminados em nulo, mas devem receber um comprimento para evitar truncamento.)  
  
 Se a chamada para **SQLFetch** ou **SQLFetchScroll** que preenche o buffer apontado por esse campo não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido. Este campo é um *campo adiado*. Ele não é usado no momento em que é definido, mas é usado posteriormente pelo driver para determinar ou indicar o comprimento do octeto dos dados.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 Esse campo de registro SQLSMALLINT é definido como SQL_PARAM_INPUT para um parâmetro de entrada, SQL_PARAM_INPUT_OUTPUT para um parâmetro de entrada/saída, SQL_PARAM_OUTPUT para um parâmetro de saída, SQL_PARAM_INPUT_OUTPUT_STREAM para um parâmetro de fluxo de entrada/saída ou SQL_PARAM_OUTPUT_STREAM para um parâmetro de saída em fluxo. Ele é definido como SQL_PARAM_INPUT por padrão.  
  
 Para um IPD, o campo é definido como SQL_PARAM_INPUT por padrão se o IPD não for preenchido automaticamente pelo driver (o atributo de instrução SQL_ATTR_ENABLE_AUTO_IPD é SQL_FALSE). Um aplicativo deve definir esse campo no IPD para parâmetros que não são parâmetros de entrada.  
  
 **SQL_DESC_PRECISION [todos]**  
 Este campo de registro SQLSMALLINT contém o número de dígitos para um tipo numérico exato, o número de bits no mantissa (precisão binária) para um tipo numérico aproximado ou os números de dígitos no componente de segundos fracionários para o tipo de dados SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP ou SQL_INTERVAL_SECOND. Esse campo é indefinido para todos os outros tipos de dados.  
  
 O valor nesse campo pode ser diferente do valor de "precisão", conforme definido no ODBC 2 *. x*. Para obter mais informações, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [descritores de implementação]**  
 Esse campo SQLSMALLINTrecord indica se uma coluna é modificada automaticamente pelo DBMS quando uma linha é atualizada (por exemplo, uma coluna do tipo "timestamp" em SQL Server). O valor desse campo de registro é definido como SQL_TRUE se a coluna é uma coluna de controle de versão de linha e SQL_FALSE caso contrário. Esse atributo de coluna é semelhante à chamada de **SQLSpecialColumns** com identificadortype de SQL_ROWVER para determinar se uma coluna é atualizada automaticamente.  
  
 **SQL_DESC_SCALE [todos]**  
 Este campo de registro SQLSMALLINT contém a escala definida para tipos de dados decimais e numéricos. O campo é indefinido para todos os outros tipos de dados.  
  
 O valor nesse campo pode ser diferente do valor de "Scale", conforme definido no ODBC 2 *. x*. Para obter mais informações, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome do esquema da tabela base que contém a coluna. O valor de retorno será dependente de driver se a coluna for uma expressão ou se a coluna fizer parte de uma exibição. Se a fonte de dados não oferecer suporte a esquemas ou se não for possível determinar o nome do esquema, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 Esse campo de registro SQLSMALLINT somente leitura é definido como um dos seguintes valores:  
  
-   SQL_PRED_NONE se a coluna não puder ser usada em uma cláusula **Where** . (É o mesmo que o valor de SQL_UNSEARCHABLE no ODBC 2 *. x*.)  
  
-   SQL_PRED_CHAR se a coluna puder ser usada em uma cláusula **Where** , mas somente com o predicado **like** . (É o mesmo que o valor de SQL_LIKE_ONLY no ODBC 2 *. x*.)  
  
-   SQL_PRED_BASIC se a coluna puder ser usada em uma cláusula **Where** com todos os operadores de comparação, exceto **como**. (É o mesmo que o valor de SQL_EXCEPT_LIKE no ODBC 2 *. x*.)  
  
-   SQL_PRED_SEARCHABLE se a coluna puder ser usada em uma cláusula **Where** com qualquer operador de comparação.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome da tabela base que contém essa coluna. O valor de retorno será dependente de driver se a coluna for uma expressão ou se a coluna fizer parte de uma exibição.  
  
 **SQL_DESC_TYPE [todos]**  
 Este campo de registro SQLSMALLINT especifica o tipo de dados conciso SQL ou C para todos os tipos de dados, exceto os tipos de dados DateTime e Interval. Para os tipos de dados DateTime e Interval, esse campo especifica o tipo de dados detalhado, que é SQL_DATETIME ou SQL_INTERVAL.  
  
 Sempre que este campo contiver SQL_DATETIME ou SQL_INTERVAL, o campo SQL_DESC_DATETIME_INTERVAL_CODE deverá conter o subcódigo apropriado para o tipo conciso. Para tipos de dados DateTime, SQL_DESC_TYPE contém SQL_DATETIME e o campo SQL_DESC_DATETIME_INTERVAL_CODE contém um subcódigo para o tipo de dados DateTime específico. Para tipos de dados de intervalo, SQL_DESC_TYPE contém SQL_INTERVAL e o campo SQL_DESC_DATETIME_INTERVAL_CODE contém um subcódigo para o tipo de dados intervalo específico.  
  
 Os valores nos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE são interdependentes. Cada vez que um dos campos é definido, o outro também deve ser definido. SQL_DESC_TYPE pode ser definido por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE pode ser definido por uma chamada para **SQLBindCol** ou **SQLBindParameter**, ou **SQLSetDescField**.  
  
 Se SQL_DESC_TYPE for definido como um tipo de dados conciso diferente de um tipo de dados de intervalo ou DateTime, o campo SQL_DESC_CONCISE_TYPE será definido com o mesmo valor e o campo SQL_DESC_DATETIME_INTERVAL_CODE será definido como 0.  
  
 Se SQL_DESC_TYPE for definido como o tipo de dados DateTime ou intervalo Detalhado (SQL_DATETIME ou SQL_INTERVAL) e o campo SQL_DESC_DATETIME_INTERVAL_CODE for definido como o subcódigo apropriado, o campo tipo de SQL_DESC_CONCISE será definido como o tipo conciso correspondente. Tentar definir SQL_DESC_TYPE como um dos tipos de DateTime ou de intervalo concisos retornará SQLSTATE HY021 (informações de descritor inconsistentes).  
  
 Quando o campo SQL_DESC_TYPE é definido por uma chamada para **SQLBindCol**, **SQLBindParameter**ou **SQLSetDescField**, os campos a seguir são definidos com os valores padrão a seguir, conforme mostrado na tabela a seguir. Os valores dos campos restantes do mesmo registro são indefinidos.  
  
|Valor de SQL_DESC_TYPE|Outros campos definidos implicitamente|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR SQL_C_VARCHAR|SQL_DESC_LENGTH é definido como 1. SQL_DESC_PRECISION é definido como 0.|  
|SQL_DATETIME|Quando SQL_DESC_DATETIME_INTERVAL_CODE é definido como SQL_CODE_DATE ou SQL_CODE_TIME, SQL_DESC_PRECISION é definido como 0. Quando definido como SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION é definido como 6.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE é definido como 0. SQL_DESC_PRECISION é definido como a precisão definida pela implementação para o respectivo tipo de dados.<br /><br /> Consulte [SQL to C: numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md) para obter informações sobre como associar manualmente um valor de SQL_C_NUMERIC.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION é definido como a precisão padrão definida pela implementação para SQL_FLOAT.|  
|SQL_INTERVAL|Quando SQL_DESC_DATETIME_INTERVAL_CODE é definido como um tipo de dados de intervalo, SQL_DESC_DATETIME_INTERVAL_PRECISION é definido como 2 (a precisão inicial do intervalo padrão). Quando o intervalo tiver um componente de segundos, SQL_DESC_PRECISION será definido como 6 (a precisão de segundos de intervalo padrão).|  
  
 Quando um aplicativo chama **SQLSetDescField** para definir campos de um descritor em vez de chamar **SQLSetDescRec**, o aplicativo deve primeiro declarar o tipo de dados. Quando ele faz, os outros campos indicados na tabela anterior são definidos implicitamente. Se qualquer um dos valores definidos implicitamente for inaceitável, o aplicativo poderá chamar **SQLSetDescField** ou **SQLSetDescRec** para definir o valor inaceitável explicitamente.  
  
 **SQL_DESC_TYPE_NAME [descritores de implementação]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome do tipo dependente da fonte de dados (por exemplo, "CHAR", "VARCHAR" e assim por diante). Se o nome do tipo de dados for desconhecido, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_UNNAMED [descritores de implementação]**  
 Esse campo de registro SQLSMALLINT em um descritor de linha é definido pelo driver para SQL_NAMED ou SQL_UNNAMED quando ele define o campo SQL_DESC_NAME. Se o campo SQL_DESC_NAME contiver um alias de coluna ou se o alias da coluna não se aplicar, o driver definirá o campo SQL_DESC_UNNAMED como SQL_NAMED. Se um aplicativo definir o SQL_DESC_NAME campo de um IPD para um nome de parâmetro ou alias, o driver definirá o SQL_DESC_UNNAMED campo do IPD como SQL_NAMED. Se não houver nenhum nome de coluna ou um alias de coluna, o driver definirá o campo SQL_DESC_UNNAMED como SQL_UNNAMED.  
  
 Um aplicativo pode definir o SQL_DESC_UNNAMED campo de um IPD para SQL_UNNAMED. Um driver retorna SQLSTATE HY091 (identificador de campo de descritor inválido) se um aplicativo tentar definir o SQL_DESC_UNNAMED campo de um IPD para SQL_NAMED. O campo SQL_DESC_UNNAMED de um IRD é somente leitura; SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado se um aplicativo tentar defini-lo.  
  
 **SQL_DESC_UNSIGNED [descritores de implementação]**  
 Esse campo de registro SQLSMALLINT somente leitura será definido como SQL_TRUE se o tipo de coluna for não assinado ou não numérico, ou SQL_FALSE se o tipo de coluna for assinado.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 Esse campo de registro SQLSMALLINT somente leitura é definido como um dos seguintes valores:  
  
-   SQL_ATTR_READ_ONLY se a coluna do conjunto de resultados for somente leitura.  
  
-   SQL_ATTR_WRITE se a coluna do conjunto de resultados for de leitura/gravação.  
  
-   SQL_ATTR_READWRITE_UNKNOWN se não for conhecido se a coluna do conjunto de resultados é atualizável ou não.  
  
 SQL_DESC_UPDATABLE descreve a capacidade de atualização da coluna no conjunto de resultados, não a coluna na tabela base. A capacidade de atualização da coluna na tabela base na qual essa coluna do conjunto de resultados é baseada pode ser diferente do valor nesse campo. A possibilidade de uma coluna ser atualizável pode ser baseada no tipo de dados, nos privilégios de usuário e na definição do próprio conjunto de resultados. Se não estiver claro se uma coluna é atualizável, SQL_ATTR_READWRITE_UNKNOWN deve ser retornado.  
  
## <a name="consistency-checks"></a>Verificações de consistência  
 Uma verificação de consistência é executada automaticamente pelo driver sempre que um aplicativo passa um valor para o campo SQL_DESC_DATA_PTR do ARD, APD ou IPD. Se qualquer um dos campos estiver inconsistente com outros campos, **SQLSetDescField** retornará SQLSTATE HY021 (informações de descritor inconsistentes). Para obter mais informações, consulte "verificação de consistência" em [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Associando um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtendo um campo de descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Referência de API do ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)
