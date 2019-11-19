---
title: Função SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1c89ff79ee0fcac37f7b6e231e957e051c9db2e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289289"
---
# <a name="sqlbindcol-function"></a>Função SQLBindCol
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 1,0: ISO 92  
  
 **Resumo**  
 O **SQLBindCol** associa buffers de dados de aplicativo a colunas no conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 Entrada Identificador de instrução.  
  
 *ColumnNumber*  
 Entrada Número da coluna do conjunto de resultados a ser associada. As colunas são numeradas no aumento da ordem das colunas, começando em 0, em que a coluna 0 é a coluna de indicadores. Se os indicadores não forem usados, ou seja, o atributo SQL_ATTR_USE_BOOKMARKS instrução será definido como SQL_UB_OFF-e os números de coluna começarão em 1.  
  
 *TargetType*  
 Entrada O identificador do tipo de dados C do buffer de \**TargetValuePtr* . Ao recuperar dados da fonte de dados com **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**ou **SQLSetPos**, o driver converte os dados para esse tipo; Quando ele envia dados para a fonte de dados com **SQLBulkOperations** ou **SQLSetPos**, o driver converte os dados desse tipo. Para obter uma lista de tipos de dados C válidos e identificadores de tipo, consulte a seção [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice D: tipos de dados.  
  
 Se o argumento *TargetType* for um tipo de dados de intervalo, a precisão inicial do intervalo padrão (2) e a precisão do intervalo padrão de segundos (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION de ARD, respectivamente, serão usados para os dados. Se o argumento *TargetType* for SQL_C_NUMERIC, a precisão padrão (definida pelo driver) e a escala padrão (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, serão usados para os dados. Se qualquer precisão ou escala padrão não for apropriada, o aplicativo deverá definir explicitamente o campo de descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Você também pode especificar um tipo de dados C estendido. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Entrada/saída adiada] Ponteiro para o buffer de dados a ser associado à coluna. **SQLFetch** e **SQLFetchScroll** retornam dados nesse buffer. **SQLBulkOperations** retorna dados nesse buffer quando a *operação* é SQL_FETCH_BY_BOOKMARK; Ele recupera dados desse buffer quando a *operação* é SQL_ADD ou SQL_UPDATE_BY_BOOKMARK. **SQLSetPos** retorna dados nesse buffer quando a *operação* é SQL_REFRESH; Ele recupera dados desse buffer quando a *operação* é SQL_UPDATE.  
  
 Se *TargetValuePtr* for um ponteiro nulo, o driver desassociará o buffer de dados para a coluna. Um aplicativo pode desassociar todas as colunas chamando **SQLFreeStmt** com a opção SQL_UNBIND. Um aplicativo pode desassociar o buffer de dados para uma coluna, mas ainda ter um buffer de comprimento/indicador associado para a coluna, se o argumento *TargetValuePtr* na chamada para **SQLBindCol** for um ponteiro nulo, mas o argumento *StrLen_or_IndPtr* for um valor válido.  
  
 *BufferLength*  
 Entrada Comprimento do buffer de *TargetValuePtr* de \*em bytes.  
  
 O driver usa *BufferLength* para evitar a gravação após o final do buffer de \**TargetValuePtr* quando ele retorna dados de comprimento variável, como caracteres ou dados binários. Observe que o driver conta o caractere de terminação nula quando retorna dados de caractere para \**TargetValuePtr*. \**TargetValuePtr* deve, portanto, conter espaço para o caractere de terminação nula ou o driver truncará os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um inteiro ou uma estrutura de data, o driver ignora *BufferLength* e assume que o buffer é grande o suficiente para manter os dados. Portanto, é importante para o aplicativo alocar um buffer suficientemente grande para dados de comprimento fixo ou o driver será gravado após o final do buffer.  
  
 **SQLBindCol** retorna SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido) quando *BufferLength* é menor que 0, mas não quando *BufferLength* é 0. No entanto, se *TargetType* especificar um tipo de caractere, um aplicativo não deverá definir *BufferLength* como 0, porque os drivers em conformidade com a CLI ISO retornam SQLSTATE HY090 (cadeia de caracteres ou comprimento de buffer inválido) nesse caso.  
  
 *StrLen_or_IndPtr*  
 [Entrada/saída adiada] Ponteiro para o buffer de comprimento/indicador para associar à coluna. **SQLFetch** e **SQLFetchScroll** retornam um valor nesse buffer. **SQLBulkOperations** recupera um valor desse buffer quando a *operação* é SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** retorna um valor nesse buffer quando a *operação* é SQL_FETCH_BY_BOOKMARK. **SQLSetPos** retorna um valor nesse buffer quando a *operação* é SQL_REFRESH; Ele recupera um valor desse buffer quando a *operação* é SQL_UPDATE.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**e **SQLSetPos** podem retornar os seguintes valores no buffer de comprimento/indicador:  
  
-   O comprimento dos dados disponíveis para retornar  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 O aplicativo pode colocar os seguintes valores no buffer de comprimento/indicador para uso com **SQLBulkOperations** ou **SQLSetPos**:  
  
-   O comprimento dos dados que estão sendo enviados  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   O resultado da macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Se o buffer do indicador e o tamanho do buffer forem buffers separados, o buffer do indicador poderá retornar apenas SQL_NULL_DATA, enquanto que o buffer de comprimento pode retornar todos os outros valores.  
  
 Para obter mais informações, consulte [função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md), [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)e [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Se *StrLen_or_IndPtr* for um ponteiro nulo, nenhum valor de comprimento ou indicador será usado. Este é um erro ao buscar dados e os dados são nulos.  
  
 Consulte [informações de ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md), se seu aplicativo for executado em um sistema operacional de 64 bits.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLBindCol** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um *identificador* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBindCol** e explica cada um no contexto dessa função; a notação "(DM)" precede as descrições de sqlstates retornadas pelo Gerenciador de driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário.  
  
|SQLSTATE|Error|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa específica do driver. (A função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|(DM) o argumento *ColumnNumber* era 0 e o argumento *TargetType* não foi SQL_C_BOOKMARK ou SQL_C_VARBOOKMARK.|  
|07009|Índice de descritor inválido|O valor especificado para o argumento *ColumnNumber* excedeu o número máximo de colunas no conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia um SQLSTATE específico e para o qual nenhum SQLSTATE específico de implementação foi definido. A mensagem de erro retornada por **SQLGetDiagRec** na *\*buffer MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar memória necessária para dar suporte à execução ou à conclusão da função.|  
|HY003|Tipo de buffer de aplicativo inválido|O argumento *TargetType* não era um tipo de dados válido nem SQL_C_DEFAULT.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado ao *StatementHandle*. Esta função assíncrona ainda estava em execução quando **SQLBindCol** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** foi chamado para *StatementHandle* e retornou SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**ou **SQLSetPos** foi chamado para o *StatementHandle* e retornou SQL_NEED_DATA. Esta função foi chamada antes de os dados serem enviados para todos os parâmetros de dados em execução ou colunas.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não puderam ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de cadeia de caracteres ou buffer inválido|(DM) o valor especificado para o argumento *BufferLength* era menor que 0.<br /><br /> (DM) o driver era um ODBC 2. *x* Driver, o argumento *ColumnNumber* foi definido como 0 e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY117|A conexão foi suspensa devido a um estado de transação desconhecido. Somente funções de desconexão e somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não oferece suporte à conversão especificada pela combinação do argumento *TargetType* e do tipo de dados SQL específico do driver da coluna correspondente.<br /><br /> O argumento *ColumnNumber* era 0 e o driver não oferece suporte a indicadores.<br /><br /> O driver dá suporte apenas ao ODBC 2. *x* e o argumento *TargetType* era um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados do intervalo C listados em [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice D: tipos de dados.<br /><br /> O driver só dá suporte a versões ODBC anteriores a 3,50, e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo limite de conexão expirado|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|O driver não oferece suporte a essa função|(DM) o driver associado ao *StatementHandle* não oferece suporte à função.|  
  
## <a name="comments"></a>Comentários  
 **SQLBindCol** é usado para *associar ou associar* colunas no conjunto de resultados a buffers de dados e buffers de comprimento/indicador no aplicativo. Quando o aplicativo chama **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos** para buscar dados, o driver retorna os dados para as colunas associadas nos buffers especificados; para obter mais informações, veja [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Quando o aplicativo chama **SQLBulkOperations** para atualizar ou inserir uma linha ou **SQLSetPos** para atualizar uma linha, o driver recupera os dados das colunas associadas dos buffers especificados; para obter mais informações, consulte [função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) ou [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md). Para obter mais informações sobre associação, consulte [recuperando resultados (básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Observe que as colunas não precisam estar associadas para recuperar dados delas. Um aplicativo também pode chamar **SQLGetData** para recuperar dados de colunas. Embora seja possível associar algumas colunas em uma linha e chamar **SQLGetData** para outras, isso está sujeito a algumas restrições. Para obter mais informações, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Associando, desvinculando e reassociando colunas  
 Uma coluna pode ser vinculada, desassociada ou reassociada a qualquer momento, mesmo depois que os dados forem obtidos do conjunto de resultados. A nova associação entrará em vigor na próxima vez que uma função que usa associações for chamada. Por exemplo, suponha que um aplicativo vincule as colunas em um conjunto de resultados e chame **SQLFetch**. O driver retorna os dados nos buffers associados. Agora suponha que o aplicativo vincule as colunas a um conjunto diferente de buffers. O driver não coloca os dados da linha recém buscada nos buffers vinculados recentemente. Em vez disso, ele aguarda até que **SQLFetch** seja chamado novamente e, em seguida, coloca os dados para a próxima linha nos buffers vinculados recentemente.  
  
> [!NOTE]  
>  O atributo de instrução SQL_ATTR_USE_BOOKMARKS sempre deve ser definido antes de associar uma coluna à coluna 0. Isso não é necessário, mas é altamente recomendável.  
  
## <a name="binding-columns"></a>Colunas de associação  
 Para associar uma coluna, um aplicativo chama **SQLBindCol** e passa o número da coluna, o tipo, o endereço e o comprimento de um buffer de dados e o endereço de um buffer de comprimento/indicador. Para obter informações sobre como esses endereços são usados, consulte "endereços de buffer", mais adiante nesta seção. Para obter mais informações sobre as colunas de associação, consulte [usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 O uso desses buffers é adiado; ou seja, o aplicativo os associa em **SQLBindCol** , mas o driver o acessa de outras funções, ou seja, **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos**. É responsabilidade do aplicativo certificar-se de que os ponteiros especificados em **SQLBindCol** permaneçam válidos, desde que a associação permaneça em vigor. Se o aplicativo permitir que esses ponteiros se tornem inválidos – por exemplo, ele libera um buffer e, em seguida, chama uma função que espera que eles sejam válidos, as consequências são indefinidas. Para obter mais informações, consulte [buffers adiados](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 A associação permanece em vigor até ser substituída por uma nova associação, a coluna é desassociada ou a instrução é liberada.  
  
## <a name="unbinding-columns"></a>Desassociando colunas  
 Para desassociar uma única coluna, um aplicativo chama **SQLBindCol** com *ColumnNumber* definido como o número dessa coluna e *TargetValuePtr* definido como um ponteiro nulo. Se *ColumnNumber* se referir a uma coluna desassociada, o **SQLBindCol** ainda retornará SQL_SUCCESS.  
  
 Para desassociar todas as colunas, um aplicativo chama **SQLFreeStmt** com *fOption* definido como SQL_UNBIND. Isso também pode ser feito definindo o campo SQL_DESC_COUNT do ARD como zero.  
  
## <a name="rebinding-columns"></a>Reassociando colunas  
 Um aplicativo pode executar uma das duas operações para alterar uma associação:  
  
-   Chame **SQLBindCol** para especificar uma nova associação para uma coluna que já está associada. O driver substitui a associação antiga por uma nova.  
  
-   Especifique um deslocamento a ser adicionado ao endereço de buffer que foi especificado pela chamada de associação para **SQLBindCol**. Para obter mais informações, consulte a próxima seção, "deslocamentos de ligação".  
  
## <a name="binding-offsets"></a>Deslocamentos de associação  
 Um deslocamento de associação é um valor que é adicionado aos endereços dos buffers de dados e de comprimento/indicador (conforme especificado no argumento *TargetValuePtr* e *StrLen_or_IndPtr* ) antes que eles sejam desreferenciados. Quando os deslocamentos são usados, as associações são um "modelo" de como os buffers do aplicativo são dispostos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória alterando o deslocamento. Como o mesmo deslocamento é adicionado a cada endereço em cada associação, os deslocamentos relativos entre os buffers para colunas diferentes devem ser os mesmos em cada conjunto de buffers. Isso é sempre verdadeiro quando a associação de linha é usada; o aplicativo deve definir cuidadosamente seus buffers para que isso seja verdadeiro quando a associação de coluna for usada.  
  
 Usar um deslocamento de associação basicamente tem o mesmo efeito que reassociar uma coluna chamando **SQLBindCol**. A diferença é que uma nova chamada para **SQLBindCol** especifica novos endereços para o buffer de dados e o buffer de comprimento/indicador, enquanto o uso de um deslocamento de associação não altera os endereços, mas apenas adiciona um deslocamento a eles. O aplicativo pode especificar um novo deslocamento sempre que desejar, e esse deslocamento é sempre adicionado aos endereços associados originalmente. Em particular, se o deslocamento for definido como 0 ou se o atributo de instrução for definido como um ponteiro nulo, o driver usará os endereços associados originalmente.  
  
 Para especificar um deslocamento de associação, o aplicativo define o atributo SQL_ATTR_ROW_BIND_OFFSET_PTR instrução como o endereço de um buffer sqlinteiro. Antes que o aplicativo chame uma função que usa associações, ele coloca um deslocamento em bytes nesse buffer. Para determinar o endereço do buffer a ser usado, o driver adiciona o deslocamento ao endereço na associação. A soma do endereço e o deslocamento devem ser um endereço válido, mas o endereço para o qual o deslocamento é adicionado não precisa ser válido. Para obter mais informações sobre como os deslocamentos de associação são usados, consulte "endereços de buffer", mais adiante nesta seção.  
  
## <a name="binding-arrays"></a>Matrizes de associação  
 Se o tamanho do conjunto de linhas (o valor do atributo SQL_ATTR_ROW_ARRAY_SIZE Statement) for maior que 1, o aplicativo associará matrizes de buffers em vez de buffers únicos. Para obter mais informações, consulte [Bloquear cursores](../../../odbc/reference/develop-app/block-cursors.md).  
  
 O aplicativo pode associar matrizes de duas maneiras:  
  
-   Associar uma matriz a cada coluna. Isso é conhecido como *associação por coluna* , pois cada estrutura de dados (matriz) contém dados para uma única coluna.  
  
-   Defina uma estrutura para manter os dados de uma linha inteira e associar uma matriz dessas estruturas. Isso é conhecido como *Associação de linha* , pois cada estrutura de dados contém os dados de uma única linha.  
  
 Cada matriz de buffers deve ter, pelo menos, tantos elementos quanto o tamanho do conjunto de linhas.  
  
> [!NOTE]  
>  Um aplicativo deve verificar se o alinhamento é válido. Para obter mais informações sobre considerações de alinhamento, consulte [Alignment](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>Associação de coluna  
 Na associação de coluna, o aplicativo associa dados separados e matrizes de comprimento/indicador a cada coluna.  
  
 Para usar a associação de coluna, o aplicativo primeiro define o atributo de instrução SQL_ATTR_ROW_BIND_TYPE como SQL_BIND_BY_COLUMN. (Esse é o padrão.) Para cada coluna a ser associada, o aplicativo executa as seguintes etapas:  
  
1.  Aloca uma matriz de buffer de dados.  
  
2.  Aloca uma matriz de buffers de comprimento/indicador.  
  
    > [!NOTE]  
    >  Se o aplicativo gravar diretamente nos descritores quando a associação de coluna for usada, matrizes separadas poderão ser usadas para dados de comprimento e indicador.  
  
3.  Chama **SQLBindCol** com os seguintes argumentos:  
  
    -   *TargetType* é o tipo de um único elemento na matriz de buffer de dados.  
  
    -   *TargetValuePtr* é o endereço da matriz de buffer de dados.  
  
    -   *BufferLength* é o tamanho de um único elemento na matriz de buffer de dados. O argumento *BufferLength* é ignorado quando os dados são de comprimento fixo.  
  
    -   *StrLen_or_IndPtr* é o endereço da matriz de comprimento/indicador.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "endereços de buffer", mais adiante nesta seção. Para obter mais informações sobre associação de coluna, consulte [Associação de coluna](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>Associação de linha  
 Na associação de linha, o aplicativo define uma estrutura que contém os buffers de dados e de comprimento/indicador para cada coluna a ser associada.  
  
 Para usar a associação de linha, o aplicativo executa as seguintes etapas:  
  
1.  Define uma estrutura para manter uma única linha de dados (incluindo buffers de dados e de comprimento/indicador) e aloca uma matriz dessas estruturas.  
  
    > [!NOTE]  
    >  Se o aplicativo gravar diretamente nos descritores quando a associação de linha for usada, campos separados poderão ser usados para dados de comprimento e indicador.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_BIND_TYPE como o tamanho da estrutura que contém uma única linha de dados ou para o tamanho de uma instância de um buffer no qual as colunas de resultados serão associadas. O comprimento deve incluir o espaço para todas as colunas associadas e qualquer preenchimento da estrutura ou do buffer, para garantir que, quando o endereço de uma coluna associada for incrementado com o comprimento especificado, o resultado aponte para o início da mesma coluna na próxima linha. Ao usar o operador *sizeof* no ANSI C, esse comportamento é garantido.  
  
3.  Chama **SQLBindCol** com os seguintes argumentos para cada coluna a ser associada:  
  
    -   *TargetType* é o tipo do membro de buffer de dados a ser associado à coluna.  
  
    -   *TargetValuePtr* é o endereço do membro do buffer de dados no primeiro elemento da matriz.  
  
    -   *BufferLength* é o tamanho do membro do buffer de dados.  
  
    -   *StrLen_or_IndPtr* é o endereço do membro de comprimento/indicador a ser associado.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "endereços de buffer", mais adiante nesta seção. Para obter mais informações sobre associação de coluna, consulte [Associação de linha](../../../odbc/reference/develop-app/row-wise-binding.md).  
  
## <a name="buffer-addresses"></a>Endereços de buffer  
 O *endereço de buffer* é o endereço real do buffer de dados ou de comprimento/indicador. O driver calcula o endereço de buffer logo antes de gravar nos buffers (como durante o tempo de busca). Ele é calculado a partir da fórmula a seguir, que usa os endereços especificados nos argumentos *TargetValuePtr* e *StrLen_or_IndPtr* , o deslocamento de associação e o número da linha:  
  
 *Endereço associado* + *deslocamento de associação* + ((*número da linha* -1) x tamanho do *elemento*)  
  
 onde as variáveis da fórmula são definidas conforme descrito na tabela a seguir.  
  
|Variável|Descrição|  
|--------------|-----------------|  
|*Endereço associado*|Para buffers de dados, o endereço especificado com o argumento *TargetValuePtr* em **SQLBindCol**.<br /><br /> Para buffers de comprimento/indicador, o endereço especificado com o argumento *StrLen_or_IndPtr* em **SQLBindCol**. Para obter mais informações, consulte "Comentários adicionais" na seção "descritores e SQLBindCol".<br /><br /> Se o endereço associado for 0, nenhum valor de dados será retornado, mesmo que o endereço conforme calculado pela fórmula anterior seja diferente de zero.|  
|*Deslocamento de associação*|Se a associação de linha for usada, o valor armazenado no endereço especificado com o atributo instrução SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Se a associação por coluna for usada ou se o valor do atributo de instrução de SQL_ATTR_ROW_BIND_OFFSET_PTR for um ponteiro nulo, o *deslocamento de associação* será 0.|  
|*Número da linha*|O número de base 1 da linha no conjunto de linhas. Para buscas de linha única, que são o padrão, isso é 1.|  
|*Tamanho do elemento*|O tamanho de um elemento na matriz associada.<br /><br /> Se a associação por coluna for usada, isso será **sizeof (SQLINTEGER)** para buffers de comprimento/indicador. Para buffers de dados, é o valor do argumento *BufferLength* em **SQLBindCol** se o tipo de dados for de comprimento variável e o tamanho do tipo de dados se o tipo de dados for de comprimento fixo.<br /><br /> Se a associação de linha for usada, esse é o valor do atributo de instrução SQL_ATTR_ROW_BIND_TYPE para os buffers de dados e de comprimento/indicador.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descritores e SQLBindCol  
 As seções a seguir descrevem como o **SQLBindCol** interage com os descritores.  
  
> [!CAUTION]  
>  Chamar **SQLBindCol** para uma instrução pode afetar outras instruções. Isso ocorre quando o ARD associado à instrução é explicitamente alocado e também está associado a outras instruções. Como **SQLBindCol** modifica o descritor, as modificações se aplicam a todas as instruções com as quais este descritor está associado. Se esse não for o comportamento necessário, o aplicativo deverá dissociar esse descritor das outras instruções antes de chamar **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Mapeamentos de argumento  
 Conceitualmente, o **SQLBindCol** executa as seguintes etapas em sequência:  
  
1.  Chama **SQLGetStmtAttr** para obter o identificador ARD.  
  
2.  Chama **SQLGetDescField** para obter o campo SQL_DESC_COUNT do descritor e, se o valor no argumento *ColumnNumber* exceder o valor de SQL_DESC_COUNT, o chamará **SQLSetDescField** para aumentar o valor de SQL_DESC_COUNT para *ColumnNumber*.  
  
3.  Chama **SQLSetDescField** várias vezes para atribuir valores aos seguintes campos do ARD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE ao valor de *TargetType*, exceto que, se *TargetType* for um dos identificadores concisos de um subtipo DateTime ou Interval, ele definirá SQL_DESC_TYPE como SQL_DATETIME ou SQL_INTERVAL, respectivamente; define SQL_DESC_CONCISE_TYPE para o identificador conciso; e define SQL_DESC_DATETIME_INTERVAL_CODE para o subcódigo datetime ou interval correspondente.  
  
    -   Define um ou mais SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_DATETIME_INTERVAL_PRECISION, conforme apropriado para *TargetType*.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH como o valor de *BufferLength*.  
  
    -   Define o campo SQL_DESC_DATA_PTR como o valor de *TargetValue*.  
  
    -   Define o campo SQL_DESC_INDICATOR_PTR como o valor de *StrLen_or_Ind*. (Consulte o parágrafo a seguir.)  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH_PTR como o valor de *StrLen_or_Ind*. (Consulte o parágrafo a seguir.)  
  
 A variável à qual o argumento *StrLen_or_Ind* se refere é usada para informações de indicador e comprimento. Se uma busca encontrar um valor nulo para a coluna, ela armazenará SQL_NULL_DATA nessa variável; caso contrário, ele armazena o comprimento dos dados nessa variável. Passar um ponteiro nulo como *StrLen_or_Ind* mantém a operação de busca retornar o comprimento dos dados, mas fará com que a busca falhe se encontrar um valor nulo e não tiver como retornar SQL_NULL_DATA.  
  
 Se a chamada para **SQLBindCol** falhar, o conteúdo dos campos de descritor que ele teria definido em ARD não será definido e o valor do campo SQL_DESC_COUNT de ARD será inalterado.  
  
## <a name="implicit-resetting-of-count-field"></a>Redefinição implícita de campo de contagem  
 **SQLBindCol** define SQL_DESC_COUNT como o valor do argumento *ColumnNumber* somente quando isso aumentaria o valor de SQL_DESC_COUNT. Se o valor no argumento *TargetValuePtr* for um ponteiro NULL e o valor no argumento *ColumnNumber* for igual a SQL_DESC_COUNT (ou seja, ao desassociar a coluna de limite mais alta), SQL_DESC_COUNT será definido como o número da coluna associada restante mais alta.  
  
## <a name="cautions-regarding-sql_default"></a>Precauções sobre SQL_DEFAULT  
 Para recuperar dados de coluna com êxito, o aplicativo deve determinar corretamente o comprimento e o ponto de partida dos dados no buffer de aplicativo. Quando o aplicativo especifica um *TargetType*explícito, as concepções informativas do aplicativo são facilmente detectadas. No entanto, quando o aplicativo especifica um *TargetType* de SQL_DEFAULT, **SQLBindCol** pode ser aplicado a uma coluna de um tipo de dados diferente daquele destinado pelo aplicativo, seja de alterações nos metadados ou aplicando o código a uma coluna diferente. Nesse caso, o aplicativo nem sempre pode determinar o início ou o comprimento dos dados de coluna buscados. Isso pode levar a erros de dados não relatados ou violações de memória.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa uma instrução **Select** na tabela Customers para retornar um conjunto de resultados das IDs de cliente, nomes e números de telefone, classificados por nome. Em seguida, ele chama **SQLBindCol** para associar as colunas de dados aos buffers locais. Por fim, o aplicativo busca cada linha de dados com **SQLFetch** e imprime o nome, a ID e o número de telefone de cada cliente.  
  
 Para obter mais exemplos de código, consulte função [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)e [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Consulte também o [exemplo de programa ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Buscando um bloco de dados ou rolando por meio de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Liberando buffers de coluna na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Buscando parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornando o número de colunas do conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Consulte também  
   de [referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)  
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
