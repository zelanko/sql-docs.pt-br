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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90bb1c1aa4dbfa2614f689faa47eb0c41a6cecd6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298736"
---
# <a name="sqlbindcol-function"></a>Função SQLBindCol
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLBindCol** vincula os buffers de dados do aplicativo a colunas no conjunto de resultados.  
  
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
 [Entrada] Alça de declaração.  
  
 *ColumnNumber*  
 [Entrada] Número da coluna definida de resultado para vincular. As colunas são numeradas em ordem de coluna crescente a partir de 0, onde a coluna 0 é a coluna marcadores. Se os marcadores não forem usados - ou seja, o atributo de declaração SQL_ATTR_USE_BOOKMARKS é definido como SQL_UB_OFF - os números da coluna começam em 1.  
  
 *Targettype*  
 [Entrada] O identificador do tipo de \*dados C do buffer *TargetValuePtr.* Quando está recuperando dados da fonte de dados com **SQLFetch,** **SQLFetchScroll,** **SQLBulkOperations**ou **SQLSetPos,** o driver converte os dados para esse tipo; quando envia dados para a fonte de dados com **SQLBulkOperations** ou **SQLSetPos,** o driver converte os dados desse tipo. Para obter uma lista de tipos de dados c válidos e identificadores de tipo, consulte a seção [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) no apêndice D: Tipos de dados.  
  
 Se o argumento *TargetType* for um tipo de dados de intervalo, a precisão de liderança do intervalo padrão (2) e a precisão dos segundos de intervalo padrão (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION do ARD, respectivamente, são usados para os dados. Se o argumento *TargetType* for SQL_C_NUMERIC, a precisão padrão (definida pelo driver) e a escala padrão (0), definidanos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, serão usadas para os dados. Se qualquer precisão ou escala padrão não for apropriada, o aplicativo deve definir explicitamente o campo descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Você também pode especificar um tipo de dados C estendido. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Entrada/saída diferida] Ponteiro para o buffer de dados para vincular à coluna. Dados de retorno **SQLFetch** e **SQLFetchScroll** neste buffer. **A SQLBulkOperations** retorna dados neste buffer quando *a operação* é SQL_FETCH_BY_BOOKMARK; ele recupera dados deste buffer quando *a operação* é SQL_ADD ou SQL_UPDATE_BY_BOOKMARK. **SQLSetPos** retorna dados neste buffer quando *a operação* é SQL_REFRESH; ele recupera dados deste buffer quando *a operação* é SQL_UPDATE.  
  
 Se *TargetValuePtr* for um ponteiro nulo, o driver desvinculará o buffer de dados da coluna. Um aplicativo pode desvincular todas as colunas ligando para **SQLFreeStmt** com a opção SQL_UNBIND. Um aplicativo pode desvincular o buffer de dados de uma coluna, mas ainda ter um buffer de comprimento/indicador vinculado à coluna, se o argumento *TargetValuePtr* na chamada para **SQLBindCol** for um ponteiro nulo, mas o argumento *StrLen_or_IndPtr* é um valor válido.  
  
 *BufferLength*  
 [Entrada] Comprimento do \* *buffer TargetValuePtr* em bytes.  
  
 O driver usa *BufferLength* para evitar \*escrever após o fim do buffer *TargetValuePtr* quando ele retorna dados de comprimento variável, como dados de caracteres ou binários. Observe que o driver conta o caractere de \*rescisão nula quando retorna os dados de caracteres ao *TargetValuePtr*. \**O TargetValuePtr* deve, portanto, conter espaço para o caractere de rescisão nula ou o driver truncará os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um inteiro ou uma estrutura de data, o driver ignora *bufferLength* e assume que o buffer é grande o suficiente para conter os dados. Portanto, é importante que o aplicativo aloque um buffer grande o suficiente para dados de comprimento fixo ou o driver escreverá após o fim do buffer.  
  
 **SQLBindCol** retorna SQLSTATE HY090 (string inválida ou comprimento de buffer) quando *BufferLength* é menor que 0, mas não quando *BufferLength* é 0. No entanto, se *o TargetType* especificar um tipo de caractere, um aplicativo não deve definir *BufferLength* para 0, porque os drivers compatíveis com ISO CLI retornam SQLSTATE HY090 (comprimento inválido ou buffer) nesse caso.  
  
 *Strlen_or_indptr*  
 [Entrada/saída diferida] Ponteiro para o buffer de comprimento/indicador para se ligar à coluna. **SQLFetch** e **SQLFetchScroll** retornam um valor neste buffer. **A SQLBulkOperations** recupera um valor deste buffer quando *a Operação* é SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** retorna um valor neste buffer quando *a operação* é SQL_FETCH_BY_BOOKMARK. **SQLSetPos** retorna um valor neste buffer quando *a operação* é SQL_REFRESH; ele recupera um valor deste buffer quando *a operação* é SQL_UPDATE.  
  
 **SQLFetch,** **SQLFetchScroll,** **SQLBulkOperations**e **SQLSetPos** podem retornar os seguintes valores no buffer de comprimento/indicador:  
  
-   A duração dos dados disponíveis para retornar  
  
-   SQL_NO_TOTAL  
  
-   Sql_null_data  
  
 O aplicativo pode colocar os seguintes valores no buffer de comprimento/indicador para uso com **SQLBulkOperations** ou **SQLSetPos:**  
  
-   A duração dos dados que estão sendo enviados  
  
-   SQL_NTS  
  
-   Sql_null_data  
  
-   SQL_DATA_AT_EXEC  
  
-   O resultado da macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Se o buffer indicador e o buffer de comprimento forem buffers separados, o buffer indicador pode retornar apenas SQL_NULL_DATA, enquanto o buffer de comprimento pode retornar todos os outros valores.  
  
 Para obter mais informações, consulte [SQLBulkOperations Function](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLFetch Function,](../../../odbc/reference/syntax/sqlfetch-function.md) [SQLSetPos Function](../../../odbc/reference/syntax/sqlsetpos-function.md)e [Using Length/Indicator Values](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Se *StrLen_or_IndPtr* for um ponteiro nulo, nenhum comprimento ou valor do indicador será usado. Este é um erro ao buscar dados e os dados são NULAS.  
  
 Consulte [As informações de 64 bits do ODBC,](../../../odbc/reference/odbc-64-bit-information.md)se o aplicativo for executado em um sistema operacional de 64 bits.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLBindCol** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de *statementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBindCol** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|(DM) O argumento *ColunaNúmero* era 0, e o argumento *TargetType* não era SQL_C_BOOKMARK ou SQL_C_VARBOOKMARK.|  
|07009|Índice de descritor inválido|O valor especificado para o argumento *ColunaNúmero* excedeu o número máximo de colunas no conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \** buffer MessageText descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar memória necessária para suportar a execução ou a conclusão da função.|  
|HY003|Tipo de buffer de aplicativo inválido|O argumento *TargetType* não era nem um tipo de dados válido nem SQL_C_DEFAULT.|  
|HY010|Erro de seqüência de função|(DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando **SQLBindCol** foi chamado.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** foram chamados para o *StatementHandle* e retornaram SQL_PARAM_DATA_AVAILABLE. Esta função foi chamada antes de os dados serem recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para o argumento *BufferLength* foi inferior a 0.<br /><br /> (DM) O motorista era um ODBC 2. *x* driver, o argumento *ColunaNúmero* foi definido como 0, e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suporta a conversão especificada pela combinação do argumento *TargetType* e do tipo de dados SQL específico do driver da coluna correspondente.<br /><br /> O argumento *ColumnNumber* era 0 e o driver não suporta marcadores.<br /><br /> O driver suporta apenas ODBC 2. *x* e o argumento *TargetType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados do intervalo C listados em [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) no apêndice D: Tipos de dados.<br /><br /> O driver só suporta versões ODBC antes do 3.50, e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver associado ao *StatementHandle* não suporta a função.|  
  
## <a name="comments"></a>Comentários  
 **O SQLBindCol** é usado para associar ou *vincular* colunas no conjunto de resultados a buffers de dados e buffers de comprimento/indicador no aplicativo. Quando o aplicativo chama **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos** para buscar dados, o driver retorna os dados para as colunas vinculadas nos buffers especificados; para obter mais informações, consulte [SQLFetch Function](../../../odbc/reference/syntax/sqlfetch-function.md). Quando o aplicativo chama **o SQLBulkOperations** para atualizar ou inserir uma linha ou **SQLSetPos** para atualizar uma linha, o driver recupera os dados das colunas vinculadas dos buffers especificados; para obter mais informações, consulte [SQLBulkOperations Function](../../../odbc/reference/syntax/sqlbulkoperations-function.md) ou [SQLSetPos Function](../../../odbc/reference/syntax/sqlsetpos-function.md). Para obter mais informações sobre vinculação, consulte [Resultados de recuperação (Básico)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Observe que as colunas não são obrigadas a recuperar dados deles. Um aplicativo também pode chamar **SQLGetData** para recuperar dados de colunas. Embora seja possível vincular algumas colunas seguidas e chamar **SQLGetData** para outras, isso está sujeito a algumas restrições. Para obter mais informações, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Colunas de vinculação, desvinculação e revinculação  
 Uma coluna pode ser vinculada, desvinculada ou rebote a qualquer momento, mesmo depois de os dados serem obtidos a partir do conjunto de resultados. A nova ligação entra em vigor na próxima vez que uma função que usa vinculações é chamada. Por exemplo, suponha que um aplicativo vincule as colunas em um conjunto de resultados e chame **SQLFetch**. O driver retorna os dados nos buffers vinculados. Agora suponha que o aplicativo vincule as colunas a um conjunto diferente de buffers. O driver não coloca os dados para a linha recém-buscada nos buffers recém-vinculados. Em vez disso, ele espera até **que o SQLFetch** seja chamado novamente e, em seguida, coloca os dados para a próxima linha nos buffers recém-vinculados.  
  
> [!NOTE]  
>  O atributo de declaração SQL_ATTR_USE_BOOKMARKS deve ser sempre definido antes de vincular uma coluna à coluna 0. Isso não é necessário, mas é fortemente recomendado.  
  
## <a name="binding-columns"></a>Colunas de associação  
 Para vincular uma coluna, um aplicativo chama **SQLBindCol** e passa o número da coluna, tipo, endereço e comprimento de um buffer de dados e o endereço de um buffer de comprimento/indicador. Para obter informações sobre como esses endereços são usados, consulte "Buffer Addresses", mais tarde nesta seção. Para obter mais informações sobre colunas de vinculação, consulte [Usando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 O uso desses buffers é adiado; ou seja, o aplicativo os vincula no **SQLBindCol,** mas o driver os acessa de outras funções - ou seja, **SQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos**. É responsabilidade do aplicativo garantir que os ponteiros especificados no **SQLBindCol** permaneçam válidos enquanto a vinculação permanecer em vigor. Se o aplicativo permitir que esses ponteiros se tornem inválidos - por exemplo, ele libera um buffer - e então chama uma função que espera que eles sejam válidos, as consequências são indefinidas. Para obter mais informações, consulte [Buffers diferidos](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 A vinculação permanece em vigor até ser substituída por uma nova vinculação, a coluna está desvinculada ou a declaração é liberada.  
  
## <a name="unbinding-columns"></a>Colunas desvinculação  
 Para desvincular uma única coluna, um aplicativo chama **SQLBindCol** com *ColumnNumber* definido para o número dessa coluna e *TargetValuePtr* definido como um ponteiro nulo. Se *O Número de* Colunas se referir a uma coluna não vinculada, o **SQLBindCol** ainda retorna SQL_SUCCESS.  
  
 Para desvincular todas as colunas, um aplicativo chama **SQLFreeStmt** com *fOption* definido para SQL_UNBIND. Isso também pode ser feito definindo o campo SQL_DESC_COUNT do ARD para zero.  
  
## <a name="rebinding-columns"></a>Colunas de revinculação  
 Um aplicativo pode executar qualquer uma das duas operações para alterar uma vinculação:  
  
-   Ligue para **o SQLBindCol** para especificar uma nova vinculação para uma coluna que já esteja vinculada. O motorista substitui a antiga ligação com a nova.  
  
-   Especifique uma compensação a ser adicionada ao endereço buffer especificado pela chamada vinculante ao **SQLBindCol**. Para obter mais informações, consulte a próxima seção, "Deslocamentos de vinculação".  
  
## <a name="binding-offsets"></a>Deslocamentos de vinculação  
 Uma compensação de vinculação é um valor adicionado aos endereços dos buffers de dados e comprimento/indicador (conforme especificado no argumento *TargetValuePtr* e *StrLen_or_IndPtr)* antes de serem desreferenciados. Quando as compensações são usadas, as vinculações são um "modelo" de como os buffers do aplicativo são definidos, e o aplicativo pode mover esse "modelo" para diferentes áreas de memória alterando o deslocamento. Como o mesmo deslocamento é adicionado a cada endereço em cada vinculação, as compensações relativas entre buffers para colunas diferentes devem ser as mesmas dentro de cada conjunto de buffers. Isso é sempre verdade quando a vinculação em termos de linha é usada; o aplicativo deve cuidadosamente definir seus buffers para que isso seja verdade quando a vinculação em termos de coluna for usada.  
  
 O uso de um deslocamento de vinculação tem basicamente o mesmo efeito que revincular uma coluna chamando **SQLBindCol**. A diferença é que uma nova chamada para **o SQLBindCol** especifica novos endereços para o buffer de dados e buffer de comprimento/indicador, enquanto o uso de uma compensação de vinculação não altera os endereços, mas apenas adiciona uma compensação a eles. O aplicativo pode especificar um novo deslocamento sempre que quiser, e esse deslocamento é sempre adicionado aos endereços originalmente vinculados. Em particular, se o deslocamento estiver definido como 0 ou se o atributo de declaração estiver definido como um ponteiro nulo, o driver usará os endereços originalmente vinculados.  
  
 Para especificar uma compensação de vinculação, o aplicativo define o atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR para o endereço de um buffer SQLINTEGER. Antes que o aplicativo chame uma função que usa vinculações, ele coloca um offset em bytes neste buffer. Para determinar o endereço do buffer a ser usado, o driver adiciona a compensação ao endereço na vinculação. A soma do endereço e da compensação deve ser um endereço válido, mas o endereço ao qual a compensação é adicionada não precisa ser válido. Para obter mais informações sobre como as compensações de vinculação são usadas, consulte "Buffer Addresses", mais tarde nesta seção.  
  
## <a name="binding-arrays"></a>Matrizes de vinculação  
 Se o tamanho do conjunto de linhas (o valor do atributo de declaração SQL_ATTR_ROW_ARRAY_SIZE) for maior que 1, o aplicativo vincula matrizes de buffers em vez de buffers únicos. Para obter mais informações, consulte [Block Cursors](../../../odbc/reference/develop-app/block-cursors.md).  
  
 O aplicativo pode vincular matrizes de duas maneiras:  
  
-   Vincule uma matriz a cada coluna. Isso é referido como *vinculação em termos de coluna* porque cada estrutura de dados (array) contém dados para uma única coluna.  
  
-   Defina uma estrutura para manter os dados por uma linha inteira e vincule uma matriz dessas estruturas. Isso é referido como *vinculação em termos de linha* porque cada estrutura de dados contém os dados de uma única linha.  
  
 Cada matriz de buffers deve ter pelo menos tantos elementos quanto o tamanho do conjunto de linhas.  
  
> [!NOTE]  
>  Um aplicativo deve verificar se o alinhamento é válido. Para obter mais informações sobre considerações de alinhamento, consulte [Alinhamento](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>Associação de coluna  
 Na vinculação em termos de coluna, o aplicativo vincula os conjuntos separados de dados e comprimento/indicador a cada coluna.  
  
 Para usar a vinculação em termos de coluna, o aplicativo define primeiro o atributo de declaração SQL_ATTR_ROW_BIND_TYPE a SQL_BIND_BY_COLUMN. (Este é o padrão.) Para cada coluna ser vinculada, o aplicativo executa as seguintes etapas:  
  
1.  Aloca um array de buffer de dados.  
  
2.  Aloca uma matriz de buffers de comprimento/indicador.  
  
    > [!NOTE]  
    >  Se o aplicativo for escrito diretamente aos descritores quando a vinculação em termos de coluna for usada, matrizes separadas poderão ser usadas para dados de comprimento e indicador.  
  
3.  Chama **sqlbindcol** com os seguintes argumentos:  
  
    -   *TargetType* é o tipo de um único elemento no array de buffer de dados.  
  
    -   *TargetValuePtr* é o endereço do array de buffer de dados.  
  
    -   *BufferLength* é o tamanho de um único elemento no array de buffer de dados. O argumento *BufferLength* é ignorado quando os dados são dados de comprimento fixo.  
  
    -   *StrLen_or_IndPtr* é o endereço da matriz comprimento/indicador.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "Buffer Addresses", mais tarde nesta seção. Para obter mais informações sobre a vinculação em termos de coluna, consulte ['Vinculação em forma de coluna'.](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
## <a name="row-wise-binding"></a>Associação de linha  
 Em vinculação em termos de linha, o aplicativo define uma estrutura que contém buffers de comprimento e comprimento/indicador para cada coluna a ser vinculada.  
  
 Para usar a vinculação em termos de linha, o aplicativo executa as seguintes etapas:  
  
1.  Define uma estrutura para conter uma única linha de dados (incluindo os buffers de dados e comprimento/indicador) e aloca um conjunto dessas estruturas.  
  
    > [!NOTE]  
    >  Se o aplicativo for escrito diretamente aos descritores quando a vinculação em termos de linha for usada, campos separados poderão ser usados para dados de comprimento e indicador.  
  
2.  Define o atributo de declaração SQL_ATTR_ROW_BIND_TYPE ao tamanho da estrutura que contém uma única linha de dados ou ao tamanho de uma instância de um buffer no qual as colunas de resultados serão vinculadas. O comprimento deve incluir espaço para todas as colunas vinculadas, e qualquer preenchimento da estrutura ou tampão, para garantir que quando o endereço de uma coluna vinculada for incrementado com o comprimento especificado, o resultado apontará para o início da mesma coluna na próxima linha. Ao utilizar o *tamanho do* operador no ANSI C, esse comportamento é garantido.  
  
3.  Chama **o SQLBindCol** com os seguintes argumentos para que cada coluna seja vinculada:  
  
    -   *TargetType* é o tipo de membro do buffer de dados a ser vinculado à coluna.  
  
    -   *TargetValuePtr* é o endereço do membro do buffer de dados no primeiro elemento de matriz.  
  
    -   *BufferLength* é o tamanho do membro do buffer de dados.  
  
    -   *StrLen_or_IndPtr* é o endereço do membro de comprimento/indicador a ser vinculado.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "Buffer Addresses", mais tarde nesta seção. Para obter mais informações sobre a vinculação em termos de coluna, consulte ['Vinculação em forma de linha'](../../../odbc/reference/develop-app/row-wise-binding.md)  
  
## <a name="buffer-addresses"></a>Endereços de buffer  
 O *endereço buffer* é o endereço real do buffer de dados ou comprimento/indicador. O driver calcula o endereço buffer pouco antes de ser escrito nos buffers (como durante o tempo de busca). Ele é calculado a partir da seguinte fórmula, que usa os endereços especificados nos argumentos *TargetValuePtr* e *StrLen_or_IndPtr,* a compensação de vinculação e o número da linha:  
  
 *Bound Address* + *Deslocamento de vinculação do* endereço vinculado + ((número*da linha* - 1) x tamanho *do elemento*)  
  
 onde as variáveis da fórmula são definidas conforme descrito na tabela a seguir.  
  
|Variável|Descrição|  
|--------------|-----------------|  
|*Endereço vinculado*|Para buffers de dados, o endereço especificado com o argumento *TargetValuePtr* no **SQLBindCol**.<br /><br /> Para buffers de comprimento/indicador, o endereço especificado com o *argumento StrLen_or_IndPtr* no **SQLBindCol**. Para obter mais informações, consulte "Comentários adicionais" na seção "Descritores e SQLBindCol".<br /><br /> Se o endereço vinculado for 0, nenhum valor de dados é devolvido, mesmo que o endereço calculado pela fórmula anterior não seja zero.|  
|*Deslocamento de vinculação*|Se for usada a vinculação em termos de linha, o valor armazenado no endereço especificado com o atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Se a vinculação em termos de coluna for usada ou se o valor do atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR for um ponteiro nulo, *a Comvidade Vinculante* será 0.|  
|*Row Number*|O número baseado em 1 da linha no conjunto de linhas. Para buscas de linha única, que são o padrão, este é 1.|  
|*Tamanho do elemento*|O tamanho de um elemento na matriz vinculada.<br /><br /> Se a vinculação em termos de coluna for usada, esta será **dimensionada (SQLINTEGER)** para buffers de comprimento/indicador. Para buffers de dados, é o valor do argumento *BufferLength* no **SQLBindCol** se o tipo de dados for comprimento variável e o tamanho do tipo de dados se o tipo de dados for comprimento fixo.<br /><br /> Se a vinculação em termos de linha for usada, este é o valor do atributo de declaração SQL_ATTR_ROW_BIND_TYPE para os buffers de comprimento/indicador de comprimento/comprimento.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descritores e SQLBindCol  
 As seções a seguir descrevem como **o SQLBindCol** interage com descritores.  
  
> [!CAUTION]  
>  Chamar **sqlBindCol** para uma instrução pode afetar outras instruções. Isso ocorre quando o ARD associado à declaração é explicitamente alocado e também está associado a outras declarações. Como **o SQLBindCol** modifica o descritor, as modificações se aplicam a todas as instruções com as quais este descritor está associado. Se este não for o comportamento necessário, o aplicativo deve dissociar este descritor das outras declarações antes de chamar **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Mapeamentos de argumentos  
 Conceitualmente, **o SQLBindCol** executa as seguintes etapas em seqüência:  
  
1.  Chama **sqlGetstmtAttr** para obter a alça ARD.  
  
2.  Chama **sQLGetDescField** para obter o campo SQL_DESC_COUNT deste descritor e se o valor no argumento *ColunaNúmero* exceder o valor de SQL_DESC_COUNT, chama **SQLSetDescField** para aumentar o valor de SQL_DESC_COUNT para *Número de Colunas*.  
  
3.  Chama **SQLSetDescField** várias vezes para atribuir valores aos seguintes campos do ARD:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE ao valor do *TargetType,* exceto que se o *TargetType* for um dos identificadores concisos de um subtipo de data ou intervalo, ele define SQL_DESC_TYPE para SQL_DATETIME ou SQL_INTERVAL, respectivamente; define SQL_DESC_CONCISE_TYPE para o identificador conciso; e define SQL_DESC_DATETIME_INTERVAL_CODE para o subcódigo de data ou intervalo correspondente.  
  
    -   Define um ou mais de SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_DATETIME_INTERVAL_PRECISION, conforme apropriado para *TargetType*.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH para o valor de *BufferLength*.  
  
    -   Define o campo SQL_DESC_DATA_PTR ao valor do *TargetValue*.  
  
    -   Define o campo SQL_DESC_INDICATOR_PTR ao valor de *StrLen_or_Ind*. (Veja o parágrafo a seguir.)  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH_PTR ao valor de *StrLen_or_Ind*. (Veja o parágrafo a seguir.)  
  
 A variável a que o *argumento StrLen_or_Ind* refere é usada tanto para informações de indicadores quanto de comprimento. Se um fetch encontrar um valor nulo para a coluna, ele armazena SQL_NULL_DATA nesta variável; caso contrário, ele armazena o comprimento dos dados nesta variável. Passar um ponteiro nulo como *StrLen_or_Ind* impede que a operação de busca retorne o comprimento dos dados, mas faz com que a busca falhe se encontrar um valor nulo e não tiver como retornar SQL_NULL_DATA.  
  
 Se a chamada para **SQLBindCol** falhar, o conteúdo dos campos de descritor que ele teria definido no ARD é indefinido e o valor do campo SQL_DESC_COUNT do ARD é inalterado.  
  
## <a name="implicit-resetting-of-count-field"></a>Redefinição implícita do campo de contagem  
 **SQLBindCol** define SQL_DESC_COUNT ao valor do argumento *ColunaNúmero* somente quando isso aumentaria o valor de SQL_DESC_COUNT. Se o valor no argumento *TargetValuePtr* for um ponteiro nulo e o valor no argumento *ColunaNúmero* for igual a SQL_DESC_COUNT (isto é, quando desvincular a coluna vinculada mais alta), SQL_DESC_COUNT será definido para o número da coluna vinculada mais alta restante.  
  
## <a name="cautions-regarding-sql_default"></a>Cuidados em relação à SQL_DEFAULT  
 Para recuperar os dados da coluna com sucesso, o aplicativo deve determinar corretamente o comprimento e o ponto de partida dos dados no buffer do aplicativo. Quando o aplicativo especifica um *TargetType*explícito, os equívocos do aplicativo são facilmente detectados. No entanto, quando o aplicativo especifica um *TargetType* de SQL_DEFAULT, **o SQLBindCol** pode ser aplicado a uma coluna de um tipo de dados diferente daquele pretendido pelo aplicativo, seja de alterações nos metadados ou aplicando o código a uma coluna diferente. Neste caso, o aplicativo pode nem sempre determinar o início ou o comprimento dos dados da coluna buscada. Isso pode levar a erros de dados não relatados ou violações de memória.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa uma declaração **SELECT** na tabela Clientes para retornar um conjunto de resultados dos IDs, nomes e números de telefone do cliente, classificados por nome. Em seguida, ele chama **sQLBindCol** para vincular as colunas de dados a buffers locais. Finalmente, o aplicativo busca cada linha de dados com **SQLFetch** e imprime o nome, id e número de telefone de cada cliente.  
  
 Para obter mais exemplos de código, consulte [SQLBulkOperations Function,](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLColumns Function,](../../../odbc/reference/syntax/sqlcolumns-function.md) [SQLFetchScroll Function](../../../odbc/reference/syntax/sqlfetchscroll-function.md)e [SQLSetPos Function](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 60
  
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
                  retcode = SQLBindCol(hstmt, 1, SQL_C_WCHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_WCHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_WCHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (int i=0 ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                     {
                        //replace wprintf with printf
                        //%S with %ls
                        //warning C4477: 'wprintf' : format string '%S' requires an argument of type 'char *'
                        //but variadic argument 2 has type 'SQLWCHAR *'
                        //wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                        printf("%d: %ls %ls %ls\n", i + 1, sCustID, szName, szPhone);  
                    }    
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
  
 Veja também [o Programa Amostra ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Liberando buffers de coluna na declaração|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Buscar parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Retornando o número de colunas de conjunto de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
