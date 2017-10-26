---
title: "Função SQLBindCol | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 641b08ab3d3aec59f66dd0405770cf19d4690769
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindcol-function"></a>Função SQLBindCol
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 1.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLBindCol** associa buffers de dados de aplicativo para as colunas no conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Identificador de instrução.  
  
 *ColumnNumber*  
 [Entrada] Número do resultado definido coluna para associar. As colunas são numeradas em ordem crescente de coluna começando em 0, onde a coluna 0 é a coluna de indicador. Se não forem usados indicadores — ou seja, o atributo de instrução de SQL_ATTR_USE_BOOKMARKS é definido como SQL_UB_OFF —, em seguida, a coluna de números começam em 1.  
  
 *TargetType*  
 [Entrada] O identificador do tipo de dados C a \* *TargetValuePtr* buffer. Quando está recuperando dados da fonte de dados com **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, ou **SQLSetPos**, o driver converte os dados para este tipo; Quando ele envia dados para a fonte de dados com **SQLBulkOperations** ou **SQLSetPos**, o driver converte os dados desse tipo. Para obter uma lista de tipos de dados válidos do C e identificadores de tipo, consulte o [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) seção apêndice d: os tipos de dados.  
  
 Se o *TargetType* argumento for um tipo de dados de intervalo, a precisão de à esquerda do intervalo de padrão (2) e a precisão de segundos de intervalo padrão (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION do Descartar, respectivamente, são usadas para os dados. Se o *TargetType* argumento é SQL_C_NUMERIC, a precisão padrão (definido pelo driver) e padrão de escala (0), conforme definido nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE a descartar, é usado para os dados. Se qualquer escala ou precisão padrão não for apropriada, o aplicativo deve definir explicitamente o campo do descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
 Você também pode especificar um tipo de dados estendido C. Para obter mais informações, consulte [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Entrada/saída adiada] Ponteiro para o buffer de dados para associar à coluna. **SQLFetch** e **SQLFetchScroll** retornar dados nesse buffer. **SQLBulkOperations** retorna dados nesse buffer quando *operação* é SQL_FETCH_BY_BOOKMARK; recupera dados desse buffer quando *operação* é SQL_ADD ou SQL_UPDATE_BY_BOOKMARK . **SQLSetPos** retorna dados nesse buffer quando *operação* é SQL_REFRESH; recupera dados desse buffer quando *operação* é SQL_UPDATE.  
  
 Se *TargetValuePtr* é um ponteiro nulo, o driver desassocia o buffer de dados para a coluna. Um aplicativo pode desassociar todas as colunas chamando **SQLFreeStmt** com a opção SQL_UNBIND. Um aplicativo pode desassociar o buffer de dados para uma coluna, mas ainda tem um buffer de comprimento/indicador associado para a coluna, se o *TargetValuePtr* argumentos na chamada para **SQLBindCol** é um ponteiro nulo, mas o *StrLen_or_IndPtr* argumento é um valor válido.  
  
 *BufferLength*  
 [Entrada] Comprimento do **TargetValuePtr* buffer em bytes.  
  
 O driver usa *BufferLength* para evitar a gravação após o término do \* *TargetValuePtr* buffer ao retorna os dados de comprimento variável, como caractere ou dados binários. Observe que o driver contará o caractere null de terminação quando ele retorna dados de caractere para \* *TargetValuePtr*. **TargetValuePtr* , portanto, deve conter um espaço para o caractere null de terminação ou o driver truncará os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um número inteiro ou uma estrutura de data, o driver ignorará *BufferLength* e pressupõe que o buffer é grande o suficiente para manter os dados. Portanto, é importante para o aplicativo para alocar um buffer grande o suficiente para dados de comprimento fixo ou o driver irá gravar após o final do buffer.  
  
 **SQLBindCol** retornará SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres) quando *BufferLength* é menor que 0 mas não quando *BufferLength* é 0. No entanto, se *TargetType* Especifica um tipo de caractere, um aplicativo não deve definir *BufferLength* como 0, porque os drivers compatíveis com ISO CLI retornam SQLSTATE HY090 (comprimento inválido de buffer ou cadeia de caracteres) em que caso.  
  
 *StrLen_or_IndPtr*  
 [Entrada/saída adiada] Ponteiro para o buffer de comprimento/indicador para associar à coluna. **SQLFetch** e **SQLFetchScroll** retorna um valor nesse buffer. **SQLBulkOperations** recupera o valor deste buffer quando *operação* é SQL_ADD, SQL_UPDATE_BY_BOOKMARK ou SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** retorna um valor nesse buffer quando *operação* é SQL_FETCH_BY_BOOKMARK. **SQLSetPos** retorna um valor nesse buffer quando *operação* é SQL_REFRESH; ela recupera um valor desse buffer quando *operação* é SQL_UPDATE.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, e **SQLSetPos** pode retornar os seguintes valores no buffer de comprimento/indicador:  
  
-   O comprimento dos dados disponíveis para retornar  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 O aplicativo pode colocar os valores a seguir no buffer de comprimento/indicador para uso com **SQLBulkOperations** ou **SQLSetPos**:  
  
-   O comprimento dos dados que estão sendo enviados  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   O resultado da macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Se o buffer de indicador e o buffer de comprimento são separadas de buffers, o buffer de indicador pode retornar apenas SQL_NULL_DATA, enquanto o buffer de comprimento pode retornar todos os outros valores.  
  
 Para obter mais informações, consulte [SQLBulkOperations função](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md), [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md), e [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Se *StrLen_or_IndPtr* é um valor nulo de ponteiro, nenhum comprimento ou indicador é usado. Este é um erro ao buscar dados e os dados é NULL.  
  
 Consulte [informações de ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), se o aplicativo será executado em um sistema operacional de 64 bits.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Quando **SQLBindCol** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtida chamando **SQLGetDiagRec** com um *HandleType* de SQL _ HANDLE_STMT e um *tratar* de *StatementHandle*. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLBindCol** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições de SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado a cada valor SQLSTATE é SQL_ERROR, a menos que indicado em contrário.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem de informação específica do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|(DM) a *ColumnNumber* argumento era 0 e o *TargetType* argumento não era SQL_C_BOOKMARK ou SQL_C_VARBOOKMARK.|  
|07009|Índice do descritor inválido|O valor especificado para o argumento *ColumnNumber* excedeu o número máximo de colunas no conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhuma SQLSTATE específico e para o qual nenhuma SQLSTATE específicos de implementação foi definida. A mensagem de erro retornada pelo **SQLGetDiagRec** no * \*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte a execução ou a conclusão da função.|  
|HY003|Tipo de buffer de aplicativo inválido|O argumento *TargetType* não era um tipo de dados válido nem SQL_C_DEFAULT.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando **SQLBindCol** foi chamado.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de recuperação para todos os parâmetros de fluxo de dados.<br /><br /> (DM) uma função de execução assíncrona foi chamada para o *StatementHandle* e ainda estava em execução quando esta função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o * StatementHandle* e retorna SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todas as colunas ou parâmetros de dados em execução.|  
|HY013|Erro de gerenciamento de memória|Não foi possível processar a chamada de função porque os objetos de memória subjacente não podem ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|(DM) o valor especificado para o argumento *BufferLength* era menor do que 0.<br /><br /> (DM) o driver foi um ODBC 2. *x* driver, o *ColumnNumber* argumento foi definido como 0 e o valor especificado para o argumento *BufferLength* não era igual a 4.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecido. Somente Desconecte e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não suporta a conversão especificada pela combinação da *TargetType* argumento e o tipo de dados específica do driver SQL da coluna correspondente.<br /><br /> O argumento *ColumnNumber* 0 e o driver não oferece suporte a indicadores.<br /><br /> O driver suporta apenas o ODBC 2. *x* e o argumento *TargetType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados de intervalo C listados na [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice d: os tipos de dados.<br /><br /> O driver só dá suporte a versões ODBC anteriores 3.50 e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo limite de Conexão expirou|O período de tempo limite de conexão expirou antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não dá suporte a esta função|O driver em (DM) associado a *StatementHandle* não oferece suporte para a função.|  
  
## <a name="comments"></a>Comentários  
 **SQLBindCol** é usada para associar, ou *associar,* colunas no resultado definido como buffers de dados e buffers de comprimento/indicador no aplicativo. Quando o aplicativo chama **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos** para buscar dados, o driver retorna os dados para as colunas associadas nos buffers especificados; para obter mais informações, consulte [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md). Quando o aplicativo chama **SQLBulkOperations** para atualizar ou inserir uma linha ou **SQLSetPos** para atualizar uma linha, o driver recupera os dados para as colunas associadas dos buffers de especificado; para obter mais informações , consulte [SQLBulkOperations função](../../../odbc/reference/syntax/sqlbulkoperations-function.md) ou [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md). Para obter mais informações sobre associação, consulte [recuperar resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Observe que colunas não precisa ser associado ao recuperar dados a partir deles. Um aplicativo também pode chamar **SQLGetData** para recuperar dados de colunas. Embora seja possível associar algumas colunas em uma linha e a chamada **SQLGetData** para outras pessoas, isso está sujeito a algumas restrições. Para obter mais informações, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Colunas de associação, desassociando e religação  
 Uma coluna pode ser vinculada, não associada ou reassociada a qualquer momento, mesmo depois que dados tiverem sido buscados do conjunto de resultados. A nova associação entra em vigor na próxima vez que uma função que usa associações é chamada. Por exemplo, suponha que um aplicativo associa as colunas em um conjunto de resultados e chama **SQLFetch**. O driver retorna os dados nos buffers associados. Agora suponha que o aplicativo associa as colunas para um conjunto diferente de buffers. O driver não coloca os dados para a linha buscada apenas nos buffers recém-associado. Em vez disso, ele aguarda até **SQLFetch** é chamado novamente e, em seguida, coloca os dados para a próxima linha em buffers recém-associado.  
  
> [!NOTE]  
>  O atributo de instrução SQL_ATTR_USE_BOOKMARKS deve sempre ser definido antes de associar uma coluna a coluna 0. Isso não é necessário, mas é altamente recomendável.  
  
## <a name="binding-columns"></a>Colunas de associação  
 Para associar uma coluna, um aplicativo chama **SQLBindCol** e passa o número da coluna, tipo, endereço e tamanho de um buffer de dados e o endereço de um buffer de comprimento/indicador. Para obter informações sobre como esses endereços são usados, consulte "Endereços de Buffer", posteriormente nesta seção. Para obter mais informações sobre colunas de associação, consulte [SQLBindCol usando](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 O uso desses buffers é adiado; ou seja, o aplicativo associa-os em **SQLBindCol** , mas o driver acessa-los de outras funções — ou seja, **SQLBulkOperations**, **SQLFetch**, ** SQLFetchScroll**, ou **SQLSetPos**. É responsabilidade do aplicativo para certificar-se de que os ponteiros especificado em **SQLBindCol** permanecerá válido, desde que a associação permanece em vigor. Se o aplicativo permite que esses ponteiros se tornar inválido — por exemplo, ela libera um buffer — e, em seguida, chama uma função que espera para ser válida, as consequências são indefinidas. Para obter mais informações, consulte [Buffers adiada](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 A associação permanece em vigor até que ele é substituído por uma nova associação, a coluna é desassociada ou a instrução é liberada.  
  
## <a name="unbinding-columns"></a>Desassociando colunas  
 Para desvincular uma única coluna, um aplicativo chama **SQLBindCol** com *ColumnNumber* definido como o número de coluna e *TargetValuePtr* definido como um ponteiro nulo. Se *ColumnNumber* refere-se a uma coluna não associada, **SQLBindCol** ainda retornará SQL_SUCCESS.  
  
 Para desvincular todas as colunas, um aplicativo chama **SQLFreeStmt** com *fOption* definido como SQL_UNBIND. Isso também pode ser feito definindo o campo SQL_DESC_COUNT de descartar a zero.  
  
## <a name="rebinding-columns"></a>Reassociando colunas  
 Um aplicativo pode executar qualquer uma das duas operações para alterar a associação:  
  
-   Chamar **SQLBindCol** para especificar uma nova associação para uma coluna que já está associada. O driver substituirá a associação antiga pelo novo.  
  
-   Especifique um deslocamento a ser adicionada para o endereço de buffer especificado pela chamada de associação para **SQLBindCol**. Para obter mais informações, consulte a próxima seção, "Deslocamentos de associação".  
  
## <a name="binding-offsets"></a>Deslocamentos de associação  
 Um deslocamento de associação é um valor que é adicionado para os endereços dos buffers de dados e comprimento/indicador (conforme especificado no *TargetValuePtr* e *StrLen_or_IndPtr* argumento) antes que eles são cancelados. Quando os deslocamentos são usados, as associações são um "modelo" de como os buffers do aplicativo são dispostos e o aplicativo pode mover esta "template" para diferentes áreas de memória, alterando o deslocamento. Como o mesmo deslocamento é adicionado a cada endereço em cada associação, os deslocamentos relativos entre buffers para diferentes colunas devem ser o mesmo em cada conjunto de buffers. Isso é sempre verdadeiro quando a associação é usada; o aplicativo deve dispor cuidadosamente seus buffers para isso como true quando a associação é usada.  
  
 Usar um deslocamento de associação tem basicamente o mesmo efeito que Reassociar uma coluna chamando **SQLBindCol**. A diferença é que uma nova chamada para **SQLBindCol** Especifica novos endereços para o buffer de dados e o buffer de comprimento/indicador, enquanto o uso de um deslocamento de associação não altera os endereços, mas apenas adiciona um deslocamento para eles. O aplicativo pode especificar um novo deslocamento sempre que desejar, e esse deslocamento sempre é adicionado aos endereços originalmente associados. Em particular, se o deslocamento é definido como 0 ou se o atributo de instrução é definido como um ponteiro nulo, o driver usa os endereços originalmente associados.  
  
 Para especificar um deslocamento de associação, o aplicativo define o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para o endereço de um buffer sqlinteger que contém. Antes do aplicativo chama uma função que usa associações, ele coloca um deslocamento em bytes nesse buffer. Para determinar o endereço do buffer a ser usado, o driver adiciona o deslocamento para o endereço na associação. A soma do endereço e o deslocamento deve ser um endereço válido, mas não tem o endereço para o qual o deslocamento é adicionado ser válido. Para obter mais informações sobre como os deslocamentos de associação são usados, consulte "Endereços de Buffer", posteriormente nesta seção.  
  
## <a name="binding-arrays"></a>Matrizes de associação  
 Se o tamanho do conjunto de linhas (o valor do atributo de instrução SQL_ATTR_ROW_ARRAY_SIZE) for maior que 1, o aplicativo associa as matrizes de buffers em vez de buffers único. Para obter mais informações, consulte [cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md).  
  
 O aplicativo pode associar as matrizes de duas maneiras:  
  
-   Associe uma matriz para cada coluna. Isso é conhecido como *a associação* porque cada estrutura de dados (matriz) contém dados para uma única coluna.  
  
-   Defina uma estrutura para reter os dados para uma linha inteira e associar uma matriz dessas estruturas. Isso é conhecido como *a associação* porque cada estrutura de dados contém os dados de uma única linha.  
  
 Cada matriz de buffers deve ter pelo menos o mesmo número de elementos como o tamanho do conjunto de linhas.  
  
> [!NOTE]  
>  Um aplicativo deve verificar se o alinhamento é válido. Para obter mais informações sobre considerações de alinhamento, consulte [alinhamento](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>A associação  
 Em que a associação, o aplicativo associa dados separada e matrizes de comprimento/indicador para cada coluna.  
  
 Para usar a associação, o aplicativo primeiro define o atributo de instrução SQL_ATTR_ROW_BIND_TYPE como SQL_BIND_BY_COLUMN. (Esse é o padrão). Para cada coluna a ser associado, o aplicativo executa as seguintes etapas:  
  
1.  Aloca uma matriz de buffer de dados.  
  
2.  Aloca uma matriz de buffers de comprimento/indicador.  
  
    > [!NOTE]  
    >  Se o aplicativo grava descritores diretamente quando a associação é usada, matrizes separados podem ser usados para dados de comprimento e indicador.  
  
3.  Chamadas **SQLBindCol** com os seguintes argumentos:  
  
    -   *TargetType* é o tipo de um único elemento da matriz de buffer de dados.  
  
    -   *TargetValuePtr* é o endereço da matriz de buffer de dados.  
  
    -   *BufferLength* é o tamanho de um único elemento da matriz de buffer de dados. O *BufferLength* argumento é ignorado quando os dados são dados de comprimento fixo.  
  
    -   *StrLen_or_IndPtr* é o endereço da matriz de comprimento/indicador.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "Endereços de Buffer", posteriormente nesta seção. Para obter mais informações sobre a associação, consulte [a associação](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>A associação  
 Na associação, o aplicativo define uma estrutura que contém dados e comprimento/indicador buffers para cada coluna a ser associado.  
  
 Para usar a associação, o aplicativo executa as seguintes etapas:  
  
1.  Define uma estrutura para conter uma única linha de dados (incluindo os buffers de dados e comprimento/indicador) e aloca uma matriz dessas estruturas.  
  
    > [!NOTE]  
    >  Se o aplicativo grava descritores diretamente quando a associação é usada, campos separados podem ser usados para dados de comprimento e indicador.  
  
2.  Define o atributo de instrução SQL_ATTR_ROW_BIND_TYPE para o tamanho da estrutura que contém uma única linha de dados ou o tamanho de uma instância de um buffer no qual as colunas de resultados serão associadas. O comprimento deve incluir espaço para todas as colunas associadas e qualquer preenchimento da estrutura ou do buffer, para certificar-se de que, quando o endereço de uma coluna associada for incrementado com o comprimento especificado, o resultado apontará para o início da mesma coluna na linha seguinte. Ao usar o *sizeof* operador em ANSI C, esse comportamento é garantido.  
  
3.  Chamadas **SQLBindCol** com os argumentos a seguir para cada coluna a ser associado:  
  
    -   *TargetType* é o tipo de buffer do membro de dados a ser associado à coluna.  
  
    -   *TargetValuePtr* é o endereço do buffer do membro de dados no primeiro elemento da matriz.  
  
    -   *BufferLength* é o tamanho do buffer do membro de dados.  
  
    -   *StrLen_or_IndPtr* é o endereço do membro de comprimento/indicador a ser associado.  
  
 Para obter mais informações sobre como essas informações são usadas, consulte "Endereços de Buffer", posteriormente nesta seção. Para obter mais informações sobre a associação, consulte [a associação](../../../odbc/reference/develop-app/row-wise-binding.md).  
  
## <a name="buffer-addresses"></a>Endereços de buffer  
 O *endereço do buffer* é o endereço real do buffer de dados ou o comprimento/indicador. O driver calcula o endereço do buffer antes que ele grava os buffers (por exemplo, durante o tempo de busca). Ele é calculado da fórmula a seguir, que usa os endereços especificados no *TargetValuePtr* e *StrLen_or_IndPtr* argumentos, o deslocamento de associação e o número da linha:  
  
 *Ligado a endereço* + *associação deslocamento* + ((*linha número* – 1) x *tamanho do elemento*)  
  
 onde as variáveis da fórmula são definidas conforme descrito na tabela a seguir.  
  
|Variável|Description|  
|--------------|-----------------|  
|*Ligado a endereço*|Para os buffers de dados, o endereço especificado com o *TargetValuePtr* argumento **SQLBindCol**.<br /><br /> Para buffers de comprimento/indicador, o endereço especificado com o *StrLen_or_IndPtr* argumento **SQLBindCol**. Para obter mais informações, consulte "Comentários" na seção "Descritores e SQLBindCol".<br /><br /> Se o endereço associado for 0, nenhum valor de dados será retornado, mesmo se o endereço conforme calculado pela fórmula anterior é diferente de zero.|  
|*Deslocamento de associação*|Se a associação for usada, o valor armazenado no endereço especificado com o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Se a associação é usada ou se o valor do atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR é um ponteiro nulo, *associação deslocamento* é 0.|  
|*Número de linha*|O número da linha no conjunto de linhas de base 1. Para buscas de única linha, que são o padrão, isso é 1.|  
|*Tamanho do elemento*|O tamanho de um elemento na matriz associada.<br /><br /> Se a associação for usada, isso é **sizeof(SQLINTEGER)** para buffers de comprimento/indicador. Para os buffers de dados, é o valor de *BufferLength* argumento na **SQLBindCol** se o tipo de dados é de comprimento variável e o tamanho do tipo de dados se o tipo de dados é de comprimento fixo.<br /><br /> Se a associação for usada, esse é o valor do atributo de instrução SQL_ATTR_ROW_BIND_TYPE para buffers de dados e comprimento/indicador.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descritores e SQLBindCol  
 As seções a seguir descrevem como **SQLBindCol** interage com descritores.  
  
> [!CAUTION]  
>  Chamando **SQLBindCol** para uma instrução pode afetar outras instruções. Isso ocorre quando a descartar associado à instrução explicitamente é alocado e também está associado com outras instruções. Porque **SQLBindCol** modifica o descritor, as modificações se aplicam a todas as instruções ao qual esse descritor está associado. Se isso não é o comportamento necessário, o aplicativo deve desassociar este descritor de outras instruções antes de chamar **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Mapeamentos de argumento  
 Conceitualmente, **SQLBindCol** executa as seguintes etapas na sequência:  
  
1.  Chamadas **SQLGetStmtAttr** ao obter o identificador de descartar.  
  
2.  Chamadas **SQLGetDescField** ao obter campo SQL_DESC_COUNT desse descritor e se o valor a *ColumnNumber* argumento excede o valor de SQL_DESC_COUNT, chamadas **SQLSetDescField ** para aumentar o valor de SQL_DESC_COUNT para *ColumnNumber*.  
  
3.  Chamadas **SQLSetDescField** várias vezes para atribuir valores para os campos de descartar a seguir:  
  
    -   Define SQL_DESC_TYPE e SQL_DESC_CONCISE_TYPE como o valor de *TargetType*, exceto que se *TargetType* é um dos identificadores de um subtipo de datetime ou intervalo de concisa, ele define SQL_DESC_TYPE para SQL _ DATETIME ou SQL_INTERVAL, respectivamente; Define SQL_DESC_CONCISE_TYPE como o identificador conciso; e conjuntos de SQL_DESC_DATETIME_INTERVAL_CODE datetime correspondente ou subcódigo de intervalo.  
  
    -   Define um ou mais dos SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_DATETIME_INTERVAL_PRECISION, conforme apropriado para *TargetType*.  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH como o valor de *BufferLength*.  
  
    -   Define o campo SQL_DESC_DATA_PTR para o valor de *TargetValue*.  
  
    -   Define o campo SQL_DESC_INDICATOR_PTR como o valor de *StrLen_or_Ind*. (Consulte o parágrafo a seguir).  
  
    -   Define o campo SQL_DESC_OCTET_LENGTH_PTR como o valor de *StrLen_or_Ind*. (Consulte o parágrafo a seguir).  
  
 A variável que o *StrLen_or_Ind* argumento refere-se a é usado para obter informações de indicador e comprimento. Se uma busca encontrar um valor nulo para a coluna, ele armazena SQL_NULL_DATA nessa variável; Caso contrário, ele armazena o comprimento de dados nessa variável. Transmitindo um ponteiro nulo como *StrLen_or_Ind* mantém a operação de busca de retornar o comprimento de dados, mas faz com que a busca falhar se ele encontra um valor nulo e não tem como retornar SQL_NULL_DATA.  
  
 Se a chamada para **SQLBindCol** falhar, o conteúdo dos campos de descritor que ele tenha definida na descartar não são definidos e o valor do campo SQL_DESC_COUNT da descartar é alterado.  
  
## <a name="implicit-resetting-of-count-field"></a>Redefinindo implícita do campo de contagem  
 **SQLBindCol** define SQL_DESC_COUNT como o valor da *ColumnNumber* argumento apenas quando isso pode aumentar o valor de SQL_DESC_COUNT. Se o valor a *TargetValuePtr* argumento é um ponteiro nulo e o valor no *ColumnNumber* argumento for igual a SQL_DESC_COUNT (ou seja, quando desassociar o mais alto associado coluna), SQL_DESC_, em seguida, CONTAGEM é definida como o número da coluna associada restante mais alto.  
  
## <a name="cautions-regarding-sqldefault"></a>Advertências sobre SQL_DEFAULT  
 Para recuperar dados de coluna com êxito, o aplicativo deve determinar corretamente o comprimento e o ponto de partida dos dados no buffer de aplicativo. Quando o aplicativo especifica um explícita *TargetType*, facilmente detectados erros de concepção do aplicativo. No entanto, quando o aplicativo especifica um *TargetType* de SQL_DEFAULT, **SQLBindCol** pode ser aplicado a uma coluna de um tipo de dados diferente da pretendida pelo aplicativo, de alterações para o metadados ou aplicando o código para uma coluna diferente. Nesse caso, o aplicativo não pode determinar sempre o início ou o comprimento dos dados da coluna buscadas. Isso pode levar a erros de dados não relatados ou violações de memória.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa um **selecione** instrução na tabela de clientes para retornar um conjunto de resultados do cliente, IDs, nomes e números de telefone, classificados por nome. Depois, ele chama **SQLBindCol** para associar as colunas de dados para buffers de locais. Por fim, o aplicativo busca cada linha de dados com **SQLFetch** e imprime o nome, ID e número de telefone de cada cliente.  
  
 Para obter mais exemplos de código, consulte [SQLBulkOperations função](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [função SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md), e [função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
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
  
 Consulte também, [exemplo ODBC programa](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Buscar um bloco de dados ou rolar por um resultado definido|[Função SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Busca de várias linhas de dados|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Liberar buffers de coluna na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Busca de parte ou toda uma coluna de dados|[Função SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Colunas do conjunto de retorno do número de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)

