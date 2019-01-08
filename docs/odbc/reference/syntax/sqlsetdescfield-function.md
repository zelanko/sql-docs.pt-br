---
title: Função SQLSetDescField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8704d28fb8ae39cf7d8f6bb595c884b70a6721a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204155"
---
# <a name="sqlsetdescfield-function"></a>Função SQLSetDescField
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLSetDescField** define o valor de um único campo de um registro do descritor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Identificador do descritor.  
  
 *RecNumber*  
 [Entrada] Indica que o registro de descritor que contém o campo que o aplicativo tenta definir. Registros de descritor são numerados de 0, com o número de registro que está sendo o registro de indicador de 0. O *RecNumber* argumento é ignorado para campos de cabeçalho.  
  
 *FieldIdentifier*  
 [Entrada] Indica o campo do descritor cujo valor deve ser definido. Para obter mais informações, consulte "*FieldIdentifier* argumento" na seção "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para um buffer que contém as informações do descritor ou um valor inteiro. O tipo de dados depende do valor de *FieldIdentifier*. Se *ValuePtr* é um valor inteiro, ele pode ser considerado como 8 bytes (SQLLEN), 4 bytes (sqlinteger que contém) ou 2 bytes (SQLSMALLINT), dependendo do valor da *FieldIdentifier* argumento.  
  
 *BufferLength*  
 [Entrada] Se *FieldIdentifier* é um campo definido pelo ODBC e *ValuePtr* aponta para uma cadeia de caracteres ou um buffer de binário, este argumento deve ser o comprimento de **ValuePtr*. Para dados de cadeia de caracteres, esse argumento deve conter o número de bytes na cadeia de caracteres.  
  
 Se *FieldIdentifier* é um campo definido pelo ODBC e *ValuePtr* é um inteiro *BufferLength* será ignorado.  
  
 Se *FieldIdentifier* é um campo definido pelo driver, o aplicativo indica a natureza do campo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma cadeia de caracteres, em seguida, *BufferLength* é o comprimento da cadeia de caracteres ou SQL_NTS.  
  
-   Se *ValuePtr* é um ponteiro para um buffer de binário, em seguida, o aplicativo coloca o resultado do SQL_LEN_BINARY_ATTR (*comprimento*) macro na *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma cadeia de caracteres ou uma cadeia de caracteres binária, em seguida, *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *ValuePtr* contiver um valor de comprimento fixo, então *BufferLength* é SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLSetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e uma *manipular* dos *DescriptorHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLSetDescField** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opção alterado|O driver não oferecia suporte para o valor especificado na  *\*ValuePtr* (se *ValuePtr* é um ponteiro) ou o valor na *ValuePtr* (se *ValuePtr*  era um valor inteiro), ou  *\*ValuePtr* era inválido devido a condições de trabalho de implementação, portanto, o driver substituído um valor semelhante. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O *FieldIdentifier* argumento era um campo de registro, o *RecNumber* argumento era 0 e o *DescriptorHandle* argumento chamado um identificador IPD.<br /><br /> O *RecNumber* argumento era menor que 0 e o *DescriptorHandle* argumento chamado um descartar ou um APD.<br /><br /> O *RecNumber* argumento era maior que o número máximo de colunas ou parâmetros que pode dar suporte a fonte de dados, e o *DescriptorHandle* argumento chamado um APD ou descartar.<br /><br /> (DM) a *FieldIdentifier* argumento era SQL_DESC_COUNT, e  *\*ValuePtr* argumento era menor que 0.<br /><br /> O *RecNumber* argumento era igual a 0 e o *DescriptorHandle* argumento chamado um APD implicitamente alocado. (Esse erro não ocorre com um descritor de aplicativo explicitamente alocados, porque ele não se sabe se um descritor de aplicativo explicitamente alocados é um APD ou descartar até executar tempo.)|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22001|Dados de cadeia de caracteres truncados à direita|O *FieldIdentifier* argumento era SQL_DESC_NAME e o *BufferLength* argumento era um valor maior que SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY010|Erro de sequência de função|(DM) a *DescriptorHandle* foi associada com um *StatementHandle* para que uma função de execução assíncrona (não esta uma) foi chamada e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* com a qual o *DescriptorHandle* foi associado e retornou SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *DescriptorHandle*. Essa função assíncrona ainda estava em execução quando o **SQLSetDescField** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para uma das alças de instrução associadas com o *DescriptorHandle* e retornado SQL_PARAM_DATA_AVAILABLE. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY016|Não é possível modificar um descritor de linha de implementação|O *DescriptorHandle* argumento foi associado um IRD e o *FieldIdentifier* argumento não era SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Informações do descritor inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo ODBC SQL válido ou um tipo válido de SQL específica do driver (para IPDs) ou um tipo válido do ODBC C (para APDs ou ARDs).<br /><br /> Informações de descritor verificadas durante uma verificação de consistência não eram consistentes. (Consulte "Verificação de consistência" na **SQLSetDescRec**.)|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM)  *\*ValuePtr* é uma cadeia de caracteres, e *BufferLength* é menor que zero, mas não era igual a SQL_NTS.<br /><br /> (DM) o driver foi um ODBC 2 *. x* driver, o descritor foi um descartar o *ColumnNumber* argumento foi definido como 0 e o valor especificado para o argumento *BufferLength* foi não é igual a 4.|  
|HY091|Identificador de campo de descritor inválido|O valor especificado para o *FieldIdentifier* argumento não era um campo definido pelo ODBC e não era um valor definido pela implementação.<br /><br /> O *FieldIdentifier* argumento era inválido para o *DescriptorHandle* argumento.<br /><br /> O *FieldIdentifier* argumento era um campo somente leitura e definido pelo ODBC.|  
|HY092|Identificador de atributo/opção inválido|O valor em  *\*ValuePtr* não era válido para o *FieldIdentifier* argumento.<br /><br /> O *FieldIdentifier* argumento era SQL_DESC_UNNAMED, e *ValuePtr* foi SQL_NAMED.|  
|HY105|Tipo de parâmetro inválido|(DM) o valor especificado para o campo SQL_DESC_PARAMETER_TYPE era inválido. (Para obter mais informações, consulte o "*InputOutputType* argumento" seção **SQLBindParameter**.)|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [o que há de novo no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *DescriptorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetDescField** para definir qualquer campo de descritor um por vez. Uma chamada para **SQLSetDescField** define um único campo em um único descritor. Essa função pode ser chamado para definir qualquer campo em qualquer tipo de descritor, fornecido que o campo pode ser definido. (Consulte a tabela nesta seção).  
  
> [!NOTE]  
>  Se uma chamada para **SQLSetDescField** falhar, o conteúdo do registro do descritor identificado pelo *RecNumber* argumento são indefinidos.  
  
 Outras funções podem ser chamadas para definir vários campos de descritor com uma única chamada da função. O **SQLSetDescRec** função define uma variedade de campos que afetam o buffer e o tipo de dados associados a uma coluna ou parâmetro (o SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL _ Campos DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR). **SQLBindCol** ou **SQLBindParameter** pode ser usado para fazer uma especificação completa para a associação de uma coluna ou parâmetro. Essas funções definem um grupo específico de campos de descritor com uma chamada de função.  
  
 **SQLSetDescField** pode ser chamado para alterar os buffers de associação, adicionando um deslocamento para os ponteiros de associação (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR ou SQL_DESC_OCTET_LENGTH_PTR). Isso altera os buffers de associação sem chamar **SQLBindCol** ou **SQLBindParameter**, que permite que um aplicativo alterar SQL_DESC_DATA_PTR sem alterar outros campos, como SQL_DESC_DATA_ TIPO.  
  
 Se um aplicativo chamar **SQLSetDescField** para definir qualquer campo que não seja SQL_DESC_COUNT ou campos adiados SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR ou SQL_DESC_INDICATOR_PTR, o registro se torna não associado.  
  
 Campos de cabeçalho do descritor são definidos chamando **SQLSetDescField** com os devidos *FieldIdentifier*. Vários campos de cabeçalho também são atributos de instrução, portanto, eles também podem ser definidos por uma chamada para **SQLSetStmtAttr**. Isso permite que aplicativos definam um campo de descritor sem primeiro obter um identificador do descritor. Quando **SQLSetDescField** é chamado para definir um campo de cabeçalho, o *RecNumber* argumento será ignorado.  
  
 Um *RecNumber* 0 é usado para definir campos de indicador.  
  
> [!NOTE]  
>  O atributo de instrução SQL_ATTR_USE_BOOKMARKS sempre deve ser definido antes de chamar **SQLSetDescField** definir campos de indicador. Embora não seja obrigatório, é altamente recomendável.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Sequência de campos de descritor de configuração  
 Ao definir campos de descritor chamando **SQLSetDescField**, o aplicativo deve seguir uma sequência específica:  
  
1.  O aplicativo deve primeiro definir o campo SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE ou SQL_DESC_DATETIME_INTERVAL_CODE.  
  
2.  Depois que um desses campos tiver sido definido, o aplicativo pode definir um atributo de tipo de dados e o driver define os campos de atributo tipo de dados para os valores padrão apropriados para o tipo de dados. Padronizando automática dos campos de atributo de tipo garante que o descritor sempre está pronto para ser usado depois que o aplicativo tiver especificado um tipo de dados. Se o aplicativo define explicitamente um atributo de tipo de dados, ela estará substituindo o atributo padrão.  
  
3.  Depois que um dos campos listados na etapa 1 foi definido e atributos de tipo de dados tiverem sido definidos, o aplicativo pode definir SQL_DESC_DATA_PTR. Isso inicia uma verificação de consistência de campos de descritor. Se o aplicativo altera o tipo de dados ou atributos depois de definir o campo SQL_DESC_DATA_PTR, o driver define SQL_DESC_DATA_PTR para um ponteiro nulo, desvinculando o registro. Isso força o aplicativo para concluir as etapas apropriadas em sequência, antes do registro de descritor é utilizável.  
  
## <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor  
 Quando um descritor é alocado, os campos no descritor de podem ser inicializados com um valor padrão, ser inicializados sem um valor padrão ou ser indefinido para o tipo de descritor. As tabelas a seguir indicam que a inicialização de cada campo para cada tipo de descritor, com "D" indicando que o campo é inicializado com um padrão e "ND" indicando que o campo for inicializado sem um padrão. Se um número é exibido, o valor padrão do campo é esse número. As tabelas também indicam se um campo é somente leitura (R) ou leitura/gravação (R/W).  
  
 Os campos de um IRD têm um valor padrão somente depois que a instrução tiver sido preparada ou executada e o IRD foi populado, não quando o identificador de instrução ou o descritor foi alocado. Até que o IRD foi populado, qualquer tentativa de obter acesso a um campo de um IRD retornará um erro.  
  
 Alguns campos de descritor são definidos para um ou mais, mas não todos, dos tipos de descritor (ARDs e IRDs e APDs e IPDs). Quando um campo é indefinido para um tipo de descritor, ela não é necessária por qualquer uma das funções que usam esse descritor.  
  
 Os campos que podem ser acessados por **SQLGetDescField** necessariamente não pode ser definido **SQLSetDescField**. Campos que podem ser definidos por **SQLSetDescField** estão listados nas tabelas a seguir.  
  
 A inicialização de campos de cabeçalho é descrita na tabela a seguir.  
  
|Nome do campo de cabeçalho|Tipo|R/W|Padrão|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|DESCARTAR: R APD: R IRD: R IPD: R|DESCARTAR: SQL_DESC_ALLOC_AUTO para implícita ou SQL_DESC_ALLOC_USER para explícita<br /><br /> APD: SQL_DESC_ALLOC_AUTO para implícita ou SQL_DESC_ALLOC_USER para explícita<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|DESCARTAR: R/W APD: R/W IRD: Não utilizado IPD: Não usado|DESCARTAR: APD [1]: [1] IRD: Não utilizado IPD: Não usado|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|DESCARTAR: R/W APD: R/W IRD: R/W IPD: R/W|DESCARTAR: Ptr nulo APD: Ptr nulo IRD: Ptr nulo IPD: Ptr nulo|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|DESCARTAR: R/W APD: R/W IRD: Não utilizado IPD: Não usado|DESCARTAR: Ptr nulo APD: Ptr nulo IRD: Não utilizado IPD: Não usado|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|DESCARTAR: R/W APD: R/W IRD: Não utilizado IPD: Não usado|DESCARTAR: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: Não usado<br /><br /> IPD: Não usado|  
SQL_DESC_COUNT|SQLSMALLINT|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD 0: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|DESCARTAR: APD não utilizado: Não utilizado IRD: R/W IPD: R/W|DESCARTAR: APD não utilizado: Não utilizado IRD: Ptr nulo IPD: Ptr nulo|  
  
 [1] esses campos são definidos somente quando o IPD é preenchida automaticamente pelo driver. Se não estiver, eles são indefinidos. Se um aplicativo tenta definir esses campos, SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado.  
  
 A inicialização de campos de registro é conforme mostrado na tabela a seguir.  
  
|Nome do campo de registro|Tipo|R/W|Padrão|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: 1!D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: SQL_C_ APD DO PADRÃO: SQL_C_ IRD DO PADRÃO: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|DESCARTAR: R/W APD: R/W IRD: Não utilizado IPD: Não usado|DESCARTAR: Ptr nulo APD: Ptr nulo IRD: Não utilizado IPD: Não utilizado de [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
SQL_DESC_DISPLAY_SIZE|SQLLEN|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: 1!D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|DESCARTAR: R/W APD: R/W IRD: Não utilizado IPD: Não usado|DESCARTAR: Ptr nulo APD: Ptr nulo IRD: Não utilizado IPD: Não usado|  
|SQL_DESC_LABEL|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_LENGTH|SQLULEN|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: 1!D [1]|  
|SQL_DESC_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
SQL_DESC_OCTET_LENGTH|SQLLEN|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|DESCARTAR: R/W APD: R/W IRD: Não utilizado IPD: Não usado|DESCARTAR: Ptr nulo APD: Ptr nulo IRD: Não utilizado IPD: Não usado|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: Não utilizado IPD: R/W|DESCARTAR: APD não utilizado: Não utilizado IRD: Não utilizado IPD: 1!D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|DESCARTAR: Não usado<br /><br /> APD: Não usado<br /><br /> IRD: R<br /><br /> IPD: R|DESCARTAR: Não usado<br /><br /> APD: Não usado<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
|SQL_DESC_TYPE|SQLSMALLINT|DESCARTAR: R/W APD: R/W IRD: R IPD: R/W|DESCARTAR: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
SQL_DESC_TYPE_NAME|SQLCHAR *|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: 1!D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R/W|DESCARTAR: APD ND: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: R|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: 1!D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|DESCARTAR: APD não utilizado: Não utilizado IRD: R IPD: Não usado|DESCARTAR: APD não utilizado: Não utilizado IRD: D IPD: Não usado|  
  
 [1] esses campos são definidos somente quando o IPD é preenchida automaticamente pelo driver. Se não estiver, eles são indefinidos. Se um aplicativo tenta definir esses campos, SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado.  
  
 [2], o campo SQL_DESC_DATA_PTR em IPD pode ser definido para forçar uma verificação de consistência. Em uma chamada subsequente para **SQLGetDescField** ou **SQLGetDescRec**, o driver não é necessário para retornar o valor SQL_DESC_DATA_PTR estava definido como.  
  
## <a name="fieldidentifier-argument"></a>Argumento FieldIdentifier  
 O *FieldIdentifier* argumento indica o campo do descritor a ser definido. Contém um descritor do *cabeçalho de descritor* consiste em campos de cabeçalho de descrito na próxima seção, "Campos do cabeçalho" e zero ou mais *registros de descritor* consiste nos campos de registro descrito na seção a seguir a seção "Campos do cabeçalho".  
  
## <a name="header-fields"></a>Campos de cabeçalho  
 Cada descritor tem um cabeçalho que consiste dos seguintes campos:  
  
 **SQL_DESC_ALLOC_TYPE [All]**  
 Este campo de cabeçalho SQLSMALLINT somente leitura Especifica se o descritor foi alocado automaticamente pelo driver ou explicitamente pelo aplicativo. O aplicativo pode obter, mas não modificar esse campo. O campo é definido como SQL_DESC_ALLOC_AUTO pelo driver, se o descritor foi alocado automaticamente pelo driver. Ele é definido como SQL_DESC_ALLOC_USER pelo driver se o descritor explicitamente foi alocado pelo aplicativo.  
  
 **SQL_DESC_ARRAY_SIZE [descritores de aplicativo]**  
 Em ARDs, esse campo de cabeçalho SQLULEN Especifica o número de linhas no conjunto de linhas. Este é o número de linhas a serem retornados por uma chamada para **SQLFetch** ou **SQLFetchScroll** ou a ser operado por uma chamada a **SQLBulkOperations** ou **SQLSetPos** .  
  
 Em APDs, esse campo de cabeçalho SQLULEN Especifica o número de valores para cada parâmetro.  
  
 O valor padrão desse campo é 1. Se SQL_DESC_ARRAY_SIZE for maior que 1, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR do APD ou descartar apontam para matrizes. A cardinalidade de cada matriz é igual ao valor desse campo.  
  
 Esse campo na descartar também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_ARRAY_SIZE. Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAMSET_SIZE.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [All]**  
 Para cada tipo de descritor, este SQLUSMALLINT * pontos de campo de cabeçalho para uma matriz de valores SQLUSMALLINT. Essas matrizes são nomeadas da seguinte maneira: matriz de status de (IRD), a matriz de status de parâmetro (IPD), a matriz de operação de linha (descartar) e a matriz de operação de parâmetro (APD) de linha.  
  
 No IRD, esse campo de cabeçalho aponta para uma matriz de status de linha que contém os valores de status após uma chamada para **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos**. A matriz tem o máximo de elementos existem linhas no conjunto de linhas. O aplicativo deve alocar uma matriz de SQLUSMALLINTs e defina esse campo para apontar para a matriz. O campo é definido como um ponteiro nulo por padrão. O driver preencherá a matriz - a menos que o campo SQL_DESC_ARRAY_STATUS_PTR é definido como um ponteiro nulo, caso em que nenhum valor de status é gerados e a matriz não é preenchida.  
  
> [!CAUTION]  
>  Comportamento do driver é indefinido se o aplicativo define os elementos da matriz de status de linha apontado pelo campo SQL_DESC_ARRAY_STATUS_PTR do IRD.  
  
 Inicialmente, a matriz é preenchida por uma chamada para **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos**. Se a chamada não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo da matriz apontado por este campo é indefinido. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_ROW_SUCCESS: A linha foi obtida com êxito e não foi alterado desde que foi buscada pela última vez.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: A linha foi obtida com êxito e não foi alterado desde que foi buscada pela última vez. No entanto, um aviso sobre a linha foi retornado.  
  
-   SQL_ROW_ERROR: Ocorreu um erro ao buscar a linha.  
  
-   SQL_ROW_UPDATED: A linha foi obtida com êxito e foi atualizada desde que foi buscada pela última vez. Se a linha é buscada novamente, seu status é SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: A linha foi excluída desde que foi buscada pela última vez.  
  
-   SQL_ROW_ADDED: A linha foi inserida pela **SQLBulkOperations**. Se a linha é buscada novamente, seu status é SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: O conjunto de linhas sobrepostas final do conjunto de resultados e nenhuma linha foi retornada que correspondeu a esse elemento da matriz de status de linha.  
  
 Esse campo do IRD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_STATUS_PTR.  
  
 O campo SQL_DESC_ARRAY_STATUS_PTR do IRD é válido somente depois que foi retornada SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO. Se o código de retorno não é um deles, o local apontado pela SQL_DESC_ROWS_PROCESSED_PTR é indefinido.  
  
 No IPD, esse campo de cabeçalho aponta para uma matriz de status de parâmetro que contém informações de status para cada conjunto de valores de parâmetro após uma chamada para **SQLExecute** ou **SQLExecDirect**. Se a chamada para **SQLExecute** ou **SQLExecDirect** não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo da matriz apontado por este campo são indefinidos. O aplicativo deve alocar uma matriz de SQLUSMALLINTs e defina esse campo para apontar para a matriz. O driver preencherá a matriz - a menos que o campo SQL_DESC_ARRAY_STATUS_PTR é definido como um ponteiro nulo, caso em que nenhum valor de status é gerados e a matriz não é preenchida. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_PARAM_SUCCESS: A instrução SQL foi executada com êxito para esse conjunto de parâmetros.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: A instrução SQL foi executada com êxito para esse conjunto de parâmetros. No entanto, informações de aviso estão disponíveis na estrutura de dados de diagnóstico.  
  
-   SQL_PARAM_ERROR: Ocorreu um erro ao processar este conjunto de parâmetros. Informações de erro adicionais estão disponíveis na estrutura de dados de diagnóstico.  
  
-   SQL_PARAM_UNUSED: Esse conjunto de parâmetros foi não utilizado, possivelmente devido ao fato de que algum conjunto de parâmetros anteriores causou um erro que anulado processamento adicional ou porque SQL_PARAM_IGNORE foi definido para esse conjunto de parâmetros da matriz especificado pelo campo SQL_DESC_ARRAY_STATUS_PTR de APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: Informações de diagnóstico não estão disponíveis. Um exemplo disso é quando o driver trata as matrizes de parâmetros como uma unidade monolítica e, portanto, não gera esse nível de informações de erro.  
  
 Esse campo em IPD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 Descartar, esse campo de cabeçalho aponta para uma matriz de operação de linha de valores que podem ser definidas pelo aplicativo para indicar se essa linha deve ser ignorado para **SQLSetPos** operações. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_ROW_PROCEED: A linha é incluída na operação em massa usando **SQLSetPos**. (Essa configuração não garante que a operação ocorrerá na linha. Se a linha tem o status SQL_ROW_ERROR na matriz de status de linha de IRD, o driver pode não ser capaz de executar a operação na linha.)  
  
-   SQL_ROW_IGNORE: A linha é excluída da operação em massa usando **SQLSetPos**.  
  
 Se nenhum elemento da matriz forem definido, todas as linhas serão incluídas na operação em massa. Se o valor no campo SQL_DESC_ARRAY_STATUS_PTR da descartar for um ponteiro nulo, todas as linhas são incluídas na operação em massa; a interpretação é o mesmo como se o ponteiro apontado para uma matriz válida e todos os elementos da matriz foram SQL_ROW_PROCEED. Se um elemento na matriz é definido como SQL_ROW_IGNORE, o valor na matriz de status de linha para a linha ignorada não é alterado.  
  
 Esse campo na descartar também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 Em APD, esse campo de cabeçalho aponta para uma matriz de parâmetros de operação de valores que podem ser definidas pelo aplicativo para indicar se este conjunto de parâmetros deve ser ignorada quando **SQLExecute** ou **SQLExecDirect**é chamado. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_PARAM_PROCEED: O conjunto de parâmetros está incluído na **SQLExecute** ou **SQLExecDirect** chamar.  
  
-   SQL_PARAM_IGNORE: O conjunto de parâmetros é excluído dos **SQLExecute** ou **SQLExecDirect** chamar.  
  
 Caso nenhum elemento da matriz forem definido, todos os conjuntos de parâmetros na matriz são usados a **SQLExecute** ou **SQLExecDirect** chamadas. Se o valor no campo SQL_DESC_ARRAY_STATUS_PTR de APD for um ponteiro nulo, todos os conjuntos de parâmetros são usados; a interpretação é o mesmo como se o ponteiro apontado para uma matriz válida e todos os elementos da matriz foram SQL_PARAM_PROCEED.  
  
 Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [descritores de aplicativo]**  
 Este SQLLEN * pontos de campo de cabeçalho para o deslocamento de associação. Ele é definido como um ponteiro nulo por padrão. Se esse campo não for um ponteiro nulo, o driver cancelará o ponteiro e adiciona o valor cancelado a cada um dos campos adiados que tem um valor não nulo no registro do descritor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) ao busca tempo e usa os novos valores de ponteiro ao associar.  
  
 O deslocamento de associação sempre é adicionado diretamente para os valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se o deslocamento for alterado para um valor diferente, o novo valor é adicionado diretamente ao valor em cada campo de descritor. O novo deslocamento não é adicionado ao valor do campo e qualquer deslocamento anterior.  
  
 Este campo é um *campo adiado*: Ele não é usado no momento, ele é definido, mas é usado em um momento posterior pelo driver quando ele precisa determinar endereços para buffers de dados.  
  
 Esse campo na descartar também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_BIND_OFFSET_PTR. Esse campo na descartar também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Para obter mais informações, consulte a descrição da associação por linha na [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) e [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [descritores de aplicativo]**  
 Este campo de cabeçalho SQLUINTEGER define a orientação de associação a ser usado para colunas ou parâmetros de associação.  
  
 No ARDs, este campo especifica a orientação de associação quando **SQLFetchScroll** ou **SQLFetch** é chamado no identificador de instrução associado.  
  
 Para selecionar a associação por coluna para colunas, esse campo é definido como SQL_BIND_BY_COLUMN (o padrão).  
  
 Esse campo na descartar também pode ser definido chamando **SQLSetStmtAttr** com o SQL_ATTR_ROW_BIND_TYPE *atributo*.  
  
 Em APDs, este campo especifica a orientação de associação a ser usado para parâmetros dinâmicos.  
  
 Para selecionar a associação de parâmetros, esse campo é definido como SQL_BIND_BY_COLUMN (o padrão).  
  
 Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o SQL_ATTR_PARAM_BIND_TYPE *atributo*.  
  
 **SQL_DESC_COUNT [All]**  
 Este campo de cabeçalho SQLSMALLINT Especifica o índice baseado em 1 do registro de número mais alto que contém dados. Quando o driver define a estrutura de dados para o descritor, ele também deve definir o campo SQL_DESC_COUNT para mostrar quantos registros são significativo. Quando um aplicativo aloca uma instância dessa estrutura de dados, ele não precisa especificar quantos registros para reservar espaço para. Como o aplicativo especifica os conteúdos dos registros, o driver usa todas as ações necessárias para garantir que o identificador do descritor se refere a uma estrutura de dados do tamanho adequado.  
  
 SQL_DESC_COUNT não é uma contagem de todas as colunas de dados que são associadas (se o campo estiver em um descartar) ou de todos os parâmetros que são associados (se o campo estiver em um APD), mas o número do registro de número mais alto. Se o parâmetro ou coluna de número mais alto é desvinculado, SQL_DESC_COUNT é alterado para o número da próxima coluna de número mais alto ou parâmetro. Se uma coluna ou um parâmetro com um número que é menor que o número da coluna de número mais alto é não associado (chamando **SQLBindCol** com o *TargetValuePtr* argumento definido como um ponteiro nulo ou **SQLBindParameter** com o *ParameterValuePtr* argumento definido como um ponteiro nulo), SQL_DESC_COUNT não é alterado. Se parâmetros ou colunas adicionais são associados com números maiores que o registro de número mais alto que contém os dados, o driver automaticamente aumenta o valor do campo SQL_DESC_COUNT. Se todas as colunas são desassociadas chamando **SQLFreeStmt** com a opção SQL_UNBIND, os campos SQL_DESC_COUNT no descartar e IRD são definidos como 0. Se **SQLFreeStmt** é chamado com a opção SQL_RESET_PARAMS, os campos SQL_DESC_COUNT no APD e IPD são definidos como 0.  
  
 O valor em SQL_DESC_COUNT pode ser definido explicitamente por um aplicativo chamando **SQLSetDescField**. Se o valor em SQL_DESC_COUNT explicitamente é reduzido, todos os registros com números maiores que o novo valor na SQL_DESC_COUNT efetivamente serão removidos. Se o valor em SQL_DESC_COUNT é definido explicitamente como 0 e o campo estiver em um descartar, todos os buffers de dados, exceto uma coluna de indicador associado são liberados.  
  
 A contagem de registros nesse campo de um descartar não inclui uma coluna de indicador associado. A única maneira de desassociar uma coluna de indicador é definir o campo SQL_DESC_DATA_PTR para um ponteiro nulo.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [descritores de implementação]**  
 Em um IRD, esse SQLULEN \* pontos de campo de cabeçalho para um buffer que contém o número de linhas buscadas após uma chamada para **SQLFetch** ou **SQLFetchScroll**, ou o número de linhas afetadas em uma operação em massa executado por uma chamada para **SQLBulkOperations** ou **SQLSetPos**, inclusive as linhas de erro.  
  
 Em um IPD, este SQLUINTEGER * pontos de campo de cabeçalho para um buffer que contém o número de conjuntos de parâmetros que foram processados, incluindo conjuntos de erro. Nenhum número será retornado se esse for um ponteiro nulo.  
  
 SQL_DESC_ROWS_PROCESSED_PTR é válido somente depois que foi retornada SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO após uma chamada para **SQLFetch** ou **SQLFetchScroll** (para um campo de IRD) ou **SQLExecute** , **SQLExecDirect**, ou **SQLParamData** (para um campo de IPD). Se a chamada que preenche o buffer apontado por este campo não retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer é indefinido, a menos que ele retornar SQL_NO_DATA, caso o valor no buffer é definido como 0.  
  
 Esse campo na descartar também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROWS_FETCHED_PTR. Esse campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAMS_PROCESSED_PTR.  
  
 O buffer apontado por este campo é alocado pelo aplicativo. É um buffer de saída adiada é definido pelo driver. Ele é definido como um ponteiro nulo por padrão.  
  
## <a name="record-fields"></a>Campos de registro  
 Cada descritor contém um ou mais registros que consiste de campos que definem os dados da coluna ou parâmetros dinâmicos, dependendo do tipo de descritor. Cada registro é uma definição completa de uma única coluna ou parâmetro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 Este campo de registro sqlinteger que contém somente leitura contém SQL_TRUE se a coluna for uma coluna de incremento automático ou SQL_FALSE se a coluna não é uma coluna de incremento automático. Este campo é somente leitura, mas a coluna de incremento automático subjacente não é necessariamente somente leitura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 Este SQLCHAR somente leitura * campo registro contém o nome da coluna de base para o resultado do conjunto de coluna. Se não existir um nome de coluna de base (como no caso de colunas que são expressões), essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 Este SQLCHAR somente leitura * campo registro contém o nome da tabela base para o resultado do conjunto de coluna. Se um nome de tabela base não pode ser definido ou não é aplicável, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_CASE_SENSITIVE [descritores de implementação]**  
 Este campo de registro sqlinteger que contém somente leitura contém SQL_TRUE se a coluna ou parâmetro é tratado como diferencia maiusculas de minúsculas para agrupamentos e comparações ou SQL_FALSE se a coluna não é tratada como diferencia maiusculas de minúsculas para agrupamentos e comparações ou se ele for um tipo não caractere coluna.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 Este SQLCHAR somente leitura * campo registro contém o catálogo para a tabela base que contém a coluna. O valor de retorno é dependente do driver, se a coluna é uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não dá suporte a catálogos ou o catálogo não pode ser determinado, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_CONCISE_TYPE [All]**  
 Este campo de cabeçalho SQLSMALLINT Especifica o tipo de dados concisa para todos os tipos de dados, incluindo os tipos de dados de data e hora e intervalo.  
  
 Os valores nos campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE são interdependentes. Cada vez que um dos campos é definido, o outro também deve ser definido. SQL_DESC_CONCISE_TYPE pode ser definido por uma chamada para **SQLBindCol** ou **SQLBindParameter**, ou **SQLSetDescField**. SQL_DESC_TYPE pode ser definido por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se SQL_DESC_CONCISE_TYPE for definido como um tipo de dados concisa que não seja um tipo de dados de intervalo ou de data/hora, o campo SQL_DESC_TYPE é definido com o mesmo valor e o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido como 0.  
  
 Se SQL_DESC_CONCISE_TYPE for definido como o tipo de dados datetime ou intervalo conciso, o campo SQL_DESC_TYPE é definido para o tipo correspondente de detalhado (SQL_DATETIME ou SQL_INTERVAL) e o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido para o subcódigo apropriado.  
  
 **SQL_DESC_DATA_PTR [descritores de aplicativo e IPDs]**  
 Este campo de registro SQLPOINTER aponta para uma variável que conterá o valor do parâmetro (para APDs) ou o valor da coluna (para ARDs). Este campo é um *campo adiado*. Ele não é usado no momento, ele é definido, mas é usado em um momento posterior pelo driver para recuperar dados.  
  
 A coluna especificada pelo campo SQL_DESC_DATA_PTR da descartar é não associada, se o *TargetValuePtr* argumento em uma chamada para **SQLBindCol** for um ponteiro nulo ou se o SQL_DESC_DATA_PTR campo na descartar é definido por um chamada para **SQLSetDescField** ou **SQLSetDescRec** como um ponteiro nulo. Outros campos não são afetados se o campo SQL_DESC_DATA_PTR é definido como um ponteiro nulo.  
  
 Se a chamada para **SQLFetch** ou **SQLFetchScroll** que preenche o buffer apontado por este campo não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer é indefinido.  
  
 Sempre que o campo SQL_DESC_DATA_PTR de APD, descartar ou IPD for definido, o driver verifica que o valor no campo SQL_DESC_TYPE contém um dos tipos de dados ODBC C válidos ou um tipo de dados específicos do driver e que todos os outros campos que afetam os tipos de dados são consistentes. Solicitar uma verificação de consistência é o uso apenas do campo SQL_DESC_DATA_PTR de um IPD. Especificamente, se um aplicativo define o campo SQL_DESC_DATA_PTR um IPD e chamadas posteriores **SQLGetDescField** esse campo, ele não é necessariamente retornado o valor que ele tinha definido. Para obter mais informações, consulte "Verificações de consistência" na [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [All]**  
 Este campo de registro SQLSMALLINT contém o subcódigo para o tipo de dados datetime ou intervalo específico quando o campo SQL_DESC_TYPE for SQL_DATETIME ou SQL_INTERVAL. Isso é verdadeiro para tipos de dados SQL e C. O código consiste do nome do tipo de dados com "Código" substituídos por "Tipo" ou "C_TYPE" (para tipos de data e hora) ou "Código" substituídos por "Intervalo" ou "C_INTERVAL" (para tipos de intervalo).  
  
 Se SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE em um descritor de aplicativo são definidos como SQL_C_DEFAULT e o descritor não está associado um identificador de instrução, o conteúdo de SQL_DESC_DATETIME_INTERVAL_CODE é indefinido.  
  
 Este campo pode ser definido para os tipos de dados de data e hora listados na tabela a seguir.  
  
|Tipos de data e hora|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP / SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Este campo pode ser definido para os tipos de dados de intervalo listados na tabela a seguir.  
  
|Tipo de intervalo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR / SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE / SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND / SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
QL_INTERVAL_HOUR_TO_MINUTE / SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE / SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND / SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
QL_INTERVAL_SECOND / SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Para obter mais informações sobre os intervalos de dados e esse campo, consulte [Data Type Identifiers and Descriptors](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [All]**  
 Este campo de registro de sqlinteger que contém contém o intervalo de precisão inicial se o campo SQL_DESC_TYPE for SQL_INTERVAL. Quando o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido como um tipo de dados de intervalo, esse campo é definido como o intervalo padrão de precisão inicial.  
  
 **Colunas de SQL_DESC_DISPLAY_SIZE [IRDs]**  
 Este campo de registro sqlinteger que contém somente leitura contém o número máximo de caracteres necessários para exibir os dados da coluna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [descritores de implementação]**  
 Esse campo de registro SQLSMALLINT somente leitura é definido como SQL_TRUE se a coluna é uma coluna numérica exata e tem uma precisão fixa e uma escala diferente de zero, ou para SQL_FALSE se a coluna não é uma coluna de numérica exata com uma precisão e escala fixas.  
  
 **SQL_DESC_INDICATOR_PTR [descritores de aplicativo]**  
 No ARDs, este SQLLEN * registrar pontos de campo para a variável de indicador. Essa variável contém SQL_NULL_DATA se o valor da coluna for um valor nulo. Para APDs, a variável de indicador é definida como SQL_NULL_DATA para especificar os argumentos dinâmicos de NULL. Caso contrário, a variável é zero (a menos que os valores em SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR são o mesmo ponteiro).  
  
 Se o campo SQL_DESC_INDICATOR_PTR um descartar for um ponteiro nulo, o driver será impedido de retornando informações sobre se a coluna é NULL ou não. Se a coluna for NULL e SQL_DESC_INDICATOR_PTR for um ponteiro nulo, SQLSTATE 22002 (variável de indicador necessária, mas não fornecida) é retornado quando o driver tenta preencher o buffer após uma chamada para **SQLFetch** ou  **SQLFetchScroll**. Se a chamada para **SQLFetch** ou **SQLFetchScroll** não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer são indefinidos.  
  
 O campo SQL_DESC_INDICATOR_PTR determina se o campo apontado pelo SQL_DESC_OCTET_LENGTH_PTR está definido. Se o valor de dados para uma coluna for NULL, o driver define a variável de indicador como SQL_NULL_DATA. O campo apontado pelo SQL_DESC_OCTET_LENGTH_PTR, em seguida, não é definido. Se um valor nulo não é encontrado durante a busca, o buffer apontado por SQL_DESC_INDICATOR_PTR é definido como zero e o buffer apontado por SQL_DESC_OCTET_LENGTH_PTR é definido como o comprimento dos dados.  
  
 Se o campo SQL_DESC_INDICATOR_PTR um APD for um ponteiro nulo, o aplicativo não é possível usar esse registro de descritor para especificar argumentos nulos.  
  
 Este campo é um *campo adiado*: Ele não é usado no momento, ele é definido, mas é usado em um momento posterior pelo driver para indicar a nulidade (para ARDs) ou para determinar a nulidade (para APDs).  
  
 **SQL_DESC_LABEL [IRDs]**  
 Este SQLCHAR somente leitura * campo registro contém o rótulo da coluna ou o título. Se a coluna não tiver um rótulo, essa variável contém o nome da coluna. Se a coluna for nomeada e sem rótulo, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_LENGTH [All]**  
 Este campo de registro SQLULEN é o comprimento máximo ou real de uma cadeia de caracteres em caracteres ou um tipo de dados binários em bytes. É o comprimento máximo para um tipo de dados de comprimento fixo ou o comprimento real para um tipo de dados de comprimento variável. Seu valor sempre exclui o caractere de terminação nula que encerra a cadeia de caracteres. Para valores cujo tipo é SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP ou um dos tipos de dados de intervalo de SQL, este campo tem o comprimento em caracteres do que a representação de cadeia de caracteres do valor datetime ou intervalo.  
  
 O valor neste campo pode ser diferente do valor de "comprimento" como definido no ODBC 2 *. x*. Para obter mais informações, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 Este SQLCHAR somente leitura * campo de registro contém um ou mais caracteres que o driver reconhece como um prefixo para um literal deste tipo de dados. Essa variável conterá uma cadeia de caracteres vazia para um tipo de dados para o qual um prefixo de literal não é aplicável.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 Este SQLCHAR somente leitura * campo de registro contém um ou mais caracteres que o driver reconhece como um sufixo para um literal deste tipo de dados. Essa variável conterá uma cadeia de caracteres vazia para um tipo de dados para o qual um sufixo literal não é aplicável.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [descritores de implementação]**  
 Este SQLCHAR somente leitura * campo registro contém qualquer nome localizado (idioma nativo) para o tipo de dados que pode ser diferente do nome do tipo de dados regular. Se não houver nenhum nome localizado, uma cadeia de caracteres vazia é retornada. Este campo é somente para exibição.  
  
 **SQL_DESC_NAME [descritores de implementação]**  
 Este SQLCHAR * campo de registro em um descritor de linha contém o alias de coluna, se aplicável. Se o alias de coluna não for aplicável, o nome da coluna será retornado. Em ambos os casos, o driver define o campo SQL_DESC_UNNAMED para SQL_NAMED quando ela define o campo SQL_DESC_NAME. Se não houver nenhum nome de coluna ou um alias de coluna, o driver retorna uma cadeia de caracteres vazia no campo SQL_DESC_NAME e define o campo SQL_DESC_UNNAMED para SQL_UNNAMED.  
  
 Um aplicativo pode definir o campo SQL_DESC_NAME de um IPD para um nome de parâmetro ou um alias para especificar parâmetros de procedimento armazenado pelo nome. (Para obter mais informações, consulte [associando parâmetros por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) O campo SQL_DESC_NAME de um IRD é um campo somente leitura; SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado se um aplicativo tentar defini-lo.  
  
 No IPDs, este campo é indefinido se o driver não dá suporte a parâmetros nomeados. Se o driver dá suporte a parâmetros nomeados e é capaz de descrever os parâmetros, o nome do parâmetro será retornado nesse campo.  
  
 **SQL_DESC_NULLABLE [descritores de implementação]**  
 Em IRDs, esse campo de registro SQLSMALLINT somente leitura é SQL_NULLABLE se a coluna pode ter valores nulos, SQL_NO_NULLS se a coluna tiver valores NULL ou SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores nulos. Este campo referente a coluna de conjunto de resultados, não a coluna base.  
  
 Em IPDs, esse campo sempre é definido como SQL_NULLABLE porque parâmetros dinâmicos são sempre que permitem valor nulos e não podem ser definidos por um aplicativo.  
  
 **SQL_DESC_NUM_PREC_RADIX [All]**  
 Este campo sqlinteger que contém contém um valor de 2 se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico aproximado, porque o campo SQL_DESC_PRECISION contém o número de bits. Este campo contém um valor de 10, se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico exato, porque o campo SQL_DESC_PRECISION contém o número de dígitos decimais. Esse campo é definido como 0 para todos os tipos de dados não numéricos.  
  
 **SQL_DESC_OCTET_LENGTH [All]**  
 Este campo de registro SQLLEN contém o comprimento, em bytes, de um tipo de dados binário ou cadeia de caracteres. Para caracteres de comprimento fixo ou tipos binários, esse é o comprimento real em bytes. Para o caractere de comprimento variável ou tipos binários, isso é o comprimento máximo em bytes. Esse valor sempre exclui espaço para o caractere nulo de terminação para descritores de implementação e sempre inclui espaço para o caractere nulo de terminação para descritores de aplicativo. Dados de aplicativos, esse campo contém o tamanho do buffer. Para APDs, esse campo é definido somente para parâmetros de entrada/saída ou de saída.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [descritores de aplicativo]**  
 Este SQLLEN * registrar pontos de campo a uma variável que conterá o tamanho total em bytes de um argumento dinâmico (para descritores de parâmetro) ou de um valor de coluna associada (para descritores de linha).  
  
 Para um APD, esse valor é ignorado para todos os argumentos, exceto a cadeia de caracteres e binários; Se esse campo apontar para SQL_NTS, o argumento dinâmico deve ser terminada em nulo. Para indicar que um parâmetro associado será um parâmetro de dados em execução, um aplicativo define esse campo no registro de APD apropriado para uma variável que, em tempo, de execução conterá o valor SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC . Se houver mais de um desses campos, SQL_DESC_DATA_PTR pode ser definido como um valor que identifica exclusivamente o parâmetro para o aplicativo determinar qual parâmetro está sendo solicitado.  
  
 Se o campo OCTET_LENGTH_PTR de um descartar for um ponteiro nulo, o driver não retorna informações de comprimento da coluna. Se o campo SQL_DESC_OCTET_LENGTH_PTR de um APD é um ponteiro nulo, o driver pressupõe que as cadeias de caracteres e valores binários terminada em nulo. (Valores binários não devem ser terminada em nulo, mas devem ser fornecidos um comprimento para evitar truncamento.)  
  
 Se a chamada para **SQLFetch** ou **SQLFetchScroll** que preenche o buffer apontado por este campo não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer é indefinido. Este campo é um *campo adiado*. Ele não é usado no momento, ele é definido, mas é usado em um momento posterior pelo driver para determinar ou indicar o comprimento do octeto de dados.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 Esse campo de registro SQLSMALLINT é definido como SQL_PARAM_INPUT para um parâmetro de entrada, SQL_PARAM_INPUT_OUTPUT para um parâmetro de entrada/saída, SQL_PARAM_OUTPUT para um parâmetro de saída, SQL_PARAM_INPUT_OUTPUT_STREAM para um parâmetro de entrada/saída transmitido ou SQL _ PARAM_OUTPUT_STREAM para um parâmetro de fluxo de saída. Ele é definido como SQL_PARAM_INPUT por padrão.  
  
 Para um IPD, o campo é definido como SQL_PARAM_INPUT por padrão se o IPD não é preenchida automaticamente com o driver (o atributo da instrução SQL_ATTR_ENABLE_AUTO_IPD é SQL_FALSE). Um aplicativo deve definir esse campo em IPD para parâmetros que não são parâmetros de entrada.  
  
 **SQL_DESC_PRECISION [All]**  
 Este campo de registro SQLSMALLINT contém o número de dígitos para um tipo numérico exato, o número de bits da mantissa (precisão binária) para um tipo numérico aproximado, ou o número de dígitos no componente de segundos fracionários para SQL_TYPE_TIME, SQL_TYPE _TIMESTAMP ou tipo de dados SQL_INTERVAL_SECOND. Este campo é indefinido para todos os outros tipos de dados.  
  
 O valor neste campo pode ser diferente do valor de "precisão" conforme definido no ODBC 2 *. x*. Para obter mais informações, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [descritores de implementação]**  
 Este campo SQLSMALLINTrecord indica se uma coluna é modificada automaticamente pelo DBMS quando uma linha é atualizada (por exemplo, uma coluna do tipo "timestamp" no SQL Server). O valor desse campo de registro é definido como SQL_TRUE se a coluna for uma coluna de controle de versão de linha e SQL_FALSE caso contrário. Esse atributo de coluna é semelhante a chamar **SQLSpecialColumns** com IdentifierType de SQL_ROWVER para determinar se uma coluna é atualizada automaticamente.  
  
 **SQL_DESC_SCALE [All]**  
 Este campo de registro SQLSMALLINT contém a escala definida para tipos de dados decimais e numéricos. O campo é indefinido para todos os outros tipos de dados.  
  
 O valor neste campo pode ser diferente do valor de "escala", conforme definido em 2 de ODBC *. x*. Para obter mais informações, consulte [apêndice d: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 Este SQLCHAR somente leitura * campo registro contém o nome do esquema da tabela base que contém a coluna. O valor de retorno é dependente do driver, se a coluna é uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não oferece suporte a esquemas ou o nome do esquema não pode ser determinado, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 Este campo de registro SQLSMALLINT somente leitura é definido como um dos seguintes valores:  
  
-   SQL_PRED_NONE se a coluna não pode ser usada em uma **onde** cláusula. (Isso é o mesmo que o valor SQL_UNSEARCHABLE no ODBC 2 *. x*.)  
  
-   SQL_PRED_CHAR se a coluna pode ser usada em uma **onde** cláusula, mas apenas com o **como** predicado. (Isso é o mesmo que o valor SQL_LIKE_ONLY no ODBC 2 *. x*.)  
  
-   SQL_PRED_BASIC se a coluna pode ser usada em uma **onde** cláusula com todos os operadores de comparação, exceto **como**. (Isso é o mesmo que o valor SQL_EXCEPT_LIKE no ODBC 2 *. x*.)  
  
-   SQL_PRED_SEARCHABLE se a coluna pode ser usada em uma **onde** cláusula com qualquer operador de comparação.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 Este SQLCHAR somente leitura * campo do registro contém o nome da tabela base que contém esta coluna. O valor de retorno é dependente do driver, se a coluna é uma expressão ou se a coluna faz parte de uma exibição.  
  
 **SQL_DESC_TYPE [All]**  
 Esse campo de registro SQLSMALLINT Especifica o tipo de dados SQL ou C conciso para todos os tipos de dados, exceto os tipos de dados de data e hora e intervalo. Para os tipos de dados de data e hora e intervalo, este campo especifica o tipo de dados detalhado, o que for SQL_DATETIME ou SQL_INTERVAL.  
  
 Sempre que esse campo contém SQL_DATETIME ou SQL_INTERVAL, o campo SQL_DESC_DATETIME_INTERVAL_CODE deve conter o subcódigo apropriado para o tipo conciso. Para tipos de dados de data e hora, SQL_DESC_TYPE contém SQL_DATETIME e o campo SQL_DESC_DATETIME_INTERVAL_CODE contém um subcódigo para o tipo de dados de data e hora específicas. Para tipos de dados de intervalo, SQL_DESC_TYPE contém SQL_INTERVAL e o campo SQL_DESC_DATETIME_INTERVAL_CODE contém um subcódigo para o tipo de dados de intervalo específico.  
  
 Os valores nos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE são interdependentes. Cada vez que um dos campos é definido, o outro também deve ser definido. SQL_DESC_TYPE pode ser definido por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE pode ser definido por uma chamada para **SQLBindCol** ou **SQLBindParameter**, ou **SQLSetDescField**.  
  
 Se SQL_DESC_TYPE for definido como um tipo de dados concisa que não seja um tipo de dados de intervalo ou de data/hora, o campo SQL_DESC_CONCISE_TYPE é definido com o mesmo valor e o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido como 0.  
  
 Se SQL_DESC_TYPE for definido como detalhado datetime ou tipo de dados de intervalo (SQL_DATETIME ou SQL_INTERVAL) e o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido para o subcódigo apropriado, o campo de tipo SQL_DESC_CONCISE é definido para o tipo conciso correspondente. Tentativa de definir SQL_DESC_TYPE para um dos tipos de data e hora ou intervalo concisos retornará SQLSTATE HY021 (informações do descritor inconsistentes).  
  
 Quando o campo SQL_DESC_TYPE é definido por uma chamada para **SQLBindCol**, **SQLBindParameter**, ou **SQLSetDescField**, os campos a seguir são definidos para os seguintes valores padrão, conforme mostrado na tabela a seguir. Os valores dos campos do mesmo registro restantes são indefinidos.  
  
|Valor de SQL_DESC_TYPE|Outros campos definidos implicitamente|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH é definido como 1. SQL_DESC_PRECISION é definido como 0.|  
|SQL_DATETIME|Quando SQL_DESC_DATETIME_INTERVAL_CODE é definido como SQL_CODE_DATE ou SQL_CODE_TIME, SQL_DESC_PRECISION é definido como 0. Quando ela é definida como SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION é definido como 6.|  
|SQL_C_NUMERIC SQL_DECIMAL, SQL_NUMERIC,|SQL_DESC_SCALE é definido como 0. SQL_DESC_PRECISION é definido como a precisão definido pela implementação para o tipo de dados respectivo.<br /><br /> Consulte [SQL to c: Numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md) para obter informações sobre como associar manualmente um valor SQL_C_NUMERIC.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION está definida como a precisão padrão definido pela implementação para SQL_FLOAT.|  
|SQL_INTERVAL|Quando SQL_DESC_DATETIME_INTERVAL_CODE é definida como um tipo de dados de intervalo, SQL_DESC_DATETIME_INTERVAL_PRECISION é definido como 2 (o padrão à esquerda precisão de intervalo). Quando o intervalo tem um componente de segundos, SQL_DESC_PRECISION é definido como 6 (o padrão intervalo precisão de segundos).|  
  
 Quando um aplicativo chama **SQLSetDescField** para definir campos de descritor em vez de chamar **SQLSetDescRec**, o aplicativo primeiro deve declarar o tipo de dados. Quando isso acontecer, os outros campos indicados na tabela anterior são definidos implicitamente. Se qualquer um dos valores implicitamente conjunto são inaceitáveis, o aplicativo pode, em seguida, chamar **SQLSetDescField** ou **SQLSetDescRec** para definir o valor inaceitável explicitamente.  
  
 **SQL_DESC_TYPE_NAME [descritores de implementação]**  
 Este SQLCHAR somente leitura * campo registro contém o nome de tipo dependente da fonte de dados ("por exemplo, CHAR", "VARCHAR" e assim por diante). Se o nome do tipo de dados for desconhecido, essa variável conterá uma cadeia de caracteres vazia.  
  
 **SQL_DESC_UNNAMED [descritores de implementação]**  
 Esse campo de registro SQLSMALLINT em um descritor de linha é definido pelo driver para SQL_NAMED ou SQL_UNNAMED quando ela define o campo SQL_DESC_NAME. Se o campo SQL_DESC_NAME contém um alias de coluna ou se o alias de coluna não se aplica, o driver define o campo SQL_DESC_UNNAMED para SQL_NAMED. Se um aplicativo define o campo SQL_DESC_NAME um IPD para um parâmetro de nome ou alias, o driver define campo de IPD SQL_DESC_UNNAMED para SQL_NAMED. Se não houver nenhum nome de coluna ou um alias de coluna, o driver define o campo SQL_DESC_UNNAMED para SQL_UNNAMED.  
  
 Um aplicativo pode definir o campo SQL_DESC_UNNAMED de um IPD para SQL_UNNAMED. Um driver retornará SQLSTATE HY091 (identificador de campo de descritor inválido) se um aplicativo tentar definir o campo SQL_DESC_UNNAMED de um IPD para SQL_NAMED. O campo SQL_DESC_UNNAMED de um IRD é somente leitura; SQLSTATE HY091 (identificador de campo de descritor inválido) será retornado se um aplicativo tentar defini-lo.  
  
 **SQL_DESC_UNSIGNED [descritores de implementação]**  
 Este campo de registro SQLSMALLINT somente leitura é definido como SQL_TRUE se o tipo de coluna é não assinado ou não numéricos, ou SQL_FALSE se o tipo de coluna é assinado.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 Este campo de registro SQLSMALLINT somente leitura é definido como um dos seguintes valores:  
  
-   SQL_ATTR_READ_ONLY se o conjunto de resultados coluna é somente leitura.  
  
-   SQL_ATTR_WRITE se o conjunto de resultados coluna é leitura / gravação.  
  
-   SQL_ATTR_READWRITE_UNKNOWN se não se sabe se o conjunto de resultados é atualizável ou não.  
  
 SQL_DESC_UPDATABLE descreve a capacidade de atualização de coluna no conjunto de resultados, não a coluna na tabela base. A capacidade de atualização da coluna na tabela base na qual se baseia essa coluna do conjunto de resultados pode ser diferente do valor nesse campo. Se uma coluna é atualizável pode ser com base no tipo de dados, privilégios de usuário e a definição do próprio conjunto de resultados. Se não está claro se uma coluna é atualizável, SQL_ATTR_READWRITE_UNKNOWN deve ser retornado.  
  
## <a name="consistency-checks"></a>Verificações de consistência  
 Uma verificação de consistência é executada pelo driver automaticamente sempre que um aplicativo transmita um valor para o campo SQL_DESC_DATA_PTR do IPD, APD ou descartar. Se qualquer um dos campos é inconsistente com outros campos, **SQLSetDescField** retornará SQLSTATE HY021 (informações do descritor inconsistentes). Para obter mais informações, consulte "Verificação de consistência" na [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Uma coluna de associação|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Um parâmetro de associação|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obter um campo de descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de descritor|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configurando vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Referência de API do ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)
