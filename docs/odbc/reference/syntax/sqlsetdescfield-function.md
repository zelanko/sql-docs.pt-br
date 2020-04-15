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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299546"
---
# <a name="sqlsetdescfield-function"></a>Função SQLSetDescField

**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLSetDescField** define o valor de um único campo de um registro descritor.  
  
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
 [Entrada] Alça do descritor.  
  
 *RecNumber*  
 [Entrada] Indica o registro descritor contendo o campo que o aplicativo procura definir. Os registros do descritor são numerados de 0, com o número recorde 0 sendo o recorde do marcador. O argumento *RecNumber* é ignorado para campos de cabeçalho.  
  
 *FieldIdentifier*  
 [Entrada] Indica o campo do descritor cujo valor deve ser definido. Para obter mais informações, consulte *"FieldIdentifier* Argument" na seção "Comentários".  
  
 *ValuePtr*  
 [Entrada] Ponteiro para um buffer contendo as informações do descritor ou um valor inteiro. O tipo de dados depende do valor do *FieldIdentifier*. Se *ValuePtr* for um valor inteiro, ele pode ser considerado como 8 bytes (SQLLEN), 4 bytes (SQLINTEGER) ou 2 bytes (SQLSMALLINT), dependendo do valor do argumento *FieldIdentifier.*  
  
 *BufferLength*  
 [Entrada] Se *fieldIdentifier* é um campo definido pelo ODBC e *ValuePtr* aponta para uma seqüência de caracteres ou um buffer binário, esse argumento deve ser o comprimento de **ValuePtr*. Para dados de seqüência de caracteres, este argumento deve conter o número de bytes na seqüência de caracteres.  
  
 Se *FieldIdentifier* é um campo definido pelo ODBC e *o ValuePtr* é um inteiro, *bufferLength* será ignorado.  
  
 Se *fieldIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength.* *BufferLength* pode ter os seguintes valores:  
  
-   Se *ValuePtr* é um ponteiro para uma seqüência de caracteres, então *BufferLength* é o comprimento da seqüência ou SQL_NTS.  
  
-   Se *ValuePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro SQL_LEN_BINARY_ATTR *(comprimento)* em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *ValuePtr* é um ponteiro para um valor diferente de uma seqüência de caracteres ou uma seqüência binária, então *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *o ValuePtr* contiver um valor de comprimento fixo, o *BufferLength* será SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT ou SQL_IS_USMALLINT, conforme apropriado.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLSetDescField** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_DESC e uma *alça* de *DscriptorHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLSetDescField** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor da opção alterado|O driver não suportava o valor especificado no * \*ValuePtr* (se *ValuePtr* era um ponteiro) ou o valor no *ValuePtr* (se *ValuePtr* era um valor inteiro), ou * \*valuePtr* era inválido devido às condições de trabalho de implementação, então o driver substituiu um valor semelhante. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07009|Índice de descritor inválido|O argumento *FieldIdentifier* era um campo de registro, o argumento *RecNumber* era 0 e o argumento *DscriptorHandle* referia-se a uma alça IPD.<br /><br /> O argumento *RecNumber* foi menor que 0, e o argumento *DescritorHandle* referia-se a um ARD ou a um APD.<br /><br /> O argumento *RecNumber* foi maior do que o número máximo de colunas ou parâmetros que a fonte de dados pode suportar, e o argumento *DescritorHandle* referido a um APD ou ARD.<br /><br /> (DM) O argumento *FieldIdentifier* foi SQL_DESC_COUNT, e * \*o argumento ValuePtr* foi menor que 0.<br /><br /> O argumento *RecNumber* era igual a 0, e o argumento *Discritoder* referia-se a uma APD implicitamente alocada. (Esse erro não ocorre com um descritor de aplicativo explicitamente alocado, porque não se sabe se um descritor de aplicativo alocado explicitamente é um APD ou ARD até a hora da execução.)|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22001|Dados de cordas, truncados direito|O argumento *FieldIdentifier* foi SQL_DESC_NAME, e o argumento *BufferLength* foi um valor maior do que SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY010|Erro de seqüência de função|(DM) O *DscriptorHandle* foi associado a um *StatementHandle* para o qual uma função de execução assíncrona (não esta) foi chamada e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* com o qual o *DscriptorHandle* foi associado e retornou SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *DscriptorHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLSetDescField** foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foi chamado para uma das alças de declaração associadas ao *DscriptorHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY016|Não é possível modificar um descritor de linha de implementação|O argumento *DscriptorHandle* foi associado a um IRD, e o argumento *FieldIdentifier* não foi SQL_DESC_ARRAY_STATUS_PTR ou SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Informações dedescritores inconsistentes|Os campos SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE não formam um tipo De SQL ODBC válido ou um tipo SQL específico para driver válido (para IPDs) ou um tipo C ODBC válido (para APDs ou ARDs).<br /><br /> As informações do descritor verificadas durante uma verificação de consistência não foram consistentes. (Consulte "Verificação de consistência" no **SQLSetDescRec**.)|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) * \*ValuePtr* é uma seqüência de caracteres, e *BufferLength* era menor que zero, mas não era igual a SQL_NTS.<br /><br /> (DM) O driver era um Driver ODBC 2 *.x,* o descritor era um ARD, o argumento *ColunaNúmero* foi definido como 0 e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY091|Identificador de campo de descritor inválido|O valor especificado para o argumento *FieldIdentifier* não era um campo definido pelo ODBC e não era um valor definido pela implementação.<br /><br /> O argumento *FieldIdentifier* era inválido para o argumento *DscriptorHandle.*<br /><br /> O argumento *FieldIdentifier* era um campo definido pela ODBC somente para leitura.|  
|HY092|Identificador de atributo/opção inválido|O valor no * \*ValuePtr* não era válido para o argumento *FieldIdentifier.*<br /><br /> O argumento *FieldIdentifier* foi SQL_DESC_UNNAMED, e *ValuePtr* foi SQL_NAMED.|  
|HY105|Tipo de parâmetro inválido|(DM) O valor especificado para o campo SQL_DESC_PARAMETER_TYPE era inválido. (Para obter mais informações, consulte a seção *"InputOutputType* Argument" no **SQLBindParameter**.)|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [O que há de novo na ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *DescritorHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 Um aplicativo pode chamar **SQLSetDescField** para definir qualquer campo descritor um de cada vez. Uma chamada para **SQLSetDescField** define um único campo em um único descritor. Esta função pode ser chamada para definir qualquer campo em qualquer tipo de descritor, desde que o campo possa ser definido. (Veja a tabela mais tarde nesta seção.)  
  
> [!NOTE]  
>  Se uma chamada para **SQLSetDescField** falhar, o conteúdo do registro descritor identificado pelo argumento *RecNumber* será indefinido.  
  
 Outras funções podem ser chamadas para definir vários campos descritores com uma única chamada da função. A função **SQLSetDescRec** define uma variedade de campos que afetam o tipo de dados e o buffer vinculados a uma coluna ou parâmetro (os campos SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_INDICATOR_PTR). **SQLBindCol** ou **SQLBindParameter** podem ser usados para fazer uma especificação completa para a vinculação de uma coluna ou parâmetro. Essas funções definem um grupo específico de campos descritores com uma chamada de função.  
  
 **SQLSetDescField** pode ser chamado para alterar os buffers de ligação adicionando uma compensação aos ponteiros de ligação (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR ou SQL_DESC_OCTET_LENGTH_PTR). Isso altera os buffers de vinculação sem chamar **SQLBindCol** ou **SQLBindParameter**, que permite que um aplicativo altere SQL_DESC_DATA_PTR sem alterar outros campos, como SQL_DESC_DATA_TYPE.  
  
 Se um aplicativo chamar **SQLSetDescField** para definir qualquer campo que não seja SQL_DESC_COUNT ou os campos diferidos SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR ou SQL_DESC_INDICATOR_PTR, o registro fica desvinculado.  
  
 Os campos de cabeçalho do descritor são definidos chamando **SQLSetDescField** com o *FieldIdentifier*apropriado . Muitos campos de cabeçalho também são atributos de declaração, de modo que eles também podem ser definidos por uma chamada para **SQLSetStmtAttr**. Isso permite que os aplicativos definam um campo descritor sem antes obter uma alça descritor. Quando **o SQLSetDescField** é chamado para definir um campo de cabeçalho, o argumento *RecNumber* é ignorado.  
  
 Um *RecNumber* de 0 é usado para definir campos de marcação.  
  
> [!NOTE]  
>  O atributo de declaração SQL_ATTR_USE_BOOKMARKS deve ser sempre definido antes de chamar **SQLSetDescField** para definir campos de marcação de marcação. Embora isso não seja obrigatório, é fortemente recomendado.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Seqüência de campos de descritor de configuração  
 Ao definir campos de descritores chamando **SQLSetDescField,** o aplicativo deve seguir uma seqüência específica:  
  
1.  A aplicação deve primeiro definir o campo SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE ou SQL_DESC_DATETIME_INTERVAL_CODE.  
  
2.  Depois que um desses campos for definido, o aplicativo pode definir um atributo de um tipo de dados e o driver define os campos de atributos do tipo de dados para os valores padrão apropriados para o tipo de dados. A inadimplência automática dos campos de atributos de tipo garante que o descritor esteja sempre pronto para ser usado depois que o aplicativo tiver especificado um tipo de dados. Se o aplicativo definir explicitamente um atributo de tipo de dados, ele será sobrepor o atributo padrão.  
  
3.  Depois que um dos campos listados na etapa 1 tiver sido definido e os atributos do tipo de dados tiverem sido definidos, o aplicativo pode definir SQL_DESC_DATA_PTR. Isso solicita uma verificação de consistência dos campos descritores. Se o aplicativo mudar o tipo de dados ou atributos após a definição do campo SQL_DESC_DATA_PTR, o driver definirá SQL_DESC_DATA_PTR para um ponteiro nulo, desvinculando o registro. Isso força a aplicação a concluir os passos apropriados em seqüência, antes que o registro do descritor seja utilizável.  
  
## <a name="initialization-of-descriptor-fields"></a>Inicialização de campos de descritor  
 Quando um descritor é alocado, os campos no descritor podem ser inicializados em um valor padrão, serem inicializados sem um valor padrão ou serem indefinidos para o tipo de descritor. As tabelas a seguir indicam a inicialização de cada campo para cada tipo de descritor, com "D" indicando que o campo é inicializado com um padrão, e "ND" indicando que o campo é inicializado sem um padrão. Se um número for mostrado, o valor padrão do campo é esse número. As tabelas também indicam se um campo é leitura/gravação (R/W) ou somente leitura (R).  
  
 Os campos de um IRD têm um valor padrão somente após a declaração ter sido preparada ou executada e o IRD tiver sido preenchido, não quando a alça da declaração ou descritor tiver sido alocado. Até que o IRD seja preenchido, qualquer tentativa de obter acesso a um campo de IRD retornará um erro.  
  
 Alguns campos descritores são definidos para um ou mais, mas não todos, dos tipos de descritores (ARDs e IRDs, e APDs e IPDs). Quando um campo é indefinido para um tipo de descritor, não é necessário por nenhuma das funções que usam esse descritor.  
  
 Os campos que podem ser acessados pelo **SQLGetDescField** não podem necessariamente ser definidos pelo **SQLSetDescField**. Os campos que podem ser definidos pelo **SQLSetDescField** estão listados nas tabelas a seguir.  
  
 A inicialização dos campos de cabeçalho é descrita na tabela a seguir.  
  
|Nome do campo de cabeçalho|Type|R/W|Padrão|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: SQL_DESC_ALLOC_AUTO para implícito ou SQL_DESC_ALLOC_USER para explícito<br /><br /> APD: SQL_DESC_ALLOC_AUTO para implícito ou SQL_DESC_ALLOC_USER para explícito<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD: R/W APD: R/W IRD: IPD não utilizado: Não utilizado|ARD:[1] APD:[1] IRD: IPD não utilizado: Não utilizado|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD: R/W APD: R/W IRD: R/W IPD: R/W|ARD: Null ptr APD: Null ptr IRD: Null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|ARD: R/W APD: R/W IRD: IPD não utilizado: Não utilizado|ARD: Null ptr APD: Null ptr IRD: IPD não utilizado: Não utilizado|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: IPD não utilizado: Não utilizado|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: Não utilizado<br /><br /> IPD: Não utilizado|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|ARD: APD não utilizado: IRD não utilizado: R/W IPD: R/W|ARD: APD não utilizado: IRD não utilizado: Null ptr IPD: Null ptr|  
  
 [1] Esses campos são definidos somente quando o IPD é preenchido automaticamente pelo driver. Se não, eles são indefinidos. Se um aplicativo tentar definir esses campos, o SQLSTATE HY091 (identificador de campo de descritor inválido) será devolvido.  
  
 A inicialização dos campos de registro é como mostrado na tabela a seguir.  
  
|Nome do campo de gravação|Type|R/W|Padrão|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_ APD PADRÃO: SQL_C_ IRD PADRÃO: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD: R/W APD: R/W IRD: IPD não utilizado: Não utilizado|ARD: Null ptr APD: Null ptr IRD: IPD não utilizado: Não utilizado[2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: IPD não utilizado: Não utilizado|ARD: Null ptr APD: Null ptr IRD: IPD não utilizado: Não utilizado|  
|SQL_DESC_LABEL|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_LENGTH|SQLULEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D[1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: IPD não utilizado: Não utilizado|ARD: Null ptr APD: Null ptr IRD: IPD não utilizado: Não utilizado|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: IPD não utilizado: R/W|ARD: APD não utilizado: IRD não utilizado: IPD não utilizado: D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: Não utilizado<br /><br /> APD: Não utilizado<br /><br /> IRD: R<br /><br /> IPD: R|ARD: Não utilizado<br /><br /> APD: Não utilizado<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: R|ARD: APD não utilizado: IRD não utilizado: D IPD: D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: APD não utilizado: IRD não utilizado: R IPD: Não utilizado|ARD: APD não utilizado: IRD não utilizado: D IPD: Não utilizado|  
  
 [1] Esses campos são definidos somente quando o IPD é preenchido automaticamente pelo driver. Se não, eles são indefinidos. Se um aplicativo tentar definir esses campos, o SQLSTATE HY091 (identificador de campo de descritor inválido) será devolvido.  
  
 [2] O campo SQL_DESC_DATA_PTR no IPD pode ser definido para forçar uma verificação de consistência. Em uma chamada subseqüente para **SQLGetDescField** ou **SQLGetDescRec,** o driver não é obrigado a devolver o valor que SQL_DESC_DATA_PTR foi definido.  
  
## <a name="fieldidentifier-argument"></a>Argumento identificador de campo  
 O argumento *FieldIdentifier* indica que o campo descritor a ser definido. Um descritor contém o *cabeçalho do descritor,* consistindo dos campos de cabeçalho descritos na próxima seção, "Campos de cabeçalho", e zero ou mais *registros descritores,* consistindo dos campos de registro descritos na seção seguinte à seção "Campos de cabeçalho".  
  
## <a name="header-fields"></a>Campos de cabeçalho  
 Cada descritor tem um cabeçalho composto pelos seguintes campos:  
  
 **SQL_DESC_ALLOC_TYPE [Todos]**  
 Este campo de cabeçalho SQLSMALLINT somente leitura especifica se o descritor foi alocado automaticamente pelo driver ou explicitamente pelo aplicativo. O aplicativo pode obter, mas não modificar, este campo. O campo é definido para SQL_DESC_ALLOC_AUTO pelo motorista se o descritor foi automaticamente alocado pelo motorista. Ele é definido para SQL_DESC_ALLOC_USER pelo motorista se o descritor foi explicitamente alocado pelo aplicativo.  
  
 **SQL_DESC_ARRAY_SIZE [Descritores de aplicativos]**  
 Em ARDs, este campo de cabeçalho SQLULEN especifica o número de linhas no conjunto de linhas. Este é o número de linhas a serem retornadas por uma chamada para **SQLFetch** ou **SQLFetchScroll** ou para serem operadas por uma chamada para **SQLBulkOperations** ou **SQLSetPos**.  
  
 Em APDs, este campo de cabeçalho SQLULEN especifica o número de valores para cada parâmetro.  
  
 O valor padrão deste campo é 1. Se SQL_DESC_ARRAY_SIZE for maior que 1, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR do APD ou ARD apontar para matrizes. A cardinalidade de cada matriz é igual ao valor deste campo.  
  
 Este campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_ARRAY_SIZE. Este campo na APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAMSET_SIZE.  
  
 **SQL_DESC_ARRAY_STATUS_PTR**  
 Para cada tipo de descritor, este campo de cabeçalho SQLUSMALLINT * aponta para uma matriz de valores SQLUSMALLINT. Essas matrizes são nomeadas da seguinte forma: matriz de status de linha (IRD), matriz de status de parâmetro (IPD), matriz de operação de linha (ARD) e matriz de operação de parâmetros (APD).  
  
 No IRD, este campo de cabeçalho aponta para uma matriz de status de linha contendo valores de status após uma chamada para **SQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos**. A matriz tem tantos elementos quanto há linhas no conjunto de linhas. O aplicativo deve alocar uma matriz de SQLUSMALLINTs e definir este campo para apontar para a matriz. O campo é definido como um ponteiro nulo por padrão. O driver preencherá a matriz - a menos que o campo SQL_DESC_ARRAY_STATUS_PTR esteja definido como um ponteiro nulo, nesse caso, nenhum valor de status é gerado e a matriz não é preenchida.  
  
> [!CAUTION]  
>  O comportamento do driver é indefinido se o aplicativo define os elementos da matriz de status da linha apontados pelo campo SQL_DESC_ARRAY_STATUS_PTR do IRD.  
  
 A matriz é inicialmente preenchida por uma chamada para **SQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos**. Se a chamada não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo da matriz apontada por este campo será indefinido. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_ROW_SUCCESS: A fila foi buscada com sucesso e não mudou desde a última vez que foi buscada.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: A fila foi buscada com sucesso e não mudou desde a última vez que foi buscada. No entanto, um aviso foi devolvido sobre a linha.  
  
-   SQL_ROW_ERROR: Ocorreu um erro ao buscar a linha.  
  
-   SQL_ROW_UPDATED: A fila foi buscada com sucesso e foi atualizada desde a última vez que foi buscada. Se a linha for buscada novamente, seu status é SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: A linha foi excluída desde a última vez que foi buscada.  
  
-   SQL_ROW_ADDED: A linha foi inserida pela **SQLBulkOperations**. Se a linha for buscada novamente, seu status é SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: O conjunto de linhas sobrepôs-se ao final do conjunto de resultados, e nenhuma linha foi devolvida que correspondia a este elemento da matriz de status da linha.  
  
 Este campo no IRD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_STATUS_PTR.  
  
 O campo SQL_DESC_ARRAY_STATUS_PTR do IRD só é válido após SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO ter sido devolvido. Se o código de devolução não for um desses, o local apontado por SQL_DESC_ROWS_PROCESSED_PTR é indefinido.  
  
 No IPD, este campo de cabeçalho aponta para um conjunto de status de parâmetro contendo informações de status para cada conjunto de valores de parâmetroapós uma chamada para **SQLExecute** ou **SQLExecDirect**. Se a chamada para **SQLExecute** ou **SQLExecDirect** não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo da matriz apontada por este campo será indefinido. O aplicativo deve alocar uma matriz de SQLUSMALLINTs e definir este campo para apontar para a matriz. O driver preencherá a matriz - a menos que o campo SQL_DESC_ARRAY_STATUS_PTR esteja definido como um ponteiro nulo, nesse caso, nenhum valor de status é gerado e a matriz não é preenchida. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_PARAM_SUCCESS: A declaração SQL foi executada com sucesso para este conjunto de parâmetros.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: A declaração SQL foi executada com sucesso para este conjunto de parâmetros; no entanto, as informações de alerta estão disponíveis na estrutura de dados de diagnóstico.  
  
-   SQL_PARAM_ERROR: Ocorreu um erro no processamento desse conjunto de parâmetros. Informações adicionais de erro estão disponíveis na estrutura de dados de diagnóstico.  
  
-   SQL_PARAM_UNUSED: Este conjunto de parâmetros não foi utilizado, possivelmente devido ao fato de que algum conjunto de parâmetros anteriores causou um erro que abortou o processamento adicional, ou porque SQL_PARAM_IGNORE foi definido para esse conjunto de parâmetros na matriz especificada pelo campo de SQL_DESC_ARRAY_STATUS_PTR da APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: As informações de diagnóstico não estão disponíveis. Um exemplo disso é quando o driver trata matrizes de parâmetros como uma unidade monolítica e, portanto, não gera esse nível de informação de erro.  
  
 Este campo no IPD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 No ARD, este campo de cabeçalho aponta para uma matriz de valores de operação de linha que pode ser definida pelo aplicativo para indicar se essa linha deve ser ignorada para operações **SQLSetPos.** Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_ROW_PROCEED: A linha está incluída na operação em massa usando **SQLSetPos**. (Esta configuração não garante que a operação ocorrerá na linha. Se a linha tiver o status SQL_ROW_ERROR na matriz de status da linha IRD, o driver pode não ser capaz de executar a operação na linha.)  
  
-   SQL_ROW_IGNORE: A linha está excluída da operação em massa usando **SQLSetPos**.  
  
 Se nenhum elemento da matriz for definido, todas as linhas serão incluídas na operação em massa. Se o valor no campo SQL_DESC_ARRAY_STATUS_PTR do ARD for um ponteiro nulo, todas as linhas serão incluídas na operação em massa; a interpretação é a mesma que se o ponteiro apontasse para uma matriz válida e todos os elementos da matriz fossem SQL_ROW_PROCEED. Se um elemento na matriz estiver definido como SQL_ROW_IGNORE, o valor na matriz de status da linha para a linha ignorada não será alterado.  
  
 Este campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 Na APD, este campo de cabeçalho aponta para um conjunto de valores de operação de parâmetros que podem ser definidos pelo aplicativo para indicar se esse conjunto de parâmetros deve ser ignorado quando **SQLExecute** ou **SQLExecDirect** for chamado. Os elementos na matriz podem conter os seguintes valores:  
  
-   SQL_PARAM_PROCEED: O conjunto de parâmetros está incluído na chamada **SQLExecute** ou **SQLExecDirect.**  
  
-   SQL_PARAM_IGNORE: O conjunto de parâmetros é excluído da chamada **SQLExecute** ou **SQLExecDirect.**  
  
 Se nenhum elemento da matriz for definido, todos os conjuntos de parâmetros na matriz serão usados nas chamadas **SQLExecute** ou **SQLExecDirect.** Se o valor no campo SQL_DESC_ARRAY_STATUS_PTR da APD for um ponteiro nulo, todos os conjuntos de parâmetros serão utilizados; a interpretação é a mesma que se o ponteiro apontasse para uma matriz válida e todos os elementos da matriz fossem SQL_PARAM_PROCEED.  
  
 Este campo na APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [Descritores de aplicativos]**  
 Este campo de cabeçalho SQLLEN * aponta para o deslocamento de vinculação. Ele é definido como um ponteiro nulo por padrão. Se este campo não for um ponteiro nulo, o driver defaz referência ao ponteiro e adiciona o valor dereferência a cada um dos campos diferidos que tem um valor não nulo no registro do descritor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR) na hora da busca e usa os novos valores de ponteiro quando vinculados.  
  
 A compensação vinculante é sempre adicionada diretamente aos valores nos campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR. Se a compensação for alterada para um valor diferente, o novo valor ainda será adicionado diretamente ao valor em cada campo descritor. O novo deslocamento não é adicionado ao valor de campo mais qualquer deslocamento anterior.  
  
 Este campo é um *campo diferido*: Ele não é usado no momento em que é definido, mas é usado posteriormente pelo driver quando ele precisa determinar endereços para buffers de dados.  
  
 Este campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROW_BIND_OFFSET_PTR. Este campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Para obter mais informações, consulte a descrição da vinculação em sentido de linha no [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) e [no SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [Descritores de aplicativos]**  
 Este campo de cabeçalho SQLUINTEGER define a orientação de vinculação a ser usada para vincular colunas ou parâmetros.  
  
 Em ARDs, este campo especifica a orientação de vinculação quando **SQLFetchScroll** ou **SQLFetch** é chamado na alça de declaração associada.  
  
 Para selecionar a vinculação em termos de coluna para colunas, este campo está definido como SQL_BIND_BY_COLUMN (o padrão).  
  
 Este campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o *atributo*SQL_ATTR_ROW_BIND_TYPE .  
  
 Em APDs, este campo especifica a orientação de vinculação a ser usada para parâmetros dinâmicos.  
  
 Para selecionar a vinculação em termos de coluna para parâmetros, este campo está definido como SQL_BIND_BY_COLUMN (o padrão).  
  
 Este campo no APD também pode ser definido chamando **SQLSetStmtAttr** com o *atributo*SQL_ATTR_PARAM_BIND_TYPE .  
  
 **SQL_DESC_COUNT [Todos]**  
 Este campo de cabeçalho SQLSMALLINT especifica o índice baseado em 1 do registro de maior numeração que contém dados. Quando o driver define a estrutura de dados para o descritor, ele também deve definir o campo SQL_DESC_COUNT para mostrar quantos registros são significativos. Quando um aplicativo aloca uma instância dessa estrutura de dados, ele não precisa especificar quantos registros reservar espaço. Como o aplicativo especifica o conteúdo dos registros, o motorista toma todas as medidas necessárias para garantir que a alça do descritor se refira a uma estrutura de dados do tamanho adequado.  
  
 SQL_DESC_COUNT não é uma contagem de todas as colunas de dados que estão vinculadas (se o campo estiver em um ARD) ou de todos os parâmetros que estão vinculados (se o campo estiver em uma APD), mas o número do registro mais numerado. Se a coluna ou parâmetro mais numerado estiver desvinculado, SQL_DESC_COUNT será alterado para o número da próxima coluna ou parâmetro numerado mais alto. Se uma coluna ou um parâmetro com um número menor que o número mais alto da coluna numerada estiver desvinculado (ligando para **SQLBindCol** com o argumento *TargetValuePtr* definido como um ponteiro nulo ou **SQLBindParameter** com o argumento *ParameterValuePtr* definido como um ponteiro nulo), SQL_DESC_COUNT não for alterada. Se colunas ou parâmetros adicionais estiverem vinculados a números superiores ao registro de maior número que contém dados, o driver aumentará automaticamente o valor no campo SQL_DESC_COUNT. Se todas as colunas estiverem desvinculadas ligando para **SQLFreeStmt** com a opção SQL_UNBIND, os campos SQL_DESC_COUNT no ARD e no IRD serão definidos como 0. Se **o SQLFreeStmt** for chamado com a opção SQL_RESET_PARAMS, os campos SQL_DESC_COUNT no APD e IPD serão definidos como 0.  
  
 O valor em SQL_DESC_COUNT pode ser definido explicitamente por um aplicativo ligando para **SQLSetDescField**. Se o valor em SQL_DESC_COUNT for explicitamente reduzido, todos os registros com números maiores que o novo valor em SQL_DESC_COUNT são efetivamente removidos. Se o valor em SQL_DESC_COUNT for explicitamente definido como 0 e o campo estiver em um ARD, todos os buffers de dados, exceto uma coluna de marcadores vinculada, serão liberados.  
  
 A contagem de registros neste campo de ARD não inclui uma coluna de marcadores vinculada. A única maneira de desvincular uma coluna de marcadores é definir o campo SQL_DESC_DATA_PTR para um ponteiro nulo.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [Descritores de implementação]**  
 Em um IRD, este \* campo de cabeçalho SQLULEN aponta para um buffer contendo o número de linhas buscadas após uma chamada para **SQLFetch** ou **SQLFetchScroll,** ou o número de linhas afetadas em uma operação em massa realizada por uma chamada para **SQLBulkOperations** ou **SQLSetPos,** incluindo linhas de erro.  
  
 Em um IPD, este campo de cabeçalho SQLUINTEGER * aponta para um buffer contendo o número de conjuntos de parâmetros que foram processados, incluindo conjuntos de erros. Nenhum número será devolvido se este for um ponteiro nulo.  
  
 SQL_DESC_ROWS_PROCESSED_PTR só é válido depois que SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO for em após uma chamada para **SQLFetch** ou **SQLFetchScroll** (para um campo IRD) ou **SQLExecute,** **SQLExecDirect**ou **SQLParamData** (para um campo IPD). Se a chamada que preenche o buffer apontado por este campo não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido, a menos que ele retorne SQL_NO_DATA, nesse caso o valor no buffer é definido como 0.  
  
 Este campo no ARD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_ROWS_FETCHED_PTR. Este campo na APD também pode ser definido chamando **SQLSetStmtAttr** com o atributo SQL_ATTR_PARAMS_PROCESSED_PTR.  
  
 O buffer apontado por este campo é alocado pela aplicação. É um buffer de saída diferido que é definido pelo driver. Ele é definido como um ponteiro nulo por padrão.  
  
## <a name="record-fields"></a>Campos de Registro  
 Cada descritor contém um ou mais registros compostos por campos que definem dados de coluna ou parâmetros dinâmicos, dependendo do tipo de descritor. Cada registro é uma definição completa de uma única coluna ou parâmetro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 Este campo de registro SQLINTEGER somente leitura contém SQL_TRUE se a coluna for uma coluna de incrementamento automático ou SQL_FALSE se a coluna não for uma coluna de incrementamento automático. Este campo é somente leitura, mas a coluna de incrementamento automático subjacente não é necessariamente somente leitura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome da coluna base para a coluna conjunto de resultados. Se um nome de coluna base não existir (como no caso de colunas que são expressões), esta variável contém uma seqüência de string vazia.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome da tabela base para a coluna conjunto de resultados. Se um nome de tabela base não puder ser definido ou não for aplicável, esta variável contém uma seqüência de string vazia.  
  
 **SQL_DESC_CASE_SENSITIVE [Descritores de implementação]**  
 Este campo de registro SQLINTEGER somente leitura contém SQL_TRUE se a coluna ou parâmetro for tratado como sensível a maiúsculas e minúsculas para colagens e comparações, ou SQL_FALSE se a coluna não for tratada como sensível a maiúsculas e outras para colagens e comparações ou se for uma coluna sem caracteres.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o catálogo da tabela base que contém a coluna. O valor de devolução é dependente do driver se a coluna for uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não suportar catálogos ou o catálogo não puder ser determinado, esta variável contém uma seqüência de string vazia.  
  
 **SQL_DESC_CONCISE_TYPE [Todos]**  
 Este campo de cabeçalho SQLSMALLINT especifica o tipo de dados concisos para todos os tipos de dados, incluindo os tipos de dados de data e intervalo.  
  
 Os valores nos campos SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE e SQL_DESC_DATETIME_INTERVAL_CODE são interdependentes. Cada vez que um dos campos é definido, o outro também deve ser definido. SQL_DESC_CONCISE_TYPE pode ser definida por uma chamada para **SQLBindCol** ou **SQLBindParameter**ou **SQLSetDescField**. SQL_DESC_TYPE pode ser definida por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Se SQL_DESC_CONCISE_TYPE for definido como um tipo de dados conciso que não seja um tipo de dados de intervalo ou data, o campo SQL_DESC_TYPE será definido para o mesmo valor e o campo SQL_DESC_DATETIME_INTERVAL_CODE será definido como 0.  
  
 Se SQL_DESC_CONCISE_TYPE estiver definido para o tipo de dados de data ou intervalo concisa, o campo SQL_DESC_TYPE será definido para o tipo de verbose correspondente (SQL_DATETIME ou SQL_INTERVAL) e o campo SQL_DESC_DATETIME_INTERVAL_CODE será definido como o subcódigo apropriado.  
  
 **SQL_DESC_DATA_PTR [Descritores de aplicativos e IPDs]**  
 Este campo de registro SQLPOINTER aponta para uma variável que conterá o valor do parâmetro (para APDs) ou o valor da coluna (para ARDs). Este campo é um *campo diferido.* Ele não é usado no momento em que é definido, mas é usado posteriormente pelo motorista para recuperar dados.  
  
 A coluna especificada pelo campo SQL_DESC_DATA_PTR do ARD é desvinculada se o argumento *TargetValuePtr* em uma chamada para **SQLBindCol** for um ponteiro nulo ou se o campo SQL_DESC_DATA_PTR no ARD for definido por uma chamada para **SQLSetDescField** ou **SQLSetDescRec** para um ponteiro nulo. Outros campos não serão afetados se o campo SQL_DESC_DATA_PTR estiver definido como um ponteiro nulo.  
  
 Se a chamada para **SQLFetch** ou **SQLFetchScroll** que preenche o buffer apontado por este campo não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido.  
  
 Sempre que o campo SQL_DESC_DATA_PTR de um APD, ARD ou IPD é definido, o driver verifica se o valor no campo SQL_DESC_TYPE contém um dos tipos de dados C válidos do ODBC ou um tipo de dados específicos do driver, e que todos os outros campos que afetam os tipos de dados são consistentes. Solicitar uma verificação de consistência é o único uso do campo SQL_DESC_DATA_PTR de um IPD. Especificamente, se um aplicativo definir o campo SQL_DESC_DATA_PTR de um IPD e posteriormente chamar **SQLGetDescField** neste campo, ele não necessariamente retornará o valor que havia definido. Para obter mais informações, consulte "Verificações de consistência" no [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [Todos]**  
 Este campo de registro SQLSMALLINT contém o subcódigo para o tipo de dados de data ou intervalo específico quando o campo SQL_DESC_TYPE está SQL_DATETIME ou SQL_INTERVAL. Isso é verdade para os tipos de dados SQL e C. O código consiste no nome do tipo de dados com "CODE" substituído por "TYPE" ou "C_TYPE" (para tipos de data- data) ou "CODE" substituído por "INTERVAL" ou "C_INTERVAL" (para tipos de intervalo).  
  
 Se SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE em um descritor de aplicativo forem definidos para SQL_C_DEFAULT e o descritor não estiver associado a uma alça de declaração, o conteúdo de SQL_DESC_DATETIME_INTERVAL_CODE será indefinido.  
  
 Este campo pode ser definido para os tipos de dados de data-hora listados na tabela a seguir.  
  
|Tipos de data-hora|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/ SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Este campo pode ser definido para os tipos de dados de intervalo listados na tabela a seguir.  
  
|Tipo de intervalo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/ SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/ SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/ SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/ SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/ SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/ SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/ SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/ SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/ SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/ SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/ SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/ SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Para obter mais informações sobre os intervalos de dados e este campo, consulte [Identificadores e Descritores de Tipo de Dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [Todos]**  
 Este campo de registro SQLINTEGER contém a precisão de intervalo principal se o campo de SQL_DESC_TYPE for SQL_INTERVAL. Quando o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido como um tipo de dados de intervalo, este campo é definido para o intervalo padrão de precisão principal.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 Este campo de registro SQLINTEGER somente leitura contém o número máximo de caracteres necessários para exibir os dados da coluna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [Descritores de implementação]**  
 Este campo de registro SQLSMALLINT somente leitura é definido para SQL_TRUE se a coluna é uma coluna numérica exata e tem uma precisão fixa e escala não zero, ou para SQL_FALSE se a coluna não for uma coluna numérica exata com uma precisão e escala fixas.  
  
 **SQL_DESC_INDICATOR_PTR [Descritores de aplicativos]**  
 Em ARDs, este campo de registro SQLLEN * aponta para a variável indicador. Esta variável contém SQL_NULL_DATA se o valor da coluna for um NULL. Para APDs, a variável indicador é definida para SQL_NULL_DATA para especificar argumentos dinâmicos NULL. Caso contrário, a variável é zero (a menos que os valores em SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR sejam o mesmo ponteiro).  
  
 Se o campo SQL_DESC_INDICATOR_PTR em um ARD for um ponteiro nulo, o driver fica impedido de retornar informações sobre se a coluna é NULA ou não. Se a coluna for NULL e SQL_DESC_INDICATOR_PTR for um ponteiro nulo, SQLSTATE 22002 (variável indicador necessária, mas não fornecida) será devolvido quando o driver tentar preencher o buffer após uma chamada para **SQLFetch** ou **SQLFetchScroll**. Se a chamada para **SQLFetch** ou **SQLFetchScroll** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido.  
  
 O campo SQL_DESC_INDICATOR_PTR determina se o campo apontado por SQL_DESC_OCTET_LENGTH_PTR está definido. Se o valor dos dados de uma coluna for NULO, o driver definirá a variável indicador a SQL_NULL_DATA. O campo apontado por SQL_DESC_OCTET_LENGTH_PTR não está então definido. Se um valor NULL não for encontrado durante a busca, o buffer apontado por SQL_DESC_INDICATOR_PTR é definido como zero e o buffer apontado por SQL_DESC_OCTET_LENGTH_PTR é definido para o comprimento dos dados.  
  
 Se o campo SQL_DESC_INDICATOR_PTR em uma APD for um ponteiro nulo, o aplicativo não poderá usar este registro de descritor para especificar argumentos NULL.  
  
 Este campo é um *campo diferido*: Não é usado no momento em que é definido, mas é usado posteriormente pelo driver para indicar nulidade (para ARDs) ou para determinar a nulidade (para APDs).  
  
 **SQL_DESC_LABEL [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o rótulo ou título da coluna. Se a coluna não tiver um rótulo, esta variável contém o nome da coluna. Se a coluna não tiver nome e não for rotulada, esta variável contém uma seqüência de string vazia.  
  
 **SQL_DESC_LENGTH [Todos]**  
 Este campo de registro SQLULEN é o comprimento máximo ou real de uma seqüência de caracteres ou um tipo de dados binários em bytes. É o comprimento máximo para um tipo de dados de comprimento fixo, ou o comprimento real para um tipo de dados de comprimento variável. Seu valor sempre exclui o caractere de rescisão nula que termina a seqüência de caracteres. Para valores cujo tipo é SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP ou um dos tipos de dados de intervalo SQL, este campo tem o comprimento em caracteres da representação da seqüência de caracteres do valor de data ou intervalo.  
  
 O valor neste campo pode ser diferente do valor para "comprimento" como definido em ODBC 2 *.x*. Para obter mais informações, consulte [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o caractere ou caracteres que o driver reconhece como um prefixo para um literal deste tipo de dados. Esta variável contém uma seqüência vazia para um tipo de dados para o qual um prefixo literal não é aplicável.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o caractere ou caracteres que o driver reconhece como um sufixo para um literal deste tipo de dados. Esta variável contém uma seqüência vazia para um tipo de dados para o qual um sufixo literal não é aplicável.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [Descritores de implementação]**  
 Este campo de registro SQLCHAR * somente leitura contém qualquer nome localizado (língua nativa) para o tipo de dados que pode ser diferente do nome regular do tipo de dados. Se não houver um nome localizado, uma seqüência vazia será devolvida. Este campo é apenas para fins de exibição.  
  
 **SQL_DESC_NAME [Descritores de implementação]**  
 Este campo de registro SQLCHAR * em um descritor de linha contém o alias da coluna, se ele se aplicar. Se o alias da coluna não se aplicar, o nome da coluna será devolvido. Em ambos os casos, o motorista define o campo SQL_DESC_UNNAMED para SQL_NAMED quando ele define o campo SQL_DESC_NAME. Se não houver nome de coluna ou um alias de coluna, o driver retorna uma seqüência vazia no campo SQL_DESC_NAME e define o campo SQL_DESC_UNNAMED para SQL_UNNAMED.  
  
 Um aplicativo pode definir o campo SQL_DESC_NAME de um IPD para um nome de parâmetro ou alias para especificar parâmetros de procedimento armazenados por nome. (Para obter mais informações, consulte [Parâmetros de vinculação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) O campo SQL_DESC_NAME de um IRD é um campo somente leitura; SQLSTATE HY091 (identificador de campo de descritor inválido) será devolvido se um aplicativo tentar defini-lo.  
  
 Em IPDs, este campo é indefinido se o driver não suporta parâmetros nomeados. Se o driver suportar parâmetros nomeados e for capaz de descrever parâmetros, o nome do parâmetro será devolvido neste campo.  
  
 **SQL_DESC_NULLABLE [Descritores de implementação]**  
 Em IRDs, este campo de registro SQLSMALLINT somente leitura é SQL_NULLABLE se a coluna pode ter valores NULOS, SQL_NO_NULLS se a coluna não tiver valores NULOS, ou SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores NULOS. Este campo diz respeito à coluna de conjunto de resultados, não à coluna base.  
  
 Nos IPDs, este campo é sempre definido como SQL_NULLABLE porque os parâmetros dinâmicos são sempre nulos e não podem ser definidos por um aplicativo.  
  
 **SQL_DESC_NUM_PREC_RADIX [Todos]**  
 Este campo SQLINTEGER contém um valor de 2 se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico aproximado, porque o campo SQL_DESC_PRECISION contém o número de bits. Este campo contém um valor de 10 se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico exato, porque o campo SQL_DESC_PRECISION contém o número de dígitos decimais. Este campo está definido como 0 para todos os tipos de dados não numéricos.  
  
 **SQL_DESC_OCTET_LENGTH [Todos]**  
 Este campo de registro SQLLEN contém o comprimento, em bytes, de uma seqüência de caracteres ou tipo de dados binários. Para caracteres de comprimento fixo ou tipos binários, este é o comprimento real em bytes. Para caracteres de comprimento variável ou tipos binários, este é o comprimento máximo em bytes. Esse valor sempre exclui o espaço para o caractere de rescisão nula para descritores de implementação e sempre inclui espaço para o caractere de rescisão nula para descritores de aplicativos. Para dados da aplicação, este campo contém o tamanho do buffer. Para APDs, este campo é definido apenas para parâmetros de saída ou de entrada/saída.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [Descritores de aplicativos]**  
 Este campo de registro SQLLEN * aponta para uma variável que conterá o comprimento total em bytes de um argumento dinâmico (para descritores de parâmetro) ou de um valor de coluna vinculado (para descritores de linha).  
  
 Para uma APD, esse valor é ignorado para todos os argumentos, exceto string de caracteree binário; se este campo aponta para SQL_NTS, o argumento dinâmico deve ser nulo. Para indicar que um parâmetro vinculado será um parâmetro de dados em execução, um aplicativo define este campo no registro apropriado da APD para uma variável que, no momento da execução, conterá o valor SQL_DATA_AT_EXEC ou o resultado da SQL_LEN_DATA_AT_EXEC macro. Se houver mais de um desses campos, SQL_DESC_DATA_PTR pode ser definido como um valor que identifica exclusivamente o parâmetro para ajudar o aplicativo a determinar qual parâmetro está sendo solicitado.  
  
 Se o campo OCTET_LENGTH_PTR de um ARD for um ponteiro nulo, o driver não retornará as informações de comprimento para a coluna. Se o campo SQL_DESC_OCTET_LENGTH_PTR de uma APD for um ponteiro nulo, o driver assumirá que as seqüências de caracteres e valores binários são nulos. (Os valores binários não devem ser anulados nulos, mas devem ser dados um comprimento para evitar a truncação.)  
  
 Se a chamada para **SQLFetch** ou **SQLFetchScroll** que preenche o buffer apontado por este campo não retornou SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o conteúdo do buffer será indefinido. Este campo é um *campo diferido.* Ele não é usado no momento em que é definido, mas é usado posteriormente pelo motorista para determinar ou indicar o comprimento do octeto dos dados.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 Este campo de registro SQLSMALLINT está definido para SQL_PARAM_INPUT para um parâmetro de entrada, SQL_PARAM_INPUT_OUTPUT para um parâmetro de entrada/saída, SQL_PARAM_OUTPUT para um parâmetro de saída, SQL_PARAM_INPUT_OUTPUT_STREAM para um parâmetro de entrada/saída em fluxo, ou SQL_PARAM_OUTPUT_STREAM para um parâmetro de saída em fluxo. Ele está definido para SQL_PARAM_INPUT por padrão.  
  
 Para um IPD, o campo é definido como SQL_PARAM_INPUT por padrão se o IPD não for preenchido automaticamente pelo driver (o atributo de declaração SQL_ATTR_ENABLE_AUTO_IPD é SQL_FALSE). Um aplicativo deve definir este campo no IPD para parâmetros que não sejam parâmetros de entrada.  
  
 **SQL_DESC_PRECISION [Todos]**  
 Este campo de registro SQLSMALLINT contém o número de dígitos para um tipo numérico exato, o número de bits na mantissa (precisão binária) para um tipo numérico aproximado, ou os números de dígitos no componente de segundos fracionados para o SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP ou SQL_INTERVAL_SECOND tipo de dados. Este campo é indefinido para todos os outros tipos de dados.  
  
 O valor neste campo pode ser diferente do valor para "precisão" como definido em ODBC 2 *.x*. Para obter mais informações, consulte [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [Descritores de implementação]**  
 Este campo SQLSMALLINTrecord indica se uma coluna é automaticamente modificada pelo DBMS quando uma linha é atualizada (por exemplo, uma coluna do tipo "carimbo de tempo" no SQL Server). O valor deste campo de registro é definido para SQL_TRUE se a coluna for uma coluna de versão em linha e para SQL_FALSE o contrário. Este atributo da coluna é semelhante ao chamar **SQLSpecialColumns** com IdentifierType of SQL_ROWVER para determinar se uma coluna é atualizada automaticamente.  
  
 **SQL_DESC_SCALE [Todos]**  
 Este campo de registro SQLSMALLINT contém a escala definida para tipos de dados decimais e numéricos. O campo é indefinido para todos os outros tipos de dados.  
  
 O valor neste campo pode ser diferente do valor para "escala" como definido em ODBC 2 *.x*. Para obter mais informações, consulte [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome do esquema da tabela base que contém a coluna. O valor de devolução é dependente do driver se a coluna for uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não suportar esquemas ou o nome do esquema não puder ser determinado, esta variável contém uma seqüência de string vazia.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 Este campo de registro SQLSMALLINT somente leitura é definido como um dos seguintes valores:  
  
-   SQL_PRED_NONE se a coluna não puder ser usada em uma cláusula **WHERE.** (Este é o mesmo valor SQL_UNSEARCHABLE em ODBC 2 *.x*.)  
  
-   SQL_PRED_CHAR se a coluna pode ser usada em uma cláusula **WHERE,** mas apenas com o predicado **LIKE.** (Este é o mesmo valor SQL_LIKE_ONLY em ODBC 2 *.x*.)  
  
-   SQL_PRED_BASIC se a coluna puder ser usada em uma cláusula **WHERE** com todos os operadores de **comparação,** exceto LIKE . (Este é o mesmo valor SQL_EXCEPT_LIKE em ODBC 2 *.x*.)  
  
-   SQL_PRED_SEARCHABLE se a coluna pode ser usada em uma cláusula **WHERE** com qualquer operador de comparação.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome da tabela base que contém esta coluna. O valor de devolução é dependente do driver se a coluna for uma expressão ou se a coluna faz parte de uma exibição.  
  
 **SQL_DESC_TYPE [Todos]**  
 Este campo de registro SQLSMALLINT especifica o tipo de dados SQL ou C conciso para todos os tipos de dados, exceto os tipos de dados de data e intervalo. Para os tipos de dados de data e intervalo, este campo especifica o tipo de dados verbose, que é SQL_DATETIME ou SQL_INTERVAL.  
  
 Sempre que este campo contiver SQL_DATETIME ou SQL_INTERVAL, o campo de SQL_DESC_DATETIME_INTERVAL_CODE deve conter o subcódigo apropriado para o tipo conciso. Para os tipos de dados de data-hora, SQL_DESC_TYPE contém SQL_DATETIME e o campo SQL_DESC_DATETIME_INTERVAL_CODE contém um subcódigo para o tipo de dados de data específica. Para tipos de dados de intervalo, SQL_DESC_TYPE contém SQL_INTERVAL e o campo SQL_DESC_DATETIME_INTERVAL_CODE contém um subcódigo para o tipo de dados de intervalo específico.  
  
 Os valores nos campos SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE são interdependentes. Cada vez que um dos campos é definido, o outro também deve ser definido. SQL_DESC_TYPE pode ser definida por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE pode ser definida por uma chamada para **SQLBindCol** ou **SQLBindParameter**ou **SQLSetDescField**.  
  
 Se SQL_DESC_TYPE for definido como um tipo de dados conciso que não seja um tipo de dados de intervalo ou data, o campo SQL_DESC_CONCISE_TYPE será definido para o mesmo valor e o campo SQL_DESC_DATETIME_INTERVAL_CODE é definido como 0.  
  
 Se SQL_DESC_TYPE estiver definido para o tipo de dados de data ou intervalo verbose (SQL_DATETIME ou SQL_INTERVAL) e o campo SQL_DESC_DATETIME_INTERVAL_CODE estiver definido como subcódigo apropriado, o campo SQL_DESC_CONCISE TYPE será definido para o tipo conciso correspondente. Tentar definir SQL_DESC_TYPE para um dos tipos de data ou intervalo concisos retornará SQLSTATE HY021 (informações inconsistentes do descritor).  
  
 Quando o campo SQL_DESC_TYPE é definido por uma chamada para **SQLBindCol,** **SQLBindParameter**ou **SQLSetDescField,** os seguintes campos são definidos para os seguintes valores padrão, conforme mostrado na tabela abaixo. Os valores dos campos remanescentes do mesmo registro são indefinidos.  
  
|Valor de SQL_DESC_TYPE|Outros campos implicitamente definidos|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR SQL_C_VARCHAR|SQL_DESC_LENGTH está definido para 1. SQL_DESC_PRECISION está definido para 0.|  
|SQL_DATETIME|Quando SQL_DESC_DATETIME_INTERVAL_CODE é definido para SQL_CODE_DATE ou SQL_CODE_TIME, SQL_DESC_PRECISION é definido para 0. Quando estiver definido para SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION está definido para 6.|  
|SQL_DECIMAL, SQL_NUMERIC SQL_C_NUMERIC|SQL_DESC_SCALE está definido para 0. SQL_DESC_PRECISION é definida como precisão definida pela implementação para o respectivo tipo de dados.<br /><br /> Consulte [SQL a C: Numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md) para obter informações sobre como vincular manualmente um valor SQL_C_NUMERIC.|  
|SQL_FLOAT SQL_C_FLOAT|SQL_DESC_PRECISION é definida como a precisão padrão definida pela implementação para SQL_FLOAT.|  
|SQL_INTERVAL|Quando SQL_DESC_DATETIME_INTERVAL_CODE é definida como um tipo de dados de intervalo, SQL_DESC_DATETIME_INTERVAL_PRECISION é definida como 2 (a precisão de liderança do intervalo padrão). Quando o intervalo tem um componente de segundos, SQL_DESC_PRECISION é definido como 6 (a precisão dos segundos de intervalo padrão).|  
  
 Quando um aplicativo chama **SQLSetDescField** para definir campos de um descritor em vez de chamar **SQLSetDescRec,** o aplicativo deve primeiro declarar o tipo de dados. Quando isso acontece, os outros campos indicados na tabela anterior são implicitamente definidos. Se algum dos valores definidos implicitamente for inaceitável, o aplicativo pode então chamar **SQLSetDescField** ou **SQLSetDescRec** para definir o valor inaceitável explicitamente.  
  
 **SQL_DESC_TYPE_NAME [Descritores de implementação]**  
 Este campo de registro SQLCHAR * somente leitura contém o nome do tipo dependente da fonte de dados (por exemplo, "CHAR", "VARCHAR" e assim por diante). Se o nome do tipo de dados for desconhecido, esta variável contém uma seqüência de string vazia.  
  
 **SQL_DESC_UNNAMED [Descritores de implementação]**  
 Este campo de registro SQLSMALLINT em um descritor de linha é definido pelo driver para SQL_NAMED ou SQL_UNNAMED quando ele define o campo SQL_DESC_NAME. Se o campo SQL_DESC_NAME contiver um alias de coluna ou se o alias da coluna não se aplicar, o driver definirá o campo SQL_DESC_UNNAMED para SQL_NAMED. Se um aplicativo definir o campo SQL_DESC_NAME de um IPD para um nome de parâmetro ou alias, o driver definirá o campo SQL_DESC_UNNAMED do IPD para SQL_NAMED. Se não houver nome de coluna ou um alias de coluna, o driver definirá o campo SQL_DESC_UNNAMED para SQL_UNNAMED.  
  
 Um aplicativo pode definir o campo SQL_DESC_UNNAMED de um IPD para SQL_UNNAMED. Um driver retorna SQLSTATE HY091 (identificador de campo de descritor inválido) se um aplicativo tentar definir o campo SQL_DESC_UNNAMED de um IPD para SQL_NAMED. O campo SQL_DESC_UNNAMED de um IRD é somente leitura; SQLSTATE HY091 (identificador de campo de descritor inválido) será devolvido se um aplicativo tentar defini-lo.  
  
 **SQL_DESC_UNSIGNED [Descritores de implementação]**  
 Este campo de registro SQLSMALLINT somente leitura é definido para SQL_TRUE se o tipo de coluna não estiver assinado ou não nuéter, ou SQL_FALSE se o tipo de coluna estiver assinado.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 Este campo de registro SQLSMALLINT somente leitura é definido como um dos seguintes valores:  
  
-   SQL_ATTR_READ_ONLY se a coluna do conjunto de resultados for somente leitura.  
  
-   SQL_ATTR_WRITE se a coluna do conjunto de resultados for leitura-gravação.  
  
-   SQL_ATTR_READWRITE_UNKNOWN se não se sabe se a coluna de configuração de resultados é updatable ou não.  
  
 SQL_DESC_UPDATABLE descreve a updatability da coluna no conjunto de resultados, não a coluna na tabela base. A updatability da coluna na tabela base na qual esta coluna de conjunto de resultados é baseada pode ser diferente do valor neste campo. Se uma coluna é updatable pode ser baseada no tipo de dados, privilégios de usuário e a definição do conjunto de resultados em si. Se não estiver claro se uma coluna é updatable, SQL_ATTR_READWRITE_UNKNOWN deve ser devolvida.  
  
## <a name="consistency-checks"></a>Verificações de consistência  
 Uma verificação de consistência é realizada automaticamente pelo motorista sempre que um aplicativo passa em um valor para o campo SQL_DESC_DATA_PTR ard, APD ou IPD. Se algum dos campos for inconsistente com outros campos, **o SQLSetDescField** retornará sqlstate hy021 (informações inconsistentes do descritor). Para obter mais informações, consulte "Verificação de consistência" no [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando uma coluna|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Vinculando um parâmetro|[Função SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtendo um campo descritor|[Função SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtendo vários campos de descritores|[Função SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuração de vários campos de descritor|[Função SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Referência de API do ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)
