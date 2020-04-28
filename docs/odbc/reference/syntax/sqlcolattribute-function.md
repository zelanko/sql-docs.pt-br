---
title: Função SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c94de3dfc7036277f8be56c401326cdab07a9606
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301286"
---
# <a name="sqlcolattribute-function"></a>Função SQLColAttribute
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLColAttribute** retorna informações de descritor para uma coluna em um conjunto de resultados. As informações do descritor são retornadas como uma cadeia de caracteres, um valor dependente de descritor ou um valor inteiro.  
  
> [!NOTE]  
>  Para obter mais informações sobre como o Gerenciador de driver mapeia essa função quando um ODBC 3. o aplicativo *x* está funcionando com um ODBC 2. Driver *x* , consulte [mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *ColumnNumber*  
 Entrada O número do registro no IRD do qual o valor do campo deve ser recuperado. Esse argumento corresponde ao número de coluna de dados de resultado, ordenado sequencialmente no aumento da ordem das colunas, começando em 1. As colunas podem ser descritas em qualquer ordem.  
  
 A coluna 0 pode ser especificada neste argumento, mas todos os valores, exceto SQL_DESC_TYPE e SQL_DESC_OCTET_LENGTH, retornarão valores indefinidos.  
  
 *FieldIdentifier*  
 Entrada O identificador do descritor. Esse identificador define qual campo em IRD deve ser consultado (por exemplo, SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 Der Ponteiro para um buffer no qual retornar o valor no campo *FieldIdentifier* da linha *ColumnNumber* do IRD, se o campo for uma cadeia de caracteres. Caso contrário, o campo não será usado.  
  
 Se *CharacterAttributePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *CharacterAttributePtr*.  
  
 *BufferLength*  
 Entrada Se *FieldIdentifier* for um campo definido pelo ODBC e *CharacterAttributePtr* apontar para uma cadeia de caracteres ou um buffer binário, esse argumento deverá ter o \*comprimento de *CharacterAttributePtr*. Se *FieldIdentifier* for um campo definido pelo ODBC e \* *characterattribute*PTR for um inteiro, esse campo será ignorado. Se * \*CharacterAttributePtr* for uma cadeia de caracteres Unicode (ao chamar **SQLColAttributeW**), o argumento *BufferLength* deverá ser um número par. Se *FieldIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength* . *BufferLength* pode ter os seguintes valores:  
  
-   Se *CharacterAttributePtr* for um ponteiro para um ponteiro, *BufferLength* deverá ter o valor SQL_IS_POINTER.  
  
-   Se *CharacterAttributePtr* for um ponteiro para uma cadeia de caracteres, o *BufferLength* será o comprimento do buffer.  
  
-   Se *CharacterAttributePtr* for um ponteiro para um buffer binário, o aplicativo colocará o resultado da macro SQL_LEN_BINARY_ATTR (*Length*) em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *CharacterAttributePtr* for um ponteiro para um tipo de dados de comprimento fixo, *BufferLength* deverá ser um dos seguintes: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT ou SQLUSMALLINT.  
  
 *StringLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o byte de terminação nula para dados de caractere) disponível para retornar em **CharacterAttributePtr*.  
  
 Para dados de caractere, se o número de bytes disponíveis para retornar for maior ou igual a *BufferLength*, as informações do descritor em \* *CharacterAttributePtr* serão truncadas para *BufferLength* menos o comprimento de um caractere de terminação nula e serão terminadas em nulo pelo driver.  
  
 Para todos os outros tipos de dados, o valor de *BufferLength* é ignorado e o driver assume que o tamanho de **CharacterAttributePtr* é de 32 bits.  
  
 *NumericAttributePtr*  
 Der Ponteiro para um buffer de inteiros no qual retornar o valor no campo *FieldIdentifier* da linha *ColumnNumber* do IRD, se o campo for um tipo numérico de descritor, como SQL_DESC_COLUMN_LENGTH. Caso contrário, o campo não será usado. Observe que alguns drivers podem gravar apenas o menor 32 ou 16 bits de um buffer e deixar o bit de ordem superior inalterado. Portanto, os aplicativos devem inicializar o valor como 0 antes de chamar essa função.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLColAttribute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLColAttribute** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres, truncados à direita|O buffer \* *CharacterAttributePtr* não era grande o suficiente para retornar o valor da cadeia de caracteres inteiro, portanto, o valor da cadeia de caracteres foi truncado. O comprimento do valor de cadeia de caracteres não truncado é retornado em **StringLengthPtr*. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07005|Instrução preparada não é uma *especificação de cursor*|A instrução associada ao *StatementHandle* não retornou um conjunto de resultados e *FieldIdentifier* não foi SQL_DESC_COUNT. Não havia colunas para descrever.|  
|07009|Índice de descritor inválido|(DM) o valor especificado para *ColumnNumber* era igual a 0 e o atributo de instrução SQL_ATTR_USE_BOOKMARKS foi SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *ColumnNumber* era maior que o número de colunas no conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagField** da estrutura de dados de diagnóstico descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativo multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função aynchronous ainda estava em execução quando SQLColAttribute foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) a função foi chamada antes de chamar **SQLPrepare**, **SQLExecDirect**ou uma função de catálogo para o *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) * \*CharacterAttributePtr* é uma cadeia de caracteres e *BufferLength* era menor que 0, mas não é igual a SQL_NTS.|  
|HY091|Identificador de campo de descritor inválido|O valor especificado para o argumento *FieldIdentifier* não era um dos valores definidos e não era um valor definido pela implementação.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Driver sem capacidade|O valor especificado para o argumento *FieldIdentifier* não tem suporte do driver.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
|IM017|A sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação for usado, a sondagem será desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesse identificador.|Se a chamada de função anterior no identificador retornar SQL_STILL_EXECUTING e se o modo de notificação estiver habilitado, **SQLCompleteAsync** deverá ser chamado na alça para executar o pós-processamento e concluir a operação.|  
  
 Quando chamado depois de **SQLPrepare** e antes de **SQLExecute**, **SQLColAttribute** pode retornar qualquer SQLSTATE que possa ser retornado por **SQLPrepare** ou **SQLExecute**, dependendo de quando a fonte de dados avaliar a instrução SQL associada ao *StatementHandle*.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLColAttribute** antes de executar uma instrução.  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre como os aplicativos usam as informações retornadas por **SQLColAttribute**, consulte [metadados do conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** retorna informações em \* *NumericAttributePtr* ou em \* *CharacterAttributePtr*. As informações de inteiros são \*retornadas em *NumericAttributePtr* como um valor SQLLEN; todos os outros formatos de informações são retornados \*em *CharacterAttributePtr*. Quando as informações são retornadas em \* *NumericAttributePtr*, o driver ignora *CharacterAttributePtr*, *BufferLength*e *StringLengthPtr*. Quando as informações são retornadas em \* *CharacterAttributePtr*, o driver ignora *NumericAttributePtr*.  
  
 **SQLColAttribute** retorna valores dos campos de descritor do IRD. A função é chamada com um identificador de instrução em vez de um identificador de descritor. Os valores retornados por **SQLColAttribute** para os valores de *FieldIdentifier* listados posteriormente nesta seção também podem ser recuperados chamando **SQLGetDescField** com o identificador IRD apropriado.  
  
 Os campos de descritor definidos atualmente, a versão do ODBC na qual eles foram introduzidos e os argumentos nos quais as informações são retornadas para eles são mostrados mais adiante nesta seção; mais tipos de descritores podem ser definidos por drivers para tirar proveito de diferentes fontes de dados.  
  
 Um ODBC 3. o driver *x* deve retornar um valor para cada um dos campos de descritor. Se um campo de descritor não se aplicar a um driver ou a uma fonte de dados e, a menos que \*indicado de outra forma, o driver retornará 0 em *StringLengthPtr* ou uma cadeia de caracteres vazia em **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 O ODBC 3. a função *x* **SQLCOLATTRIBUTE** substitui o ODBC 2 substituído. *x* função x **SQLColAttributes**. Ao mapear **SQLColAttributes** para **SQLColAttribute** (quando um ODBC 2.* *o aplicativo x está trabalhando com um ODBC 3. *x* driver) ou mapeando **SQLColAttribute** para **SQLColAttributes** (quando um ODBC 3.* *o aplicativo x está funcionando com um ODBC 2. *x* driver), o Gerenciador de driver passa o valor de *FieldIdentifier* até, mapeia-o para um novo valor ou retorna um erro, da seguinte maneira:  
  
> [!NOTE]  
>  O prefixo usado nos valores de *FieldIdentifier* no ODBC 3. *x* foi alterado de usado no ODBC 2. *x*. O novo prefixo é "SQL_DESC"; o prefixo antigo era "SQL_COLUMN".  
  
-   Se o valor de **#define** do ODBC 2. *x* *FieldIdentifier* é o mesmo que o valor **#define** do ODBC 3. *x* *FieldIdentifier*, o valor na chamada de função é apenas passado.  
  
-   Os valores de **#define** do ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION e SQL_COLUMN_SCALE são diferentes dos valores **#define** do ODBC 3. *x* *FieldIdentifiers* SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_LENGTH. Um ODBC 2. o driver *x* precisa dar suporte apenas ao ODBC 2. valores *x* . Um ODBC 3. o driver *x* deve dar suporte aos valores "SQL_COLUMN" e "SQL_DESC" para esses três *FieldIdentifiers*. Esses valores são diferentes porque precisão, escala e comprimento são definidos de forma diferente no ODBC 3. *x* do que estavam no ODBC 2. *x*. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
-   Se o valor de **#define** do ODBC 2. *x* *FieldIdentifier* é diferente do valor **#define** do ODBC 3. *x* *FieldIdentifier*, como ocorre com os valores Count, Name e Nullable, o valor na chamada de função é mapeado para o valor correspondente. Por exemplo, SQL_COLUMN_COUNT é mapeado para SQL_DESC_COUNT e SQL_DESC_COUNT é mapeado para SQL_COLUMN_COUNT, dependendo da direção do mapeamento.  
  
-   Se *FieldIdentifier* for um novo valor no ODBC 3. *x*, para o qual não havia nenhum valor correspondente no ODBC 2. *x*, ele não será mapeado quando um ODBC 3. o aplicativo *x* usa-o em uma chamada para **SQLCOLATTRIBUTE** em um ODBC 2. *x* Driver, e a chamada retornará SQLSTATE HY091 (identificador de campo de descritor inválido).  
  
 A tabela a seguir lista os tipos de descritores retornados por **SQLColAttribute**. O tipo de valores *NumericAttributePtr* é **SQLLEN \* **.  
  
|*FieldIdentifier*|Informações<br /><br /> retornado em|Descrição|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1,0)|*NumericAttributePtr*|SQL_TRUE se a coluna for uma coluna de incremento automático.<br /><br /> SQL_FALSE se a coluna não for uma coluna de incremento automático ou não for numérica.<br /><br /> Este campo é válido somente para colunas de tipo de dados numéricos. Um aplicativo pode inserir valores em uma linha que contém uma coluna AutoIncrement, mas normalmente não pode atualizar valores na coluna.<br /><br /> Quando uma inserção é feita em uma coluna de incremento automático, um valor exclusivo é inserido na coluna no momento da inserção. O incremento não está definido, mas é específico da fonte de dados. Um aplicativo não deve supor que uma coluna de incremento automático comece em qualquer ponto específico ou seja incrementada por qualquer valor específico.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3,0)|*CharacterAttributePtr*|O nome da coluna base para a coluna do conjunto de resultados. Se um nome de coluna base não existir (como no caso de colunas que são expressões), essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_BASE_COLUMN_NAME do IRD, que é um campo somente leitura.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3,0)|*CharacterAttributePtr*|O nome da tabela base que contém a coluna. Se o nome da tabela base não puder ser definido ou não for aplicável, essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_BASE_TABLE_NAME do IRD, que é um campo somente leitura.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1,0)|*NumericAttributePtr*|SQL_TRUE se a coluna for tratada como diferenciação de maiúsculas e minúsculas para agrupamentos e comparações.<br /><br /> SQL_FALSE se a coluna não for tratada como diferenciação de maiúsculas e minúsculas para agrupamentos e comparações ou não for caractere.|  
|SQL_DESC_CATALOG_NAME (ODBC 2,0)|*CharacterAttributePtr*|O catálogo da tabela que contém a coluna. O valor retornado será definido como implementação se a coluna for uma expressão ou se a coluna fizer parte de uma exibição. Se a fonte de dados não oferecer suporte a catálogos ou se o nome do catálogo não puder ser determinado, uma cadeia de caracteres vazia será retornada. Este campo de registro VARCHAR não está limitado a 128 caracteres.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1,0)|*NumericAttributePtr*|O tipo de dados conciso.<br /><br /> Para os tipos de dados DateTime e Interval, esse campo retorna o tipo de dados conciso; por exemplo, SQL_TYPE_TIME ou SQL_INTERVAL_YEAR. (Para obter mais informações, consulte [identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) no Apêndice D: tipos de dados.)<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_CONCISE_TYPE do IRD.|  
|SQL_DESC_COUNT (ODBC 1,0)|*NumericAttributePtr*|O número de colunas disponíveis no conjunto de resultados. Isso retornará 0 se não houver nenhuma coluna no conjunto de resultados. O valor no argumento *ColumnNumber* é ignorado.<br /><br /> Essas informações são retornadas do campo de cabeçalho SQL_DESC_COUNT do IRD.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1,0)|*NumericAttributePtr*|Número máximo de caracteres necessários para exibir dados da coluna. Para obter mais informações sobre o tamanho de exibição, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1,0)|*NumericAttributePtr*|SQL_TRUE se a coluna tiver uma precisão fixa e uma escala diferente de zero que sejam específicas da fonte de dados.<br /><br /> SQL_FALSE se a coluna não tiver uma precisão fixa e uma escala diferente de zero que sejam específicas da fonte de dados.|  
|SQL_DESC_LABEL (ODBC 2,0)|*CharacterAttributePtr*|O rótulo ou título da coluna. Por exemplo, uma coluna chamada EmpName pode ser rotulada como nome do funcionário ou pode ser rotulada com um alias.<br /><br /> Se uma coluna não tiver um rótulo, o nome da coluna será retornado. Se a coluna não estiver rotulada e não tiver nome, uma cadeia de caracteres vazia será retornada.|  
|SQL_DESC_LENGTH (ODBC 3,0)|*NumericAttributePtr*|Um valor numérico que é o comprimento de caractere máximo ou real de uma cadeia de caracteres ou tipo de dados binário. É o comprimento máximo de caracteres para um tipo de dados de comprimento fixo ou o comprimento de caractere real para um tipo de dados de comprimento variável. Seu valor sempre exclui o byte de terminação nula que termina a cadeia de caracteres.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_LENGTH do IRD.<br /><br /> Para obter mais informações sobre comprimento, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3,0)|*CharacterAttributePtr*|Este campo de registro VARCHAR (128) contém o caractere ou caracteres que o driver reconhece como um prefixo para um literal desse tipo de dados. Este campo contém uma cadeia de caracteres vazia para um tipo de dados para o qual um prefixo literal não é aplicável. Para obter mais informações, consulte [prefixos e sufixos literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3,0)|*CharacterAttributePtr*|Este campo de registro VARCHAR (128) contém o caractere ou caracteres que o driver reconhece como um sufixo para um literal desse tipo de dados. Este campo contém uma cadeia de caracteres vazia para um tipo de dados para o qual um sufixo literal não é aplicável. Para obter mais informações, consulte [prefixos e sufixos literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3,0)|*CharacterAttributePtr*|Este campo de registro VARCHAR (128) contém qualquer nome localizado (idioma nativo) para o tipo de dados que pode ser diferente do nome regular do tipo de dados. Se não houver nenhum nome localizado, uma cadeia de caracteres vazia será retornada. Este campo é apenas para fins de exibição. O conjunto de caracteres da cadeia de caracteres é dependente de localidade e normalmente é o conjunto de caracteres padrão do servidor.|  
|SQL_DESC_NAME (ODBC 3,0)|*CharacterAttributePtr*|O alias da coluna, se aplicável. Se o alias da coluna não se aplicar, o nome da coluna será retornado. Em ambos os casos, SQL_DESC_UNNAMED é definido como SQL_NAMED. Se não houver nenhum nome de coluna ou um alias de coluna, uma cadeia de caracteres vazia será retornada e SQL_DESC_UNNAMED será definida como SQL_UNNAMED.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_NAME do IRD.|  
|SQL_DESC_NULLABLE (ODBC 3,0)|*NumericAttributePtr*|SQL_ ANULÁVEL se a coluna puder ter valores nulos; SQL_NO_NULLS se a coluna não tiver valores nulos; ou SQL_NULLABLE_UNKNOWN se não for conhecido se a coluna aceita valores nulos.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_NULLABLE do IRD.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3,0)|*NumericAttributePtr*|Se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico aproximado, esse campo SQLINTEGER conterá um valor 2 porque o campo SQL_DESC_PRECISION contém o número de bits. Se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico exato, esse campo conterá um valor de 10 porque o campo SQL_DESC_PRECISION contém o número de dígitos decimais. Esse campo é definido como 0 para todos os tipos de dados não numéricos.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3,0)|*NumericAttributePtr*|O comprimento, em bytes, de uma cadeia de caracteres ou tipo de dados Binary. Para tipos de caracteres de comprimento fixo ou binários, esse é o comprimento real em bytes. Para tipos de caracteres de comprimento variável ou binários, esse é o comprimento máximo em bytes. Esse valor não inclui o terminador nulo.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_OCTET_LENGTH do IRD.<br /><br /> Para obter mais informações sobre comprimento, consulte [tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: tipos de dados.|  
|SQL_DESC_PRECISION (ODBC 3,0)|*NumericAttributePtr*|Um valor numérico que para um tipo de dados numérico denota a precisão aplicável. Para tipos de dados SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP e todos os tipos de dados de intervalo que representam um intervalo de tempo, seu valor é a precisão aplicável do componente de segundos fracionários.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_PRECISION do IRD.|  
|SQL_DESC_SCALE (ODBC 3,0)|*NumericAttributePtr*|Um valor numérico que é a escala aplicável para um tipo de dados numérico. Para tipos de dados decimais e NUMÉRICOs, essa é a escala definida. Ele é indefinido para todos os outros tipos de dados.<br /><br /> Essas informações são retornadas do campo de registro de escala do IRD.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2,0)|*CharacterAttributePtr*|O esquema da tabela que contém a coluna. O valor retornado será definido como implementação se a coluna for uma expressão ou se a coluna fizer parte de uma exibição. Se a fonte de dados não oferecer suporte a esquemas ou o nome do esquema não puder ser determinado, uma cadeia de caracteres vazia será retornada. Este campo de registro VARCHAR não está limitado a 128 caracteres.|  
|SQL_DESC_SEARCHABLE (ODBC 1,0)|*NumericAttributePtr*|SQL_PRED_NONE se a coluna não puder ser usada em uma cláusula WHERE. (Isso é o mesmo que o valor de SQL_UNSEARCHABLE no ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se a coluna puder ser usada em uma cláusula WHERE, mas somente com o predicado LIKE. (Isso é o mesmo que o valor de SQL_LIKE_ONLY no ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se a coluna puder ser usada em uma cláusula WHERE com todos os operadores de comparação, exceto como. (Isso é o mesmo que o valor de SQL_EXCEPT_LIKE no ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE se a coluna puder ser usada em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> As colunas do tipo SQL_LONGVARCHAR e SQL_LONGVARBINARY geralmente retornam SQL_PRED_CHAR.|  
|SQL_DESC_TABLE_NAME (ODBC 2,0)|*CharacterAttributePtr*|O nome da tabela que contém a coluna. O valor retornado será definido como implementação se a coluna for uma expressão ou se a coluna fizer parte de uma exibição.<br /><br /> Se o nome da tabela não puder ser determinado, uma cadeia de caracteres vazia será retornada.|  
|SQL_DESC_TYPE (ODBC 3,0)|*NumericAttributePtr*|Um valor numérico que especifica o tipo de dados SQL.<br /><br /> Quando *ColumnNumber* é igual a 0, SQL_BINARY é retornado para indicadores de comprimento variável e SQL_INTEGER é retornado para indicadores de comprimento fixo.<br /><br /> Para os tipos de dados DateTime e Interval, esse campo retorna o tipo de dados verbose: SQL_DATETIME ou SQL_INTERVAL. (Para obter mais informações, consulte [identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) no Apêndice D: tipos de dados.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_TYPE do IRD. **Observação:**  Para trabalhar com o ODBC 2. drivers *x* , use SQL_DESC_CONCISE_TYPE em vez disso.|  
|SQL_DESC_TYPE_NAME (ODBC 1,0)|*CharacterAttributePtr*|Nome do tipo de dados dependente de fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" ou "CHAR () para dados de BIT".<br /><br /> Se o tipo for desconhecido, uma cadeia de caracteres vazia será retornada.|  
|SQL_DESC_UNNAMED (ODBC 3,0)|*NumericAttributePtr*|SQL_NAMED ou SQL_UNNAMED. Se o campo SQL_DESC_NAME de IRD contiver um alias de coluna ou um nome de coluna, SQL_NAMED será retornado. Se não houver nenhum nome de coluna ou alias de coluna, SQL_UNNAMED será retornado.<br /><br /> Essas informações são retornadas do campo de registro de SQL_DESC_UNNAMED do IRD.|  
|SQL_DESC_UNSIGNED (ODBC 1,0)|*NumericAttributePtr*|SQL_TRUE se a coluna não for assinada (ou não for numérica).<br /><br /> SQL_FALSE se a coluna for assinada.|  
|SQL_DESC_UPDATABLE (ODBC 1,0)|*NumericAttributePtr*|A coluna é descrita pelos valores para as constantes definidas:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE descreve a capacidade de atualização da coluna no conjunto de resultados, não a coluna na tabela base. A capacidade de atualização da coluna base na qual a coluna do conjunto de resultados é baseada pode ser diferente do valor nesse campo. A possibilidade de uma coluna ser atualizável pode ser baseada no tipo de dados, nos privilégios de usuário e na definição do próprio conjunto de resultados. Se não estiver claro se uma coluna é atualizável, SQL_ATTR_READWRITE_UNKNOWN deve ser retornado.|  
  
 **SQLColAttribute** é uma alternativa extensível para **SQLDescribeCol**. **SQLDescribeCol** retorna um conjunto fixo de informações de descritor com base em ANSI-89 SQL. O **SQLColAttribute** permite o acesso ao conjunto mais abrangente de informações de descritor disponível em extensões ANSI SQL-92 e DBMS Vendor.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Associando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Exemplo  
 O código de exemplo a seguir não libera identificadores e conexões. Consulte a função [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md), o [programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)e a [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obter exemplos de código para liberar identificadores e instruções.  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)
