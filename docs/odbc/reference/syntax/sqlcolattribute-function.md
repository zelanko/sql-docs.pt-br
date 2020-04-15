---
title: Função SQLColATTRIBUTE | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301286"
---
# <a name="sqlcolattribute-function"></a>Função SQLColAttribute
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **SQLColAttribute** retorna informações do descritor para uma coluna em um conjunto de resultados. As informações do descritor são retornadas como uma seqüência de caracteres, um valor dependente do descritor ou um valor inteiro.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Driver Manager mapeia essa função para quando um ODBC 3. *x* aplicativo está trabalhando com um ODBC 2. *x* driver, consulte [Funções de substituição de mapeamento para compatibilidade retrógrada de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 [Entrada] Alça de declaração.  
  
 *ColumnNumber*  
 [Entrada] O número do registro no IRD do qual o valor de campo deve ser recuperado. Este argumento corresponde ao número de coluna de dados de resultados, ordenado sequencialmente em ordem de coluna crescente, a partir de 1. As colunas podem ser descritas em qualquer ordem.  
  
 A coluna 0 pode ser especificada neste argumento, mas todos os valores, exceto SQL_DESC_TYPE e SQL_DESC_OCTET_LENGTH, retornarão valores indefinidos.  
  
 *FieldIdentifier*  
 [Entrada] A alça do descritor. Esta alça define qual campo no IRD deve ser consultado (por exemplo, SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 [Saída] Ponteiro para um buffer no qual para retornar o valor no campo *FieldIdentifier* da linha *ColunaNúmero* do IRD, se o campo for uma seqüência de caracteres. Caso contrário, o campo não será usado.  
  
 Se *CharacterAttributePtr* for NULL, *StringLengthLengthTr* ainda retornará o número total de bytes (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *CharacterAttributePtr*.  
  
 *BufferLength*  
 [Entrada] Se *FieldIdentifier* é um campo definido pelo ODBC e *OAttributePtr de caracteres* aponta \*para uma seqüência de caracteres ou buffer binário, esse argumento deve ser o comprimento do *CharacterAttributePtr*. Se *FieldIdentifier* é um campo definido \*pelo ODBC e *CharacterAttribute*Ptr é um inteiro, este campo será ignorado. Se o * \*CharacterAttributePtr* for uma seqüência unicode (ao chamar **SQLColAttributeW),** o argumento *BufferLength* deve ser um número uniforme. Se *fieldIdentifier* for um campo definido pelo driver, o aplicativo indicará a natureza do campo para o Gerenciador de driver, definindo o argumento *BufferLength.* *BufferLength* pode ter os seguintes valores:  
  
-   Se *CharacterAttributePtr* for um ponteiro para um ponteiro, *BufferLength* deve ter o valor SQL_IS_POINTER.  
  
-   Se *CharacterAttributePtr* é um ponteiro para uma seqüência de caracteres, o *BufferLength* é o comprimento do buffer.  
  
-   Se *CharacterAttributePtr* for um ponteiro para um buffer binário, o aplicativo coloca o resultado da macro*SQL_LEN_BINARY_ATTR(comprimento)* em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *CharacterAttributePtr* for um ponteiro para um tipo de dados de comprimento fixo, *bufferLength* deve ser um dos seguintes: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT ou SQLUSMALLINT.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o byte de rescisão nula para dados de caracteres) disponível para retornar em **CharacterAttributePtr*.  
  
 Para dados de caracteres, se o número de bytes disponíveis para retornar for \*maior ou igual a *BufferLength,* as informações do descritor em *CharacterAttributePtr* são truncadas para *BufferLength* menos o comprimento de um caractere de rescisão nula e é anulada nula pelo driver.  
  
 Para todos os outros tipos de dados, o valor do *BufferLength* é ignorado e o driver assume que o tamanho de **CharacterAttributePtr* é de 32 bits.  
  
 *NumericAttributePtr*  
 [Saída] Pointer para um buffer inteiro no qual retornar o valor no campo *FieldIdentifier* da linha *ColunaNúmero* do IRD, se o campo for um tipo de descritor numérico, como SQL_DESC_COLUMN_LENGTH. Caso contrário, o campo não será usado. Observe que alguns drivers só podem escrever o buffer de 32 ou 16 bits inferior e deixar o bit de ordem superior inalterado. Portanto, os aplicativos devem inicializar o valor para 0 antes de chamar essa função.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLColAttribute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLColAttribute** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|O \*buffer *CharacterAttributePtr* não era grande o suficiente para retornar todo o valor da seqüência, de modo que o valor da seqüência foi truncado. O comprimento do valor da seqüência não truncado é devolvido em **StringLengthLengthPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07005|Declaração preparada não uma *especificação do cursor*|A declaração associada ao *StatementHandle* não retornou um conjunto de resultados e *o FieldIdentifier* não foi SQL_DESC_COUNT. Não havia colunas para descrever.|  
|07009|Índice de descritor inválido|(DM) O valor especificado para *O Número de Colunas* era igual a 0, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS era SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *ColumnNumber* foi maior do que o número de colunas no conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagField** da estrutura de dados de diagnóstico descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de concluir a execução, **sqlCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um segmento diferente em um aplicativo multithread.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função ayncrona ainda estava sendo executada quando SQLColAttribute foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) A função foi chamada antes de chamar **SQLPrepare,** **SQLExecDirect**ou uma função de catálogo para o *StatementHandle*.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) * \*CharacterAttributePtr* é uma seqüência de caracteres, e *BufferLength* era menor que 0, mas não igual a SQL_NTS.|  
|HY091|Identificador de campo de descritor inválido|O valor especificado para o argumento *FieldIdentifier* não era um dos valores definidos e não era um valor definido pela implementação.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Motorista não é capaz|O valor especificado para o argumento *FieldIdentifier* não foi suportado pelo driver.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 Quando chamado após **o SQLPrepare** e antes **do SQLExecute,** **o SQLColAttribute** pode retornar qualquer SQLSTATE que possa ser devolvido pelo **SQLPrepare** ou **SQLExecute,** dependendo de quando a fonte de dados avaliar a declaração SQL associada ao *StatementHandle*.  
  
 Por razões de desempenho, um aplicativo não deve chamar **SQLColAttribute** antes de executar uma declaração.  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre como os aplicativos usam as informações retornadas pelo **SQLColAttribute,** consulte [Metadados do conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** retorna informações \*em *NumericAttributePtr* ou em \* *CharacterAttributePtr*. As informações de inteiro \*são retornadas no *NumericAttributePtr* como um valor SQLLEN; todos os outros formatos de \*informação são retornados no *CharacterAttributePtr*. Quando as informações \*são retornadas em *NumericAttributePtr,* o driver ignora *CharacterAttributePtr,* *BufferLength*e *StringLengthPtr*. Quando as informações \*são retornadas no *CharacterAttributePtr,* o driver ignora *NumericAttributePtr*.  
  
 **SQLColAttribute** retorna valores dos campos descritores do IRD. A função é chamada com uma alça de declaração em vez de uma alça descritor. Os valores retornados pelo **SQLColAttribute** para os valores *fieldIdentifier* listados posteriormente nesta seção também podem ser recuperados ligando para **SQLGetDescField** com a alça IRD apropriada.  
  
 Os campos descritores atualmente definidos, a versão do ODBC em que foram introduzidos e os argumentos nos quais as informações são devolvidas para eles são mostrados mais tarde nesta seção; mais tipos de descritores podem ser definidos pelos drivers para tirar proveito de diferentes fontes de dados.  
  
 Um ODBC 3. *x* driver deve retornar um valor para cada um dos campos descritores. Se um campo descritor não se aplicar a um driver ou fonte de \*dados e, salvo indicação em contrário, o driver retorna 0 em *StringLengthPtr* ou uma string vazia em **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 O ODBC 3. *x* função **SQLColAttribute** substitui o ODBC 2 depreciado. *x* função **SQLColAttributes**. Ao mapear **SQLColAttributes** to **SQLColAttribute** (quando um ODBC 2.* x* aplicativo está trabalhando com um ODBC 3. *x* driver), ou mapeamento **SQLColAttribute** to **SQLColAttributes** (quando um ODBC 3.* x* aplicativo está trabalhando com um ODBC 2. *x* driver), o Driver Manager passa o valor do *FieldIdentifier* através, mapeia-o para um novo valor ou retorna um erro, da seguinte forma:  
  
> [!NOTE]  
>  O prefixo usado nos valores *fieldidentifier* em ODBC 3. *x* foi alterado do usado no ODBC 2. *x*. O novo prefixo é "SQL_DESC"; o prefixo antigo era "SQL_COLUMN".  
  
-   Se o **valor #define** do ODBC 2. *x* *FieldIdentifier* é o mesmo que o valor **#define** do ODBC 3. *x* *FieldIdentifier*, o valor na chamada de função é apenas passado.  
  
-   Os **valores #define** da ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION e SQL_COLUMN_SCALE são diferentes dos valores **#define** do ODBC 3. *x* *FieldIdentifiers* SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_LENGTH. Um ODBC 2. *x* driver só precisa de suporte ao ODBC 2. *x* valores. Um ODBC 3. *x* driver deve suportar os valores "SQL_COLUMN" e "SQL_DESC" para esses três *FieldIdentifiers*. Esses valores são diferentes porque precisão, escala e comprimento são definidos de forma diferente no ODBC 3. *x* do que estavam em ODBC 2. *x*. Para obter mais informações, consulte [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho do display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
-   Se o **valor #define** do ODBC 2. *x* *FieldIdentifier* é diferente do valor **#define** do ODBC 3. *x* *FieldIdentifier*, como ocorre com os valores COUNT, NAME e NULLABLE, o valor na chamada de função é mapeado para o valor correspondente. Por exemplo, SQL_COLUMN_COUNT é mapeada para SQL_DESC_COUNT, e SQL_DESC_COUNT é mapeada para SQL_COLUMN_COUNT, dependendo da direção do mapeamento.  
  
-   Se *FieldIdentifier* é um novo valor no ODBC 3. *x*, para o qual não houve valor correspondente em ODBC 2. *x*, não será mapeado quando um ODBC 3. *x* aplicativo usa-o em uma chamada para **SQLColAttribute** em um ODBC 2. *x* driver, e a chamada retornará SQLSTATE HY091 (identificador de campo descritor inválido).  
  
 A tabela a seguir lista os tipos de descritores retornados pelo **SQLColAttribute**. O tipo de valores *NumericAttributePtr* é **SQLLEN \* **.  
  
|*FieldIdentifier*|Informações<br /><br /> voltou em|Descrição|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna for uma coluna de autoincrementamento.<br /><br /> SQL_FALSE se a coluna não for uma coluna de autoincrementamento ou não for numérica.<br /><br /> Este campo é válido apenas para colunas de tipo de dados numéricos. Um aplicativo pode inserir valores em uma linha contendo uma coluna de incremento automático, mas normalmente não é possível atualizar valores na coluna.<br /><br /> Quando uma inserção é feita em uma coluna de autoincremento, um valor único é inserido na coluna no momento da inserção. O incremento não é definido, mas é específico da fonte de dados. Um aplicativo não deve assumir que uma coluna de autoincremento é iniciada em qualquer ponto ou incrementa por qualquer valor específico.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|O nome da coluna base para a coluna conjunto de resultados. Se um nome de coluna base não existir (como no caso de colunas que são expressões), então esta variável contém uma seqüência de string vazia.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_BASE_COLUMN_NAME do IRD, que é um campo somente leitura.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|O nome da tabela base que contém a coluna. Se o nome da tabela base não puder ser definido ou não for aplicável, esta variável contém uma seqüência de string vazia.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_BASE_TABLE_NAME do IRD, que é um campo somente leitura.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna for tratada como sensível a maiúsculas e minúsculas para colagens e comparações.<br /><br /> SQL_FALSE se a coluna não for tratada como sensível a maiúsculas e minúsculas para colagens e comparações ou não for de caráter.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|O catálogo da tabela que contém a coluna. O valor retornado é definido pela implementação se a coluna é uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não suportar catálogos ou o nome do catálogo não puder ser determinado, uma seqüência de string vazia será devolvida. Este campo de registro VARCHAR não se limita a 128 caracteres.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|O tipo de dados concisos.<br /><br /> Para os tipos de dados de data e intervalo, este campo retorna o tipo de dados concisos; por exemplo, SQL_TYPE_TIME ou SQL_INTERVAL_YEAR. (Para obter mais informações, consulte [identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) no apêndice D: Tipos de dados.)<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_CONCISE_TYPE do IRD.|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|O número de colunas disponíveis no conjunto de resultados. Isso retorna 0 se não houver colunas no conjunto de resultados. O valor no argumento *ColunaNúmero* é ignorado.<br /><br /> Essas informações são devolvidas do campo de cabeçalho SQL_DESC_COUNT do IRD.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|Número máximo de caracteres necessários para exibir dados da coluna. Para obter mais informações sobre o tamanho do display, consulte [Tamanho da coluna, dígitos decimais, comprimento do octeto de transferência e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no apêndice D: Tipos de dados.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna tiver uma precisão fixa e uma escala não zero que sejam específicas da fonte de dados.<br /><br /> SQL_FALSE se a coluna não tiver uma escala fixa de precisão e não zero específica da fonte de dados.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|O rótulo ou título da coluna. Por exemplo, uma coluna chamada EmpName pode ser rotulada como Nome do Funcionário ou pode ser rotulada com um alias.<br /><br /> Se uma coluna não tiver uma etiqueta, o nome da coluna será devolvido. Se a coluna não for rotulada e sem nome, uma seqüência vazia será devolvida.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que é o comprimento máximo ou real do caractere de uma seqüência de caracteres ou tipo de dados binários. É o comprimento máximo de caractere para um tipo de dados de comprimento fixo, ou o comprimento real do caractere para um tipo de dados de comprimento variável. Seu valor sempre exclui o byte de rescisão nula que termina a seqüência de caracteres.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_LENGTH do IRD.<br /><br /> Para obter mais informações sobre o comprimento, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro VARCHAR(128) contém o caractere ou caracteres que o driver reconhece como um prefixo para um literal deste tipo de dados. Este campo contém uma seqüência vazia para um tipo de dados para o qual um prefixo literal não é aplicável. Para obter mais informações, consulte [Prefixos e Sufixos Literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro VARCHAR(128) contém o caractere ou caracteres que o driver reconhece como um sufixo para um literal deste tipo de dados. Este campo contém uma seqüência vazia para um tipo de dados para o qual um sufixo literal não é aplicável. Para obter mais informações, consulte [Prefixos e Sufixos Literais](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro VARCHAR(128) contém qualquer nome localizado (língua nativa) para o tipo de dados que pode ser diferente do nome regular do tipo de dados. Se não houver um nome localizado, então uma seqüência vazia é devolvida. Este campo é apenas para fins de exibição. O conjunto de caracteres da seqüência é dependente de localidade e é tipicamente o conjunto de caracteres padrão do servidor.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|O alias da coluna, se for aplicado. Se o alias da coluna não se aplicar, o nome da coluna será devolvido. Em ambos os casos, SQL_DESC_UNNAMED está definido para SQL_NAMED. Se não houver nome de coluna ou um alias de coluna, uma seqüência de string vazia será devolvida e SQL_DESC_UNNAMED está definida como SQL_UNNAMED.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_NAME do IRD.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ anulado se a coluna puder ter valores NULOS; SQL_NO_NULLS se a coluna não tiver valores NULOS; ou SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores NULOS.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_NULLABLE do IRD.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|Se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico aproximado, este campo SQLINTEGER contém um valor de 2 porque o campo SQL_DESC_PRECISION contém o número de bits. Se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico exato, este campo contém um valor de 10 porque o campo SQL_DESC_PRECISION contém o número de dígitos decimais. Este campo está definido como 0 para todos os tipos de dados não numéricos.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|O comprimento, em bytes, de uma seqüência de caracteres ou tipo de dados binários. Para caracteres de comprimento fixo ou tipos binários, este é o comprimento real em bytes. Para caracteres de comprimento variável ou tipos binários, este é o comprimento máximo em bytes. Este valor não inclui o exterminador nulo.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_OCTET_LENGTH do IRD.<br /><br /> Para obter mais informações sobre o comprimento, consulte [Tamanho da coluna, Dígitos decimais, Comprimento do Octeto de Transferência e Tamanho do Display](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice D: Tipos de dados.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que para um tipo de dados numérico denota a precisão aplicável. Para tipos de dados SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP e todos os tipos de dados de intervalo que representam um intervalo de tempo, seu valor é a precisão aplicável do componente de segundos fracionados.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_PRECISION do IRD.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que é a escala aplicável para um tipo de dados numérico. Para os tipos de dados DECIMAL e NUMERIC, esta é a escala definida. É indefinido para todos os outros tipos de dados.<br /><br /> Essas informações são devolvidas do campo de registro SCALE do IRD.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|O esquema da tabela que contém a coluna. O valor retornado é definido pela implementação se a coluna é uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não suportar esquemas ou o nome do esquema não puder ser determinado, uma seqüência de string vazia será devolvida. Este campo de registro VARCHAR não se limita a 128 caracteres.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE se a coluna não puder ser usada em uma cláusula WHERE. (Este é o mesmo valor SQL_UNSEARCHABLE em ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se a coluna pode ser usada em uma cláusula WHERE, mas apenas com o predicado LIKE. (Este é o mesmo valor SQL_LIKE_ONLY em ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se a coluna puder ser usada em uma cláusula WHERE com todos os operadores de comparação, exceto LIKE. (Este é o mesmo valor SQL_EXCEPT_LIKE em ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE se a coluna pode ser usada em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> Colunas de SQL_LONGVARCHAR tipo e SQL_LONGVARBINARY geralmente retornam SQL_PRED_CHAR.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|O nome da tabela que contém a coluna. O valor retornado é definido pela implementação se a coluna é uma expressão ou se a coluna faz parte de uma exibição.<br /><br /> Se o nome da tabela não puder ser determinado, uma seqüência vazia será devolvida.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que especifica o tipo de dados SQL.<br /><br /> Quando *o ColumnNumber* é igual a 0, SQL_BINARY é devolvido para marcadores de comprimento variável e SQL_INTEGER é devolvido para marcadores de comprimento fixo.<br /><br /> Para os tipos de dados de data e intervalo, este campo retorna o tipo de dados verboso: SQL_DATETIME ou SQL_INTERVAL. (Para obter mais informações, consulte [identificadores e descritores de tipo de dados](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) no apêndice D: Tipos de dados.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_TYPE do IRD. **Nota:**  Para trabalhar contra o ODBC 2. *x* drivers, use SQL_DESC_CONCISE_TYPE em vez disso.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|Nome do tipo de dados dependente da fonte de dados; por exemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" ou "CHAR ( ) FOR BIT DATA".<br /><br /> Se o tipo for desconhecido, uma seqüência vazia será devolvida.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED ou SQL_UNNAMED. Se o campo SQL_DESC_NAME do IRD contiver um alias de coluna ou um nome de coluna, SQL_NAMED será devolvido. Se não houver nome de coluna ou alias de coluna, SQL_UNNAMED é devolvido.<br /><br /> Essas informações são devolvidas do campo de registro SQL_DESC_UNNAMED do IRD.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna não estiver assinada (ou não numérica).<br /><br /> SQL_FALSE se a coluna estiver assinada.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|A coluna é descrita pelos valores para as constantes definidas:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE descreve a updatability da coluna no conjunto de resultados, não a coluna na tabela base. A updatability da coluna base na qual a coluna de conjunto de resultados é baseada pode ser diferente do valor neste campo. Se uma coluna é updatable pode ser baseada no tipo de dados, privilégios de usuário e a definição do conjunto de resultados em si. Se não estiver claro se uma coluna é updatable, SQL_ATTR_READWRITE_UNKNOWN deve ser devolvida.|  
  
 **SQLColAttribute** é uma alternativa extensível ao **SQLDescribeCol**. **SQLDescribeCol** retorna um conjunto fixo de informações do descritor com base no SQL ANSI-89. **O SQLColAttribute** permite acesso ao conjunto mais extenso de informações de descritores disponíveis nas extensões de fornecedor ANSI SQL-92 e DBMS.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Vinculando um buffer a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelamento do processamento de declarações|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Exemplo  
 O código de amostra a seguir não libera alças e conexões. Consulte [SQLFreeHandle Function](../../../odbc/reference/syntax/sqlfreehandle-function.md), [Sample ODBC Program](../../../odbc/reference/sample-odbc-program.md)e [SQLFreeStmt Function](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obter amostras de código para obter alças e instruções gratuitas.  
  
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
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)
