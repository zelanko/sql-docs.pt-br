---
title: Função SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285502"
---
# <a name="sqlgetdata-function"></a>Função SQLGetData
**Conformidade**  
 Versão introduzida: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLGetData** recupera dados para uma única coluna no conjunto de resultados ou para um único parâmetro após o **retorno do SQLParamData** SQL_PARAM_DATA_AVAILABLE. Ele pode ser chamado várias vezes para recuperar dados de comprimento variável em partes.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Alça de declaração.  
  
 *Col_or_Param_Num*  
 [Entrada] Para recuperar dados da coluna, é o número da coluna para a qual retornar dados. As colunas de conjunto de resultados são numeradas em ordem de coluna crescente a partir de 1. A coluna marcadores é a coluna número 0; isso só pode ser especificado se os marcadores estiverem habilitados.  
  
 Para recuperar dados de parâmetros, é a ordinal do parâmetro, que começa em 1.  
  
 *Targettype*  
 [Entrada] O identificador de tipo do tipo de dados C do buffer ** TargetValuePtr.* Para obter uma lista de tipos de dados c válidos e identificadores de tipo, consulte a seção [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) no apêndice D: Tipos de dados.  
  
 Se *o TargetType* estiver SQL_ARD_TYPE, o driver usará o identificador de tipo especificado no campo SQL_DESC_CONCISE_TYPE do ARD. Se *o TargetType* for SQL_APD_TYPE, **o SQLGetData** usará o mesmo tipo de dados C especificado no **SQLBindParameter**. Caso contrário, o tipo de dados C especificado no **SQLGetData** substitui o tipo de dados C especificado no **SQLBindParameter**. Se estiver SQL_C_DEFAULT, o driver selecionará o tipo de dados C padrão com base no tipo de dados SQL da fonte.  
  
 Você também pode especificar um tipo de dados C estendido. Para obter mais informações, consulte [Tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Saída] Ponteiro para o buffer no qual retornar os dados.  
  
 *O TargetValuePtr* não pode ser NULO.  
  
 *BufferLength*  
 [Entrada] Comprimento do buffer ** TargetValuePtr* em bytes.  
  
 O driver usa *BufferLength* para evitar \*escrever após o fim do buffer *TargetValuePtr* ao retornar dados de comprimento variável, como dados de caracteres ou binários. Observe que o driver conta o caractere de \*rescisão nula ao retornar dados de caracteres ao *TargetValuePtr*. **O TargetValuePtr* deve, portanto, conter espaço para o caractere de rescisão nula, ou o driver truncará os dados.  
  
 Quando o driver retorna dados de comprimento fixo, como um inteiro ou uma estrutura de data, o driver ignora *bufferLength* e assume que o buffer é grande o suficiente para conter os dados. Portanto, é importante que o aplicativo aloque um buffer grande o suficiente para dados de comprimento fixo ou o driver escreverá após o fim do buffer.  
  
 **SQLGetData** retorna SQLSTATE HY090 (string inválida ou comprimento de buffer) quando *BufferLength* é menor que 0, mas não quando *BufferLength* é 0.  
  
 *Strlen_or_indptr*  
 [Saída] Ponteiro para o buffer no qual retornar o comprimento ou valor do indicador. Se este for um ponteiro nulo, nenhum comprimento ou valor do indicador é devolvido. Isso retorna um erro quando os dados que estão sendo buscados são NULOS.  
  
 **SQLGetData** pode retornar os seguintes valores no buffer de comprimento/indicador:  
  
-   A duração dos dados disponíveis para retornar  
  
-   SQL_NO_TOTAL  
  
-   Sql_null_data  
  
 Para obter mais informações, consulte [Usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) e "Comentários" neste tópico.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Quando **o SQLGetData** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido ligando para **sqlGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e uma *alça* de controle de *declaração*. A tabela a seguir lista os valores SQLSTATE comumente retornados pelo **SQLGetData** e explica cada um no contexto desta função; a notação "(DM)" precede as descrições de SQLSTATEs devolvidas pelo Driver Manager. O código de devolução associado a cada valor SQLSTATE é SQL_ERROR, a menos que seja observado o contrário.  
  
|SQLSTATE|Erro|Descrição|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informacional específica do motorista. (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cordas, truncados direito|Nem todos os dados da coluna especificada, *Col_or_Param_Num,* poderiam ser recuperados em uma única chamada para a função. SQL_NO_TOTAL ou o comprimento dos dados restantes na coluna especificada antes da chamada \*atual para **SQLGetData** é devolvido em *StrLen_or_IndPtr*. (Função retorna SQL_SUCCESS_WITH_INFO.)<br /><br /> Para obter mais informações sobre o uso de várias chamadas para **SQLGetData** para uma única coluna, consulte "Comentários".|  
|01S07|Truncação fracionada|Os dados devolvidos para uma ou mais colunas foram truncados. Para os tipos de dados numéricos, a parte fracionada do número foi truncada. Por tempo, carimbo de tempo e tipos de dados de intervalo contendo um componente de tempo, a parte fracionada do tempo foi truncada.<br /><br /> (Função retorna SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação de atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pode ser convertido para o tipo de dados C especificado pelo argumento *TargetType*.|  
|07009|Índice de descritor inválido|O valor especificado para o argumento *Col_or_Param_Num* foi 0, e o atributo de declaração SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.<br /><br /> O valor especificado para o argumento *Col_or_Param_Num* foi maior do que o número de colunas no conjunto de resultados.<br /><br /> O *valor Col_or_Param_Num* não foi igual à ordinal do parâmetro disponível.<br /><br /> (DM) A coluna especificada estava vinculada. Esta descrição não se aplica aos drivers que retornam a máscara de bitSQL_GD_BOUND para a opção SQL_GETDATA_EXTENSIONS no **SQLGetInfo**.<br /><br /> (DM) O número da coluna especificada era menor ou igual ao número da coluna vinculada mais alta. Esta descrição não se aplica aos drivers que retornam a máscara de bitSQL_GD_ANY_COLUMN para a opção SQL_GETDATA_EXTENSIONS no **SQLGetInfo**.<br /><br /> (DM) O aplicativo já chamou **SQLGetData** para a linha atual; o número da coluna especificada na chamada atual foi menor do que o número da coluna especificada na chamada anterior; e o driver não retorna a máscara de bitSQL_GD_ANY_ORDER para a opção SQL_GETDATA_EXTENSIONS no **SQLGetInfo**.<br /><br /> (DM) O argumento *TargetType* foi SQL_ARD_TYPE, e o registro do descritor *Col_or_Param_Num* no ARD falhou na verificação de consistência.<br /><br /> (DM) O argumento *TargetType* foi SQL_ARD_TYPE, e o valor no campo SQL_DESC_COUNT do ARD foi menor do que o *argumento Col_or_Param_Num.*|  
|08S01|Falha no link de comunicação|O link de comunicação entre o driver e a fonte de dados à qual o driver estava conectado falhou antes da função ser concluída.|  
|22002|Variável indicador necessária, mas não fornecida|*StrLen_or_IndPtr* foi um ponteiro nulo e dados NULAS foram recuperados.|  
|22003|Valor numérico fora do alcance|Devolver o valor numérico (como numérico ou string) para a coluna teria feito com que a parte inteira (em oposição a fracionária) do número fosse truncada.<br /><br /> Para obter mais informações, consulte [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de data-hora inválido|A coluna de caracteres no conjunto de resultados estava vinculada a uma data, hora ou estrutura de carimbo de data C, e o valor na coluna era uma data, hora ou carimbo de tempo inválidos, respectivamente. Para obter mais informações, consulte [o apêndice D: Tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22012|Divisão por zero|Um valor de uma expressão aritmética que resultou em divisão por zero foi devolvido.|  
|22015|Estouro do campo de intervalo|Atribuir de um tipo sql numérico ou intervalado para um tipo de intervalo C causou uma perda de dígitos significativos no campo principal.<br /><br /> Ao retornar os dados para um tipo C de intervalo, não houve representação do valor do tipo SQL no tipo c do intervalo.|  
|22018|Valor de caractere inválido para especificação do elenco|Uma coluna de caracteres no conjunto de resultados foi devolvida a um buffer de caractereS C, e a coluna continha um caractere para o qual não havia representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um numérico exato ou aproximado, um período de data ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caracteres; e o valor na coluna não era um literal válido do tipo C ligado.|  
|24.000|Estado de cursor inválido|(DM) A função foi chamada sem antes chamar **SQLFetch** ou **SQLFetchScroll** para posicionar o cursor na linha de dados necessária.<br /><br /> (DM) O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.<br /><br /> Um cursor foi aberto no *StatementHandle* e **SQLFetch** ou **SQLFetchScroll** tinha sido chamado, mas o cursor foi posicionado antes do início do conjunto de resultados ou após o fim do conjunto de resultados.|  
|HY000|Erro geral|Ocorreu um erro para o qual não havia SQLSTATE específico e para o qual não foi definido sqlSTATE específico para a implementação. A mensagem de erro retornada pelo **SQLGetDiagRec** no buffer *MessageText* descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não conseguiu alocar a memória necessária para suportar a execução ou a conclusão da função.|  
|HY003|Tipo de programa fora de alcance|(DM) O argumento *TargetType* não era um tipo de dados válido, SQL_C_DEFAULT, SQL_ARD_TYPE (em caso de recuperação de dados de coluna) ou SQL_APD_TYPE (em caso de recuperação de dados de parâmetros).<br /><br /> (DM) O argumento *Col_or_Param_Num* era 0, e o argumento *TargetType* não foi SQL_C_BOOKMARK para um marcador de comprimento fixo ou SQL_C_VARBOOKMARK para um marcador de comprimento variável.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e, antes de concluir a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*e, em seguida, a função foi chamada novamente no *StatementHandle*.<br /><br /> A função foi chamada e, antes de ser concluída a execução, **sqlCancelou-se** ou **SQLCancelHandle** foi chamada no *StatementHandle* de um segmento diferente em um aplicativo multithread e, em seguida, a função foi chamada novamente no *StatementHandle*.|  
|HY009|Uso inválido do ponteiro nulo|(DM) O argumento *TargetValuePtr* era um ponteiro nulo.|  
|HY010|Erro de seqüência de função|(DM) O *StatementHandle* especificado não estava em um estado executado. A função foi chamada sem antes chamar **SQLExecDirect,** **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) Uma função de execução assíncrona foi chamada para o cabo de conexão associado ao *StatementHandle*. Esta função assíncrona ainda estava sendo executada quando a função **SQLGetData** foi chamada.<br /><br /> (DM) Uma função de execução assíncrona (não esta) foi chamada para o *StatementHandle* e ainda estava sendo executada quando esta função foi chamada.<br /><br /> (DM) **SQLExecute,** **SQLExecDirect,** **SQLBulkOperations**ou **SQLSetPos** foram chamados para o *StatementHandle* e retornaram SQL_NEED_DATA. Essa função foi chamada antes de os dados serem enviados para todos os parâmetros ou colunas de execução de dados.<br /><br /> (DM) O *StatementHandle* estava em um estado executado, mas nenhum conjunto de resultados foi associado ao *StatementHandle*.<br /><br /> Uma chamada para **SQLExeceute,** **SQLExecDirect**ou **SQLMoreResults** retornou SQL_PARAM_DATA_AVAILABLE, mas **o SQLGetData** foi chamado, em vez de **SQLParamData**.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacentes não podiam ser acessados, possivelmente devido às baixas condições de memória.|  
|HY090|Comprimento de seqüência ou buffer inválido|(DM) O valor especificado para *o argumento BufferLength* foi inferior a 0.<br /><br /> O valor especificado para o argumento *BufferLength* foi inferior a 4, o *Col_or_Param_Num* argumento foi definido como 0, e o driver era um driver ODBC 2 *.x.*|  
|HY109|Posição do cursor inválido|O cursor foi posicionado (por **SQLSetPos,** **SQLFetch,** **SQLFetchScroll**ou **SQLBulkOperations)** em uma linha que havia sido excluída ou não podia ser buscada.<br /><br /> O cursor era um cursor para a frente, e o tamanho do conjunto de linhas era maior do que um.|  
|HY117|A conexão está suspensa devido ao estado de transação desconhecido. Somente funções desconectadas e somente leitura são permitidas.|(DM) Para obter mais informações sobre o estado suspenso, consulte [a função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|O driver ou a fonte de dados não suporta o uso de **SQLGetData** com várias linhas no **SQLFetchScroll**. Esta descrição não se aplica aos drivers que retornam a máscara de bitSQL_GD_BLOCK para a opção SQL_GETDATA_EXTENSIONS no **SQLGetInfo**.<br /><br /> O driver ou a fonte de dados não suporta a conversão especificada pela combinação do argumento *TargetType* e do tipo de dados SQL da coluna correspondente. Esse erro só se aplica quando o tipo de dados SQL da coluna foi mapeado para um tipo de dados SQL específico do driver.<br /><br /> O driver suporta apenas ODBC 2 *.x*, e o argumento *TargetType* foi um dos seguintes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> e qualquer um dos tipos de dados do intervalo C listados em [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) no apêndice D: Tipos de dados.<br /><br /> O driver só suporta versões ODBC antes do 3.50, e o argumento *TargetType* foi SQL_C_GUID.|  
|HYT01|Tempo de tempo de conexão expirado|O período de tempo de tempo de conexão expirou antes que a fonte de dados respondesse à solicitação. O período de tempo de tempo de conexão é definido através **de SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não suporta esta função|(DM) O driver correspondente ao *StatementHandle* não suporta a função.|  
|IM017|A votação é desativada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a votação é desativada.|  
|IM018|**O SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior nesta alça.|Se a chamada de função anterior na alça retornar SQL_STILL_EXECUTING e se o modo de notificação estiver ativado, o **SQLCompleteAsync** deve ser chamado na alça para fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLGetData** retorna os dados em uma coluna especificada. **SQLGetData** só pode ser chamado depois que uma ou mais linhas forem buscadas a partir do resultado definido por **SQLFetch,** **SQLFetchScroll**ou **SQLExtendedFetch**. Se os dados de comprimento variável forem muito grandes para serem retornados em uma única chamada ao **SQLGetData** (devido a uma limitação no aplicativo), o **SQLGetData** pode recuperá-los em partes. É possível vincular algumas colunas seguidas e chamar **SQLGetData** para outras, embora isso esteja sujeito a algumas restrições. Para obter mais informações, consulte [Getting Long Data](../../../odbc/reference/develop-app/getting-long-data.md).  
  
 Para obter informações sobre o uso **do SQLGetData** com parâmetros de saída transmitidos, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-sqlgetdata"></a>Usando sqlgetdata  
 Se o driver não suportar extensões ao **SQLGetData,** a função só poderá retornar dados para colunas desvinculadas com um número maior que o da última coluna vinculada. Além disso, dentro de uma linha de dados, o valor do *argumento Col_or_Param_Num* em cada chamada para **SQLGetData** deve ser maior ou igual ao valor de *Col_or_Param_Num* na chamada anterior; ou seja, os dados devem ser recuperados em ordem de número de coluna crescente. Finalmente, se nenhuma extensão for suportada, **o SQLGetData** não poderá ser chamado se o tamanho do conjunto de linhas for maior que 1.  
  
 Os motoristas podem relaxar qualquer uma dessas restrições. Para determinar quais restrições um driver relaxa, um aplicativo chama **sqlGetInfo** com qualquer uma das seguintes opções SQL_GETDATA_EXTENSIONS:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** pode ser chamado para retornar os valores do parâmetro de saída. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_GD_ANY_COLUMN. Se essa opção for devolvida, **o SQLGetData** pode ser chamado para qualquer coluna não vinculada, incluindo aquelas antes da última coluna vinculada.  
  
-   SQL_GD_ANY_ORDER. Se essa opção for retornada, **o SQLGetData** pode ser chamado para colunas desvinculadas em qualquer ordem.  
  
-   SQL_GD_BLOCK. Se essa opção for devolvida pelo **SQLGetInfo** para o infoType SQL_GETDATA_EXTENSIONS, o driver suportará chamadas para **SQLGetData** quando o tamanho do conjunto de linhas for maior que 1 e o aplicativo pode chamar **SQLSetPos** com a opção SQL_POSITION de posicionar o cursor na linha correta antes de ligar para **o SQLGetData.**  
  
-   SQL_GD_BOUND. Se essa opção for retornada, **o SQLGetData** pode ser chamado para colunas vinculadas, bem como colunas não vinculadas.  
  
 Há duas exceções a essas restrições e a capacidade do motorista de relaxá-las. Primeiro, **o SQLGetData** nunca deve ser chamado para um cursor somente para frente quando o tamanho do conjunto de linhas for maior que 1. Em segundo lugar, se um driver suporta marcadores, ele deve sempre suportar a capacidade de chamar **SQLGetData** para a coluna 0, mesmo que não permita que aplicativos chamem **SQLGetData** para outras colunas antes da última coluna vinculada. (Quando um aplicativo está trabalhando com um driver ODBC 2 *.x,* **O SQLGetData** retornará com sucesso um marcador quando chamado com *Col_or_Param_Num* igual a 0 após uma chamada para **SQLFetch,** porque o **SQLFetch** é mapeado pelo ODBC 3 *.x* Driver Manager para **SQLExtendedFetch** com uma *orientação de SQL_FETCH_NEXT,* e **o SQLGetData** com *um Col_or_Param_Num* de 0 é mapeado pelo ODBC 3 *.x* Driver Manager para **SQLGetStmtOption** com uma *opção fOption* of SQL_GET_BOOKMARK.)  
  
 **SQLGetData** não pode ser usado para recuperar o marcador para uma linha apenas inserida chamando **SQLBulkOperations** com a opção SQL_ADD, porque o cursor não está posicionado na linha. Um aplicativo pode recuperar o marcador para tal linha vinculando a coluna 0 antes de ligar para **a SQLBulkOperations** com SQL_ADD, nesse caso, a **SQLBulkOperations** retorna o marcador no buffer vinculado. **SQLFetchScroll** pode então ser chamado com SQL_FETCH_BOOKMARK para reposicionar o cursor nessa linha.  
  
 Se o argumento *TargetType* for um tipo de dados de intervalo, a precisão de liderança do intervalo padrão (2) e a precisão dos segundos de intervalo padrão (6), conforme definido nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION e SQL_DESC_PRECISION do ARD, respectivamente, são usados para os dados. Se o argumento *TargetType* for um SQL_C_NUMERIC tipo de dados, a precisão padrão (definida pelo driver) e a escala padrão (0), definidas nos campos SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, serão usadas para os dados. Se qualquer precisão ou escala padrão não for apropriada, o aplicativo deve definir explicitamente o campo descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**. Ele pode definir o campo SQL_DESC_CONCISE_TYPE para SQL_C_NUMERIC e chamar **SQLGetData** com um argumento *TargetType* de SQL_ARD_TYPE, o que fará com que os valores de precisão e escala nos campos descritores sejam usados.  
  
> [!NOTE]
>  No ODBC 2 *.x,* os aplicativos definem *targetType* para \*SQL_C_DATE, SQL_C_TIME ou SQL_C_TIMESTAMP para indicar que *o TargetValuePtr* é uma estrutura de data, hora ou carimbo de data. No ODBC 3 *.x,* os aplicativos definem *targetType* para SQL_C_TYPE_DATE, SQL_C_TYPE_TIME ou SQL_C_TYPE_TIMESTAMP. O Driver Manager faz mapeamentos apropriados, se necessário, com base na versão de aplicativo e driver.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>Recuperando dados de comprimento variável em peças  
 **O SQLGetData** pode ser usado para recuperar dados de uma coluna que contém dados de comprimento variável em partes - ou seja, quando o identificador do tipo de dados SQL da coluna é SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY ou um identificador específico do driver para um tipo de comprimento variável.  
  
 Para recuperar dados de uma coluna em partes, o aplicativo chama **SQLGetData** várias vezes em sucessão para a mesma coluna. Em cada chamada, **o SQLGetData** retorna a próxima parte dos dados. Cabe ao aplicativo remontar as peças, tomando o cuidado de remover o caractere de rescisão nula de partes intermediárias dos dados de caracteres. Se houver mais dados para retornar ou não, o buffer foi alocado para o caractere de terminação, o **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE 01004 (Dados truncados). Quando retorna a última parte dos dados, o **SQLGetData** retorna SQL_SUCCESS. Nem SQL_NO_TOTAL nem zero podem ser devolvidos na última chamada válida para recuperar dados de uma coluna, pois o aplicativo não teria como saber quanto dos dados no buffer do aplicativo é válido. Se **o SQLGetData** for chamado depois disso, ele retornou SQL_NO_DATA. Para obter mais informações, consulte a próxima seção, "Recuperando dados com SQLGetData".  
  
 Marcadores de comprimento variável podem ser devolvidos em partes pelo **SQLGetData**. Como acontece com outros dados, uma chamada para **o SQLGetData** para retornar marcadores de comprimento variável em partes retornará SQLSTATE 01004 (dados string, truncados à direita) e SQL_SUCCESS_WITH_INFO quando houver mais dados a serem devolvidos. Isso é diferente do caso quando um marcador de comprimento variável é truncado por uma chamada para **SQLFetch** ou **SQLFetchScroll**, que retorna SQL_ERROR e SQLSTATE 22001 (dados de string, truncados à direita).  
  
 **SQLGetData** não pode ser usado para retornar dados de comprimento fixo em partes. Se **o SQLGetData** for chamado mais de uma vez seguida por uma coluna contendo dados de comprimento fixo, ele retorna SQL_NO_DATA para todas as chamadas após a primeira.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperando parâmetros de saída em fluxo  
 Se um driver suportar parâmetros de saída em fluxo, um aplicativo pode chamar **SQLGetData** com um pequeno buffer muitas vezes para recuperar um grande valor de parâmetro. Para obter mais informações sobre o parâmetro de saída transmitida, consulte [Recuperando parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="retrieving-data-with-sqlgetdata"></a>Recuperando dados com SQLGetData  
 Para retornar dados para a coluna especificada, **o SQLGetData** executa a seguinte seqüência de etapas:  
  
1.  Retorna SQL_NO_DATA se já devolveu todos os dados para a coluna.  
  
2.  Define \* *StrLen_or_IndPtr* para SQL_NULL_DATA se os dados forem NULOS. Se os dados forem NULOS e *StrLen_or_IndPtr* fosse um ponteiro nulo, **o SQLGetData** retorna SQLSTATE 22002 (variável indicador necessária, mas não fornecida).  
  
     Se os dados da coluna não forem NULOS, **o SQLGetData** prosseguirá para a etapa 3.  
  
3.  Se o atributo de declaração SQL_ATTR_MAX_LENGTH for definido como um valor não zero, se a coluna contiver caracteres ou dados binários e se **o SQLGetData** não tiver sido previamente chamado para a coluna, os dados são truncados para SQL_ATTR_MAX_LENGTH bytes.  
  
    > [!NOTE]  
    >  O atributo de declaração SQL_ATTR_MAX_LENGTH destina-se a reduzir o tráfego da rede. Geralmente é implementado pela fonte de dados, que trunca os dados antes de devolvê-los pela rede. Drivers e fontes de dados não são necessários para apoiá-lo. Portanto, para garantir que os dados sejam truncados para um determinado tamanho, um aplicativo deve alocar um buffer desse tamanho e especificar o tamanho no argumento *BufferLength.*  
  
4.  Converte os dados para o tipo especificado no *TargetType*. Os dados recebem a precisão e a escala padrão para esse tipo de dados. Se *o TargetType* for SQL_ARD_TYPE, o tipo de dados no campo SQL_DESC_CONCISE_TYPE do ARD é usado. Se *o TargetType* for SQL_ARD_TYPE, os dados receberão a precisão e a escala nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, dependendo do tipo de dados no campo SQL_DESC_CONCISE_TYPE. Se qualquer precisão ou escala padrão não for apropriada, o aplicativo deve definir explicitamente o campo descritor apropriado por uma chamada para **SQLSetDescField** ou **SQLSetDescRec**.  
  
5.  Se os dados foram convertidos em um tipo de dados de comprimento variável, como caractere ou binário, **o SQLGetData** verifica se o comprimento dos dados excede o *BufferLength*. Se o comprimento dos dados de caracteres (incluindo o caractere de terminação nula) exceder *o BufferLength,* **o SQLGetData** trunca os dados para *BufferLength* menos o comprimento de um caractere de rescisão nula. Em seguida, anula os dados. Se o comprimento dos dados binários exceder o comprimento do buffer de dados, o **SQLGetData** o truncará para *bytes BufferLength.*  
  
     Se o buffer de dados fornecido for muito pequeno para manter o caractere de rescisão nula, **o SQLGetData** retorna SQL_SUCCESS_WITH_INFO e o SQLSTATE 01004.  
  
     **O SQLGetData** nunca trunca dados convertidos em tipos de dados de comprimento fixo; ele sempre assume que o comprimento de **TargetValuePtr* é o tamanho do tipo de dados.  
  
6.  Coloca os dados convertidos (e possivelmente truncados) no \* *TargetValuePtr*. Observe que **o SQLGetData** não pode retornar dados fora de linha.  
  
7.  Coloca o comprimento dos \*dados em *StrLen_or_IndPtr*. Se *StrLen_or_IndPtr* fosse um ponteiro nulo, **o SQLGetData** não retornará o comprimento.  
  
    -   Para dados de caracteres ou binários, este é o comprimento dos dados após a conversão e antes da truncação devido ao *BufferLength*. Se o driver não puder determinar o comprimento dos dados após a conversão, como às vezes é o caso com dados longos, ele retorna SQL_SUCCESS_WITH_INFO e define o comprimento para SQL_NO_TOTAL. (A última chamada para **SQLGetData** deve sempre retornar o comprimento dos dados, não zero ou SQL_NO_TOTAL.) Se os dados foram truncados devido ao atributo de declaração SQL_ATTR_MAX_LENGTH, o \*valor deste atributo - ao contrário do comprimento real - é colocado em *StrLen_or_IndPtr*. Isso porque este atributo foi projetado para truncar dados no servidor antes da conversão, de modo que o driver não tem como descobrir qual é o comprimento real. Quando **sQLGetData** é chamado várias vezes em sucessão para a mesma coluna, este é o comprimento dos dados disponíveis no início da chamada atual; ou seja, o comprimento diminui a cada chamada subseqüente.  
  
    -   Para todos os outros tipos de dados, este é o comprimento dos dados após a conversão; ou seja, é o tamanho do tipo para o qual os dados foram convertidos.  
  
8.  Se os dados forem truncados sem perda de significância durante a conversão (por exemplo, o número real 1.234 é truncado quando convertido para o inteiro 1) ou porque o *BufferLength* é muito pequeno (por exemplo, a string "abcdef" é colocada em um buffer de 4 bytes), **o SQLGetData** retorna sQLSTATE 01004 (Dados truncados) e SQL_SUCCESS_WITH_INFO. Se os dados forem truncados sem perda de significância devido ao atributo de declaração SQL_ATTR_MAX_LENGTH, o **SQLGetData** retorna SQL_SUCCESS e não retorna sQLSTATE 01004 (Dados truncados).  
  
 O conteúdo do buffer de dados vinculado (se **o SQLGetData** for chamado em uma coluna vinculada) e o buffer comprimento/indicador são indefinidos se **o SQLGetData** não retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO.  
  
 Chamadas sucessivas para **SQLGetData** recuperarão dados da última coluna solicitada; compensações anteriores tornam-se inválidas. Por exemplo, quando a seguinte seqüência é realizada:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 a segunda chamada para SQLGetData(icol=n) recupera dados desde o início da coluna n. Qualquer compensação nos dados devido a chamadas anteriores ao **SQLGetData** para a coluna não é mais válida.  
  
## <a name="descriptors-and-sqlgetdata"></a>Descritores e SQLGetData  
 **O SQLGetData** não interage diretamente com nenhum campo descritor.  
  
 Se *o TargetType* for SQL_ARD_TYPE, o tipo de dados no campo SQL_DESC_CONCISE_TYPE do ARD é usado. Se *o TargetType* for SQL_ARD_TYPE ou SQL_C_DEFAULT, os dados receberão a precisão e a escala nos campos SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION e SQL_DESC_SCALE do ARD, dependendo do tipo de dados no campo SQL_DESC_CONCISE_TYPE.  
  
## <a name="code-example"></a>Exemplo de código  
 No exemplo a seguir, um aplicativo executa uma declaração **SELECT** para retornar um conjunto de resultados dos IDs, nomes e números de telefone do cliente classificados por nome, ID e número de telefone. Para cada linha de dados, ele chama **SQLFetch** para posicionar o cursor para a próxima linha. Ele chama **sqlGetData** para recuperar os dados buscados; os buffers para os dados e o número retornado de bytes são especificados na chamada para **SQLGetData**. Finalmente, ele imprime o nome, o id e o número de telefone de cada funcionário.  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Atribuindo armazenamento para uma coluna em um conjunto de resultados|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizando operações em massa que não se relacionam com a posição do cursor de bloco|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelamento do processamento de declarações|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Executando uma declaração SQL|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executando uma declaração SQL preparada|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscar um bloco de dados ou rolar através de um conjunto de resultados|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Buscando uma única linha de dados ou um bloco de dados em uma direção somente para a frente|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Envio de dados de parâmetros na hora da execução|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|Posicionando o cursor, atualizando dados no conjunto de linhas ou atualizando ou excluindo dados no conjunto de linhas|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parâmetros de saída usando SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
