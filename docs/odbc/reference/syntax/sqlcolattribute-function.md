---
title: Função SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5afbe6bbea4e1c50e3b16742bf5d0fa1b3c16a9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922980"
---
# <a name="sqlcolattribute-function"></a>Função SQLColAttribute
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLColAttribute** retorna informações de descritor para uma coluna em um conjunto de resultados. Informações do descritor são retornadas como uma cadeia de caracteres, um valor de descritor dependente ou um valor inteiro.  
  
> [!NOTE]  
>  Para obter mais informações sobre o que o Gerenciador de Driver mapeia essa função quando um ODBC 3. *x* aplicativo estiver trabalhando com um ODBC 2. *x* driver, consulte [mapeamento de funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução.  
  
 *ColumnNumber*  
 [Entrada] O número do registro do IRD do qual o valor do campo é a ser recuperado. Esse argumento corresponde ao número da coluna de dados de resultado, ordenados consecutivamente em ordem crescente de coluna, começando em 1. Colunas podem ser descritas em qualquer ordem.  
  
 A coluna 0 pode ser especificada neste argumento, mas todos os valores exceto SQL_DESC_TYPE e SQL_DESC_OCTET_LENGTH retornará valores indefinidos.  
  
 *FieldIdentifier*  
 [Entrada] O identificador do descritor. Esse identificador define qual campo do IRD deve ser consultado (por exemplo, SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 [Saída] Ponteiro para um buffer no qual retornar o valor de *FieldIdentifier* campo do *ColumnNumber* linha do ird, se o campo for uma cadeia de caracteres. Caso contrário, o campo é usado.  
  
 Se *CharacterAttributePtr* for NULL, *StringLengthPtr* ainda retornará o número total de bytes (excluindo o caractere null de terminação para dados de caractere) disponível no buffer de retorno apontada pelo *CharacterAttributePtr*.  
  
 *BufferLength*  
 [Entrada] Se *FieldIdentifier* é um campo definido pelo ODBC e *CharacterAttributePtr* aponta para um buffer binário ou de cadeia de caracteres, esse argumento deve ser o comprimento de \*  *CharacterAttributePtr*. Se *FieldIdentifier* é um campo definido pelo ODBC e \* *CharacterAttribute*Ptr é um número inteiro, este campo será ignorado. Se o  *\*CharacterAttributePtr* é uma cadeia de caracteres Unicode (ao chamar **SQLColAttributeW**), o *BufferLength* argumento deve ser um número par. Se *FieldIdentifier* é um campo definido pelo driver, o aplicativo indica a natureza do campo para o Gerenciador de Driver, definindo o *BufferLength* argumento. *BufferLength* pode ter os seguintes valores:  
  
-   Se *CharacterAttributePtr* é um ponteiro para um ponteiro *BufferLength* devem ter o valor SQL_IS_POINTER.  
  
-   Se *CharacterAttributePtr* é um ponteiro para uma cadeia de caracteres, o *BufferLength* é o comprimento do buffer.  
  
-   Se *CharacterAttributePtr* é um ponteiro para um buffer de binário, os locais de aplicativo o resultado da SQL_LEN_BINARY_ATTR (*comprimento*) macro em *BufferLength*. Isso coloca um valor negativo em *BufferLength*.  
  
-   Se *CharacterAttributePtr* é um ponteiro para um tipo de dados de comprimento fixo, *BufferLength* deve ser um dos seguintes: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT ou SQLUSMALLINT.  
  
 *StringLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de bytes (excluindo o byte nulo de terminação para dados de caractere) disponíveis para retornar em **CharacterAttributePtr*.  
  
 Para dados de caracteres, se o número de bytes disponíveis para retornar é maior que ou igual a *BufferLength*, as informações de descritor no \* *CharacterAttributePtr* será truncado para  *BufferLength* menos o comprimento de um caractere null de terminação e é terminada em nulo pelo driver.  
  
 Todos os outros tipos de dados, o valor de *BufferLength* é ignorada e o driver pressupõe que o tamanho de **CharacterAttributePtr* é de 32 bits.  
  
 *NumericAttributePtr*  
 [Saída] Ponteiro para um buffer de inteiro no qual retornar o valor de *FieldIdentifier* campo do *ColumnNumber* linha do ird, se o campo for um tipo de descritor numérico, como SQL_DESC_COLUMN_LENGTH. Caso contrário, o campo é usado. Observe que alguns drivers podem gravar somente inferior 32 bits ou 16 bits de um buffer e deixe o bit de ordem superior inalterado. Portanto, aplicativos devem inicializar o valor para 0 antes de chamar essa função.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLColAttribute** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType*sql_handle_stmt e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLColAttribute** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|O buffer \* *CharacterAttributePtr* não era grande o suficiente para retornar o valor de cadeia de caracteres inteira, para que o valor de cadeia de caracteres foi truncado. O comprimento do valor completo da cadeia de caracteres é retornado em **StringLengthPtr*. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07005|Instrução preparada não um *especificação de cursor*|A instrução associada a *StatementHandle* não retornou um conjunto de resultados e *FieldIdentifier* não era SQL_DESC_COUNT. Não havia nenhuma coluna para descrever.|  
|07009|Índice do descritor inválido|(DM) o valor especificado para *ColumnNumber* igual a 0, e o atributo de instrução SQL_ATTR_USE_BOOKMARKS era SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *ColumnNumber* era maior que o número de colunas no conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagField** de dados de diagnóstico estrutura descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em uma aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrono ainda estava em execução quando SQLColAttribute foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM), a função foi chamada antes de chamar **SQLPrepare**, **SQLExecDirect**, ou uma função de catálogo para o *StatementHandle*.<br /><br /> (DM) uma função de execução assíncrona (não la) foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM)  *\*CharacterAttributePtr* é uma cadeia de caracteres, e *BufferLength* era menor que 0 mas não igual a SQL_NTS.|  
|HY091|Identificador de campo de descritor inválido|O valor especificado para o argumento *FieldIdentifier* não era um dos valores definidos e não era um valor definido pela implementação.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Driver não funciona|O valor especificado para o argumento *FieldIdentifier* não era compatível com o driver.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem está desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior na alça retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
 Quando chamado depois **SQLPrepare** e antes de **SQLExecute**, **SQLColAttribute** pode retornar qualquer SQLSTATE que pode ser retornado por **SQLPrepare**ou **SQLExecute**, dependendo de quando a fonte de dados avalia a instrução SQL associada a *StatementHandle*.  
  
 Por motivos de desempenho, um aplicativo não deve chamar **SQLColAttribute** antes de executar uma instrução.  
  
## <a name="comments"></a>Comentários  
 Para obter informações sobre como os aplicativos usam as informações retornadas por **SQLColAttribute**, consulte [metadados de conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** retorna informações ou em \* *NumericAttributePtr* ou \* *CharacterAttributePtr*. Informações de inteiro são retornadas no \* *NumericAttributePtr* como um valor SQLLEN; todos os outros formatos de informações são retornados em \* *CharacterAttributePtr*. Quando as informações são retornadas em \* *NumericAttributePtr*, o driver ignorará *CharacterAttributePtr*, *BufferLength*, e  *StringLengthPtr*. Quando as informações são retornadas em \* *CharacterAttributePtr*, o driver ignorará *NumericAttributePtr*.  
  
 **SQLColAttribute** retorna valores de campos de descritor do ird. A função é chamada com um identificador de instrução, em vez de um identificador do descritor. Os valores retornados por **SQLColAttribute** para o *FieldIdentifier* valores listados mais adiante nesta seção também podem ser recuperados chamando **SQLGetDescField** com o Identificador IRD apropriado.  
  
 Campos de descritor definido no momento, a versão do ODBC no qual eles foram introduzidos e os argumentos na qual as informações são retornadas para que eles são mostrados mais adiante nesta seção; mais tipos de descritor podem ser definidos por drivers para tirar proveito de diferentes fontes de dados.  
  
 ODBC 3. *x* driver deve retornar um valor para cada um dos campos de descritor. Se um campo de descritor não se aplica a uma fonte de dados ou driver e, a menos que indicado o contrário, o driver retorna 0 em \* *StringLengthPtr* ou uma cadeia de caracteres vazia **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Compatibilidade com versões anteriores  
 O ODBC 3. *x* função **SQLColAttribute** substitui o preterido ODBC 2. *x* função **SQLColAttributes**. Ao mapear **SQLColAttributes** para **SQLColAttribute** (quando um ODBC 2. *x* aplicativo estiver trabalhando com um ODBC 3. *x* driver), ou o mapeamento de **SQLColAttribute** para **SQLColAttributes** (quando um ODBC 3. *x* aplicativo estiver trabalhando com um ODBC 2. *x* driver), o Gerenciador de Driver ou passa o valor de *FieldIdentifier* , mapeia para um novo valor, ou retornar um erro, da seguinte maneira:  
  
> [!NOTE]  
>  O prefixo usado em *FieldIdentifier* valores em ODBC 3. *x* foi alterado do que o usado em ODBC 2. *x*. O novo prefixo é "SQL_DESC"; o prefixo antigo foi "SQL_COLUMN".  
  
-   Se o **#define** valor do ODBC 2. *x* *FieldIdentifier* é igual a **#define** valor ODBC 3. *x* *FieldIdentifier*, o valor na chamada de função é passado apenas.  
  
-   O **#define** valores do ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION e SQL_COLUMN_SCALE são diferentes de **#define** valores do ODBC 3. *x* *FieldIdentifiers* SQL_DESC_SCALE, SQL_DESC_PRECISION e SQL_DESC_LENGTH. ODBC 2. *x* driver precisa dar suporte apenas do ODBC 2. *x* valores. ODBC 3. *x* driver deve oferecer suporte a valores de "SQL_COLUMN" e "SQL_DESC" para esses três *FieldIdentifiers*. Esses valores são diferentes porque a precisão, escala e comprimento são definidos de forma diferente em ODBC 3. *x* que estavam no ODBC 2. *x*. Para obter mais informações, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
-   Se o **#define** valor do ODBC 2. *x* *FieldIdentifier* é diferente de **#define** valor ODBC 3. *x* *FieldIdentifier*, assim como ocorre com a contagem, nome, e valores nulos, o valor na chamada de função é mapeada para o valor correspondente. Por exemplo, SQL_COLUMN_COUNT é mapeado para SQL_DESC_COUNT, e SQL_DESC_COUNT é mapeada para SQL_COLUMN_COUNT, dependendo da direção do mapeamento.  
  
-   Se *FieldIdentifier* é um novo valor em ODBC 3. *x*, para que nenhum valor correspondente foi no ODBC 2. *x*, não será mapeada quando um ODBC 3. *x* aplicativo usá-los em uma chamada para **SQLColAttribute** em um ODBC 2. *x* driver e a chamada retornará SQLSTATE HY091 (identificador de campo de descritor inválido).  
  
 A tabela a seguir lista os tipos de descritor retornados por **SQLColAttribute**. O tipo de *NumericAttributePtr* valores é **SQLLEN \*** .  
  
|*FieldIdentifier*|Informações<br /><br /> retornado em|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna é uma coluna de incremento automático.<br /><br /> SQL_FALSE se a coluna não é uma coluna de incremento automático ou não for numérica.<br /><br /> Esse campo é válido para somente colunas de tipo de dados numéricos. Um aplicativo pode inserir valores em uma linha que contém uma coluna autoincrement, mas geralmente não é possível atualizar os valores na coluna.<br /><br /> Quando uma inserção é feita em uma coluna autoincrement, um valor exclusivo é inserido na coluna em tempo de inserção. O incremento não está definido, mas é específico da fonte de dados. Um aplicativo não deve presumir que uma coluna autoincrement inicia em qualquer momento determinado ou incrementos de qualquer valor específico.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|O nome da coluna de base para o resultado definir coluna. Se não existir um nome de coluna de base (como no caso de colunas que são expressões), essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_BASE_COLUMN_NAME do ird, que é um campo somente leitura.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|O nome da tabela base que contém a coluna. Se o nome da tabela base não pode ser definido ou não é aplicável, essa variável conterá uma cadeia de caracteres vazia.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_BASE_TABLE_NAME do ird, que é um campo somente leitura.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna é tratada como diferencia maiusculas de minúsculas para agrupamentos e comparações.<br /><br /> SQL_FALSE se a coluna não é tratada como diferencia maiusculas de minúsculas para agrupamentos e comparações ou for não caractere.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|O catálogo da tabela que contém a coluna. O valor retornado é definido pela implementação se a coluna é uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não oferece suporte a catálogos ou o nome do catálogo não pode ser determinado, uma cadeia de caracteres vazia é retornada. Este campo de registro VARCHAR não está limitado a 128 caracteres.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|O tipo de dados concisa.<br /><br /> Para os tipos de dados datetime e intervalo, esse campo retorna o tipo de dados conciso; Por exemplo, SQL_TYPE_TIME ou SQL_INTERVAL_YEAR. (Para obter mais informações, consulte [identificadores de tipo de dados e os descritores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) no Apêndice d: os tipos de dados.)<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_CONCISE_TYPE do ird.|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|O número de colunas disponíveis no conjunto de resultados. Isso retornará 0 se não houver nenhuma coluna no conjunto de resultados. O valor de *ColumnNumber* argumento será ignorado.<br /><br /> Essas informações são retornadas do campo de cabeçalho SQL_DESC_COUNT do ird.|  
|COLUNAS DE SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|Número máximo de caracteres necessários para exibir dados da coluna. Para obter mais informações sobre o tamanho de exibição, consulte [tamanho da coluna, dígitos decimais, o comprimento do octeto transferir e exibir tamanho](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna tem uma precisão fixa e uma escala diferente de zero que são específico da fonte de dados.<br /><br /> SQL_FALSE se a coluna não tem uma precisão fixa e uma escala diferente de zero que são específico da fonte de dados.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|O rótulo da coluna ou o título. Por exemplo, uma coluna denominada EmpName pode ser rotulado como nome do funcionário, ou pode ser rotulada com um alias.<br /><br /> Se uma coluna não tem um rótulo, o nome da coluna é retornado. Se a coluna for sem rótulo e sem nome, uma cadeia de caracteres vazia é retornada.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que é o comprimento de caracteres real ou máximo de um dado binário ou cadeia de caracteres de tipo. É o número máximo de caracteres para um tipo de dados de comprimento fixo ou o comprimento de caracteres real para um tipo de dados de comprimento variável. O valor sempre exclui o byte nulo de terminação que encerra a cadeia de caracteres.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_LENGTH do ird.<br /><br /> Para obter mais informações sobre o tamanho, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro de varchar (128) contém um ou mais caracteres que o driver reconhece como um prefixo para um literal deste tipo de dados. Este campo contém uma cadeia de caracteres vazia para um tipo de dados para o qual um prefixo de literal não é aplicável. Para obter mais informações, consulte [Literal prefixos e sufixos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro de varchar (128) contém um ou mais caracteres que o driver reconhece como um sufixo para um literal deste tipo de dados. Este campo contém uma cadeia de caracteres vazia para um tipo de dados para o qual um sufixo literal não é aplicável. Para obter mais informações, consulte [Literal prefixos e sufixos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro de varchar (128) contém qualquer nome localizado (idioma nativo) para o tipo de dados que pode ser diferente do nome do tipo de dados regular. Se não houver nenhum nome localizado, uma cadeia de caracteres vazia é retornada. Este campo é somente para exibição. O conjunto de caracteres da cadeia de caracteres é dependente de localidade e normalmente é o conjunto de caracteres padrão do servidor.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|O alias de coluna, se aplicável. Se o alias de coluna não for aplicável, o nome da coluna é retornado. Em ambos os casos, SQL_DESC_UNNAMED é definido como SQL_NAMED. Se não houver nenhum nome de coluna ou um alias de coluna, uma cadeia de caracteres vazia é retornada e SQL_DESC_UNNAMED é definido como SQL_UNNAMED.<br /><br /> Essas informações são retornadas do campo SQL_DESC_NAME de registro do ird.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL _ permite valor nulo se a coluna pode ter valores NULL. SQL_NO_NULLS se a coluna não tiver valores NULL. ou SQL_NULLABLE_UNKNOWN se não se sabe se a coluna aceita valores nulos.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_NULLABLE do ird.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|Se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico aproximado, este campo sqlinteger que contém contém um valor de 2 porque o campo SQL_DESC_PRECISION contém o número de bits. Se o tipo de dados no campo SQL_DESC_TYPE for um tipo de dados numérico exato, este campo contém um valor de 10, porque o campo SQL_DESC_PRECISION contém o número de dígitos decimais. Este campo é definido como 0 para todos os tipos de dados não numéricos.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|O comprimento, em bytes, de um tipo de dados de binário ou cadeia de caracteres. Para caracteres de comprimento fixo ou tipos binários, este é o comprimento real em bytes. Para caracteres de comprimento variável ou tipos binários, este é o comprimento máximo em bytes. Esse valor não inclui o terminador nulo.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_OCTET_LENGTH do ird.<br /><br /> Para obter mais informações sobre o tamanho, consulte [tamanho da coluna, dígitos decimais, transferir o comprimento do octeto e tamanho de exibição](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) no Apêndice d: os tipos de dados.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que indica a precisão aplicável para um tipo de dados numérico. Para tipos de dados SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, e todos os tipos de dados de intervalo que representam um intervalo de tempo, seu valor é a precisão aplicável do componente de segundos fracionários.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_PRECISION do ird.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que é a escala aplicável para um tipo de dados numérico. Para tipos de dados decimais e numéricos, esta é a escala definida. É indefinido para todos os outros tipos de dados.<br /><br /> Essas informações são retornadas do campo de registro de escala do ird.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|O esquema da tabela que contém a coluna. O valor retornado é definido pela implementação se a coluna é uma expressão ou se a coluna faz parte de uma exibição. Se a fonte de dados não dá suporte a esquemas ou o nome do esquema não pode ser determinado, uma cadeia de caracteres vazia é retornada. Este campo de registro VARCHAR não está limitado a 128 caracteres.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE se a coluna não pode ser usada em uma cláusula WHERE. (Isso é igual ao valor SQL_UNSEARCHABLE no ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR se a coluna pode ser usada em uma cláusula WHERE, mas apenas com o predicado LIKE. (Isso é igual ao valor SQL_LIKE_ONLY no ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC se a coluna pode ser usada em uma cláusula WHERE com todos os operadores de comparação exceto SEMELHANTE. (Isso é igual ao valor SQL_EXCEPT_LIKE no ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE se a coluna pode ser usada em uma cláusula WHERE com qualquer operador de comparação.<br /><br /> Colunas de tipo SQL_LONGVARCHAR e SQL_LONGVARBINARY SQL_PRED_CHAR de retorno normalmente.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|O nome da tabela que contém a coluna. O valor retornado é definido pela implementação se a coluna é uma expressão ou se a coluna faz parte de uma exibição.<br /><br /> Se o nome da tabela não pode ser determinado, uma cadeia de caracteres vazia é retornada.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|Um valor numérico que especifica o tipo de dados SQL.<br /><br /> Quando *ColumnNumber* é igual a 0, SQL_BINARY é retornado para os indicadores de comprimento variável e SQL_INTEGER é retornado para os indicadores de comprimento fixo.<br /><br /> Para os tipos de dados datetime e intervalo, esse campo retorna o tipo de dados detalhado: SQL_DATETIME ou SQL_INTERVAL. (Para obter mais informações, consulte [identificadores de tipo de dados e os descritores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) no Apêndice d: os tipos de dados.<br /><br /> Essas informações são retornadas do campo SQL_DESC_TYPE de registro do ird. **Observação:** para trabalhar em ODBC 2. *x* drivers, use SQL_DESC_CONCISE_TYPE em vez disso.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|Nome do tipo de dados de origem dependente de dados; Por exemplo, "CHAR", "VARCHAR", "MONEY", "VARBINARY longo" ou "CHAR () para dados BIT".<br /><br /> Se o tipo é desconhecido, uma cadeia de caracteres vazia é retornada.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED ou SQL_UNNAMED. Se o campo SQL_DESC_NAME do ird contém um alias de coluna ou um nome de coluna, SQL_NAMED será retornado. Se não houver nenhum nome de coluna ou alias de coluna, SQL_UNNAMED será retornado.<br /><br /> Essas informações são retornadas do campo de registro SQL_DESC_UNNAMED do ird.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE se a coluna é não assinado (ou não numéricos).<br /><br /> SQL_FALSE se a coluna está assinada.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|Coluna é descrita pelos valores de constantes definidas:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE descreve a atualização de coluna no conjunto de resultados, não a coluna na tabela base. A atualização da coluna de base no qual se baseia a coluna do conjunto de resultados pode ser diferente do valor neste campo. Se uma coluna é atualizável pode ser com base no tipo de dados, privilégios de usuário e a definição do resultado definido automaticamente. Se não está claro se uma coluna é atualizável, SQL_ATTR_READWRITE_UNKNOWN devem ser retornados.|  
  
 **SQLColAttribute** é uma alternativa extensível para **SQLDescribeCol**. **SQLDescribeCol** retorna um conjunto fixo de informações com base em SQL ANSI-89 do descritor. **SQLColAttribute** permite o acesso ao conjunto mais amplo de informações de descritor disponíveis no ANSI SQL-92 e DBMS extensões do fornecedor.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Busca de várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Exemplo  
 O código de exemplo a seguir não libera identificadores e conexões. Consulte [função SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md), [exemplo ODBC programa](../../../odbc/reference/sample-odbc-program.md), e [função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md) para exemplos de código liberar identificadores e instruções.  
  
```  
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
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   retCode = SQLNumResultCols(hstmt, &numColumn);  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)
