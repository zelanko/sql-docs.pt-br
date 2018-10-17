---
title: Função SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 146967ebc31d5e7d8176d37ee5b8b0b97b6c0674
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769484"
---
# <a name="sqlfetchscroll-function"></a>Função SQLFetchScroll
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLFetchScroll** busca o conjunto de linhas especificado de dados do conjunto de resultados e retorna dados para todas as colunas associadas. Conjuntos de linhas podem ser especificados em uma posição absoluta ou relativa, ou pelo indicador.  
  
 Ao trabalhar com um driver de ODBC 2. x, o Gerenciador de Driver mapeia essa função para **SQLExtendedFetch**. Para obter mais informações, consulte [funções de mapeamento de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrução.  
  
 *FetchOrientation*  
 [Entrada]  
  
 Tipo de busca:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Para obter mais informações, consulte "Posicionando o Cursor", na seção "Comentários".  
  
 *FetchOffset*  
 [Entrada]  
  
 Número da linha de busca. A interpretação desse argumento depende do valor da *FetchOrientation* argumento. Para obter mais informações, consulte "Posicionando o Cursor", na seção "Comentários".  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Quando **SQLFetchScroll** retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO, um valor SQLSTATE associado pode ser obtido chamando **SQLGetDiagRec** com um HandleType de SQL_HANDLE_STMT e um identificador de StatementHandle. A tabela a seguir lista os valores SQLSTATE normalmente retornados por **SQLFetchScroll** e explica cada uma no contexto dessa função; a notação "(DM)" precede as descrições das SQLSTATEs retornados pelo Gerenciador de Driver. O código de retorno associado com cada valor SQLSTATE é SQL_ERROR, a menos que indicado o contrário. Se ocorrer um erro em uma única coluna, **SQLGetDiagField** pode ser chamado com um DiagIdentifier de SQL_DIAG_COLUMN_NUMBER para determinar a coluna que o erro ocorreu em; e **SQLGetDiagField** pode ser chamado com um DiagIdentifier de SQL_DIAG_ROW_NUMBER para determinar a linha que contém essa coluna.  
  
 Para todos esses SQLSTATEs que podem retornar SQL_SUCCESS_WITH_INFO ou SQL_ERROR (exceto 01xxx SQLSTATEs), SQL_SUCCESS_WITH_INFO será retornado se ocorrer um erro em um ou mais, mas nem todas as linhas de uma operação de várias linhas, e SQL_ERROR será retornado se ocorrer um erro em um operação de uma única linha.  
  
|SQLSTATE|Erro|Description|  
|--------------|-----------|-----------------|  
|01000|Aviso geral|Mensagem informativa de específicos do driver. (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01004|Dados de cadeia de caracteres truncados à direita|Cadeia de caracteres ou dados binários retornados para uma coluna resultaram em truncamento de caractere não vazios ou nulos de dados binários. Se fosse um valor de cadeia de caracteres, ele era truncados à direita.|  
|01S01|Erro na linha|Ocorreu um erro ao buscar uma ou mais linhas.<br /><br /> (Se este SQLSTATE é retornado quando um ODBC 3 *. x* aplicativo está funcionando com um ODBC 2 *. x* driver, ele pode ser ignorado.)|  
|01S06|Tentativa de buscar antes do conjunto de resultados retornado o primeiro conjunto de linhas|O conjunto de linhas solicitado sobreposta o início do conjunto de resultados quando FetchOrientation era SQL_FETCH_PRIOR, a posição atual estava além da primeira linha e o número da linha atual é menor que ou igual ao tamanho do conjunto de linhas.<br /><br /> O conjunto de linhas solicitado sobreposta o início do conjunto de resultados quando FetchOrientation era SQL_FETCH_PRIOR, a posição atual foi além do fim do conjunto de resultados e o tamanho do conjunto de linhas era maior do que o conjunto de resultados tamanho.<br /><br /> O conjunto de linhas solicitado sobreposta o início do conjunto de resultados quando FetchOrientation era SQL_FETCH_RELATIVE, FetchOffset estava negativo e o valor absoluto de FetchOffset era menor ou igual ao tamanho do conjunto de linhas.<br /><br /> O conjunto de linhas solicitado sobreposta o início do conjunto de resultados quando FetchOrientation era SQL_FETCH_ABSOLUTE, FetchOffset estava negativo e o valor absoluto de FetchOffset era maior do que o conjunto de resultados tamanho, mas menor ou igual ao tamanho do conjunto de linhas.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|01S07|Truncamento fracionário|Os dados retornados de uma coluna foi truncados. Para tipos de dados numéricos, a parte fracionária do número foi truncada. Para o tempo, carimbo de hora e tipos de dados de intervalo que contém um componente de tempo, a parte fracionária do tempo foi truncada.<br /><br /> (A função retornará SQL_SUCCESS_WITH_INFO.)|  
|07006|Violação do atributo de tipo de dados restrito|O valor de dados de uma coluna no conjunto de resultados não pôde ser convertido para o tipo de dados especificado por *TargetType* na **SQLBindCol**.<br /><br /> A coluna 0 foi associada com um tipo de dados de SQL_C_BOOKMARK, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_VARIABLE.<br /><br /> A coluna 0 foi associada com um tipo de dados de SQL_C_VARBOOKMARK, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS não foi definido como SQL_UB_VARIABLE.|  
|07009|Índice de descritor inválido|O driver foi um ODBC 2 *. x* driver não oferece suporte a **SQLExtendedFetch**, e um número de coluna especificado na associação para uma coluna era 0.<br /><br /> A coluna 0 foi associada, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.|  
|08S01|Falha de link de comunicação|Falha do link de comunicação entre o driver e a fonte de dados ao qual o driver foi conectado antes do processamento da função foi concluída.|  
|22001|Dados de cadeia de caracteres truncados à direita|Um indicador de comprimento variável retornado para uma coluna foi truncado.|  
|22002|Variável de indicador necessária, mas não fornecida|Dados nulos foi buscados em uma coluna cuja *StrLen_or_IndPtr* definido por **SQLBindCol** (ou SQL_DESC_INDICATOR_PTR definido pela **SQLSetDescField** ou  **SQLSetDescRec**) é um ponteiro nulo.|  
|22003|Valor numérico fora do intervalo|Retornando o valor numérico (como numérico ou cadeia de caracteres) para um ou mais colunas associadas teria causado parte inteira (em vez de fracionários) o número a ser truncado.<br /><br /> Para obter mais informações, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) na [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de data/hora inválido|Uma coluna de caractere no conjunto de resultados foi associada a uma data, hora ou estrutura de carimbo de hora C, e um valor na coluna foi, respectivamente, uma data inválida, hora ou carimbo de hora.|  
|22012|Divisão por zero|Um valor de uma expressão aritmética foi retornado, que resultou na divisão por zero.|  
|22015|Estouro no campo de intervalo|A atribuição de um numérico exato ou o intervalo de tipo SQL para um tipo de intervalo C causou uma perda de dígitos significativos no campo à esquerda.<br /><br /> Ao buscar dados para um tipo de intervalo de C, não houve nenhuma representação do valor do tipo SQL no tipo de intervalo de C.|  
|22018|Valor de caractere inválido para especificação de conversão|Uma coluna de caractere no conjunto de resultados foi associada a um buffer de caracteres C, e a coluna continha um caractere para o qual não havia nenhuma representação no conjunto de caracteres do buffer.<br /><br /> O tipo C era um valor numérico exato ou aproximado, uma data e hora ou um tipo de dados de intervalo; o tipo SQL da coluna era um tipo de dados de caractere; e o valor na coluna não era um literal válido do tipo C associado.|  
|24000|Estado de cursor inválido|O *StatementHandle* estava em um estado executado mas nenhum conjunto de resultados foi associado a *StatementHandle*.|  
|40001|Falha na serialização|A transação na qual a busca foi executada foi encerrada para evitar o deadlock.|  
|40003|Conclusão desconhecida de declaração|A conexão associada falhou durante a execução dessa função e o estado da transação não pode ser determinado.|  
|HY000|Erro geral|Ocorreu um erro para o qual não houve nenhum SQLSTATE específico e para o qual não foi definida nenhuma SQLSTATE específicos de implementação. A mensagem de erro retornada por **SQLGetDiagRec** na  *\*MessageText* buffer descreve o erro e sua causa.|  
|HY001|Erro de alocação de memória|O driver não pôde alocar a memória necessária para dar suporte à execução ou a conclusão da função.|  
|HY008|Operação cancelada|O processamento assíncrono foi habilitado para o *StatementHandle*. A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle*. Em seguida, a função foi chamada novamente na *StatementHandle*.<br /><br /> A função foi chamada e antes ele concluiu a execução, **SQLCancel** ou **SQLCancelHandle** foi chamado no *StatementHandle* de um thread diferente em um aplicativos multithread.|  
|HY010|Erro de sequência de função|(DM) uma função de execução assíncrona foi chamada para o identificador de conexão que está associado a *StatementHandle*. Essa função assíncrona ainda estava em execução quando o **SQLFetchScroll** função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** foi chamado para o *StatementHandle* e retornado SQL_PARAM_DATA_ DISPONÍVEL. Essa função foi chamada antes de dados foram recuperados para todos os parâmetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* não estava em um estado executado. A função foi chamada sem primeiro chamar **SQLExecDirect**, **SQLExecute** ou uma função de catálogo.<br /><br /> (DM) uma função de execução assíncrona (não desse último) foi chamada para o *StatementHandle* e ainda estava em execução quando essa função foi chamada.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, ou **SQLSetPos** foi chamado para o  *StatementHandle* e retornados de SQL_NEED_DATA. Essa função foi chamada antes de dados foi enviados para todos os parâmetros de dados em execução ou colunas.<br /><br /> (DM) **SQLFetch** foi chamado para o *StatementHandle* após **SQLExtendedFetch** foi chamado e antes **SQLFreeStmt** com o SQL _ Opção Fechar foi chamada.|  
|HY013|Erro de gerenciamento de memória|A chamada de função não pôde ser processada porque os objetos de memória subjacente não pôde ser acessados, possivelmente devido a condições de memória insuficiente.|  
|HY090|Comprimento de buffer ou cadeia de caracteres inválido|O atributo da instrução SQL_ATTR_USE_BOOKMARK foi definido como SQL_UB_VARIABLE e a coluna 0 estava associada a um buffer cujo comprimento não era igual ao comprimento máximo para o indicador para esse conjunto de resultados. (Esse tamanho está disponível no campo do IRD SQL_DESC_OCTET_LENGTH e pode ser obtido chamando **SQLDescribeCol**, **SQLColAttribute**, ou **SQLGetDescField**.)|  
|HY106|Tipo de busca fora do intervalo|O valor especificado para o argumento FetchOrientation de DM) era inválido.<br /><br /> (DM) o argumento FetchOrientation era SQL_FETCH_BOOKMARK, e o atributo da instrução SQL_ATTR_USE_BOOKMARKS foi definido como SQL_UB_OFF.<br /><br /> O valor do atributo de instrução SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_FORWARD_ONLY e o valor do argumento que fetchorientation não era SQL_FETCH_NEXT.<br /><br /> O valor do atributo de instrução SQL_ATTR_CURSOR_SCROLLABLE era SQL_NONSCROLLABLE e o valor do argumento que fetchorientation não era SQL_FETCH_NEXT.|  
|HY107|Valor de linha fora do intervalo|O valor especificado com o atributo de instrução SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, mas o valor especificado com o atributo da instrução SQL_ATTR_KEYSET_SIZE era maior que 0 e menor que o valor especificado com o SQL_ATTR_ROW_ARRAY_ Atributo de instrução de tamanho.|  
|HY111|Valor de indicador inválido|O argumento FetchOrientation era SQL_FETCH_BOOKMARK, e o indicador apontado pelo valor no atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR não era válido ou é um ponteiro nulo.|  
|HY117|Conexão está suspenso devido ao estado de transação desconhecida. Somente se desconectar e funções de somente leitura são permitidas.|(DM) para obter mais informações sobre o estado suspenso, consulte [função SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Recurso opcional não implementado|A driver ou fonte de dados não suporta a conversão especificada pela combinação da *TargetType* na **SQLBindCol** e o tipo de dados SQL da coluna correspondente.|  
|HYT00|Tempo limite esgotado|O período de tempo limite da consulta expirou antes da fonte de dados retornada um conjunto de resultado solicitada. O período de tempo limite é definido por meio de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tempo limite da Conexão expirado|O período de tempo limite de conexão expirado antes que a fonte de dados respondeu à solicitação. O período de tempo limite de conexão é definido por meio **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Driver não oferece suporte a essa função|O driver em (DM) associado a *StatementHandle* não suporta a função.|  
|IM017|Sondagem está desabilitada no modo de notificação assíncrona|Sempre que o modelo de notificação é usado, a sondagem é desabilitada.|  
|IM018|**SQLCompleteAsync** não foi chamado para concluir a operação assíncrona anterior neste identificador.|Se a chamada de função anterior no identificador retornará SQL_STILL_EXECUTING e se o modo de notificação está habilitado, **SQLCompleteAsync** deve ser chamado no identificador de fazer o pós-processamento e concluir a operação.|  
  
## <a name="comments"></a>Comentários  
 **SQLFetchScroll** retorna um conjunto de linhas especificado do conjunto de resultados. Conjuntos de linhas podem ser especificados por posição absoluta ou relativa, ou pelo indicador. **SQLFetchScroll** pode ser chamado somente enquanto existe um conjunto de resultados — ou seja, após uma chamada que cria um conjunto de resultados e antes do cursor over que o conjunto de resultados está fechado. Se todas as colunas são associadas, ele retorna os dados nessas colunas. Se o aplicativo tiver especificado um ponteiro para um buffer no qual retornar o número de linhas buscadas, ou uma matriz de status de linha **SQLFetchScroll** retorna essas informações também. Chamadas para **SQLFetchScroll** podem ser misturadas a chamadas para **SQLFetch** , mas não podem ser misturadas a chamadas para **SQLExtendedFetch**.  
  
 Para obter mais informações, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md) e [usando cursores roláveis](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Posicionando o Cursor  
 Quando o conjunto de resultados é criado, o cursor é posicionado antes do início do conjunto de resultados. **SQLFetchScroll** posiciona o cursor em bloco com base nos valores da *FetchOrientation* e *FetchOffset* argumentos, conforme mostrado na tabela a seguir. As regras exatas para determinar o início do novo conjunto de linhas são mostradas na próxima seção.  
  
|FetchOrientation|Significado|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Retorne o próximo conjunto de linhas. Isso é equivalente a chamar **SQLFetch**.<br /><br /> **SQLFetchScroll** ignora o valor da *FetchOffset*.|  
|SQL_FETCH_PRIOR|Retorne o conjunto de linhas anterior.<br /><br /> **SQLFetchScroll** ignora o valor da *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Retornar o conjunto de linhas *FetchOffset* desde o início do conjunto de linhas atual.|  
|SQL_FETCH_ABSOLUTE|Retornar o conjunto de linhas a partir da linha *FetchOffset*.|  
|SQL_FETCH_FIRST|Retorne o primeiro conjunto de linhas no conjunto de resultados.<br /><br /> **SQLFetchScroll** ignora o valor da *FetchOffset*.|  
|SQL_FETCH_LAST|Retorne o último conjunto de linhas completo no conjunto de resultados.<br /><br /> **SQLFetchScroll** ignora o valor da *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Retorne o conjunto de linhas FetchOffset linhas de indicador especificado pelo atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 Drivers não são necessários para dar suporte a todas as orientações de busca; um aplicativo chama **SQLGetInfo** com um tipo de informação de SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 ou SQL_STATIC_CURSOR_ATTRIBUTES1 (dependendo do tipo de cursor) para determinar quais fetch as orientações são compatíveis com o driver. O aplicativo deve examinar as máscaras de bits SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE e WQL_CA1_BOOKMARK nesses tipos de informações. Além disso, se o cursor é de somente avanço e FetchOrientation não SQL_FETCH_NEXT, **SQLFetchScroll** retornará SQLSTATE HY106 (tipo fora do intervalo de busca).  
  
 O atributo da instrução SQL_ATTR_ROW_ARRAY_SIZE Especifica o número de linhas no conjunto de linhas. Se o conjunto de linhas que estão sendo buscadas por **SQLFetchScroll** sobrepõe o final do conjunto de resultados, **SQLFetchScroll** retorna um conjunto de linhas parcial. Ou seja, se S + R – 1 é maior que L, onde S é a linha inicial do conjunto de linhas que estão sendo buscada, R é o tamanho do conjunto de linhas e L é a última linha no conjunto de resultados, em seguida, somente o primeiro L – S + 1 linhas do conjunto de linhas são válidos. As linhas restantes estão vazias e têm um status de SQL_ROW_NOROW.  
  
 Após **SQLFetchScroll** retorna, a linha atual é a primeira linha do conjunto de linhas.  
  
## <a name="cursor-positioning-rules"></a>Regras de posicionamento do cursor  
 As seções a seguir descrevem as regras exatas para cada valor de FetchOrientation. Essas regras usar a notação a seguir.  
  
|Notação|Significado|  
|--------------|-------------|  
|*Antes de iniciar*|O cursor em bloco é posicionado antes do início do conjunto de resultados. Se a primeira linha do novo conjunto de linhas é antes do início do conjunto de resultados, **SQLFetchScroll** retorne SQL_NO_DATA.|  
|*Após o fim*|O cursor em bloco é posicionado após o final do resultado definido. Se a primeira linha do novo conjunto de linhas for após o final do conjunto de resultados **SQLFetchScroll** retorne SQL_NO_DATA.|  
|*CurrRowsetStart*|O número da primeira linha no conjunto de linhas atual.|  
|*LastResultRow*|O número da última linha no conjunto de resultados.|  
|*RowsetSize*|O tamanho do conjunto de linhas.|  
|*FetchOffset*|O valor de *FetchOffset* argumento.|  
|*BookmarkRow*|A linha correspondente para o indicador especificado pelo atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Antes de iniciar*|1|  
|*CurrRowsetStart + RowsetSize*[1]  *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*Após o fim*|  
|*Após o fim*|*Após o fim*|  
  
 [1] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, esse é o tamanho do conjunto de linhas que foi usado com a chamada anterior.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Antes de iniciar*|*Antes de iniciar*|  
|*CurrRowsetStart = 1*|*Antes de iniciar*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2].</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*Após o término e LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Após o término LastResultRow e > = RowsetSize* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2].</sup>|  
  
 [1] **SQLFetchScroll** retornará SQLSTATE 01S06 (tentativa de buscar antes do conjunto de resultados retornado o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [2] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, isso é o novo tamanho do conjunto de linhas.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*(Antes de iniciar e FetchOffset > 0) OU (após final e FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart e FetchOffset < = 0*|*Antes de iniciar*|  
|*CurrRowsetStart = 1 FetchOffset AND < 0*|*Antes de iniciar*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 e &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Antes de iniciar*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 e &#124; FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Após o fim*|  
|*Após o término FetchOffset e > = 0*|*Após o fim*|  
  
 [1] ***SQLFetchScroll*** retorna o mesmo conjunto de linhas como se ele foi chamado com FetchOrientation definido como SQL_FETCH_ABSOLUTE. Para obter mais informações, consulte a seção "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** retornará SQLSTATE 01S06 (tentativa de buscar antes do conjunto de resultados retornado o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [3] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, isso é o novo tamanho do conjunto de linhas.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Antes de iniciar*|  
|*FetchOffset < 0 e &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*Antes de iniciar*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Após o fim*|  
  
 [1] **SQLFetchScroll** retornará SQLSTATE 01S06 (tentativa de buscar antes do conjunto de resultados retornado o primeiro conjunto de linhas) e SQL_SUCCESS_WITH_INFO.  
  
 [2] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, isso é o novo tamanho do conjunto de linhas.  
  
 Uma busca absoluta executada em relação a um cursor dinâmico não pode fornecer o resultado necessário porque as posições de linha em um cursor dinâmico são indeterminadas. Essa operação é equivalente a uma busca primeiro, seguida por uma busca relativa; não é uma operação atômica, pois é uma busca absoluta em um cursor estático.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*Qualquer*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] se o tamanho do conjunto de linhas tiver sido alterado desde a chamada anterior para buscar linhas, isso é o novo tamanho do conjunto de linhas.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 As seguintes regras se aplicam.  
  
|Condição|Primeira linha do novo conjunto de linhas|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Antes de iniciar*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Após o fim*|  
  
 Para obter informações sobre os indicadores, consulte [indicadores (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Efeito de adicionado, excluído e linhas de erro em movimento do Cursor  
 Às vezes, Cursores estáticos e controlados por detectam linhas adicionadas ao resultado definir e remover linhas excluídas do conjunto de resultados. Chamando **SQLGetInfo** com o SQL_STATIC_CURSOR_ATTRIBUTES2 e SQL_KEYSET_CURSOR_ATTRIBUTES2 opções e examinando o SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS e SQL_CA2_SENSITIVITY_ Máscaras de bits de atualizações, um aplicativo que determina se os cursores implementados por um determinado driver de fazer isso. Para os drivers que podem detectar linhas excluídas e removê-los, os parágrafos a seguir descrevem os efeitos desse comportamento. Para os drivers que podem detectar linhas excluídas, mas não é possível removê-los, as exclusões não têm efeito sobre movimentos do cursor e os parágrafos a seguir não se aplicam.  
  
 Se o cursor detecta linhas adicionadas ao conjunto de resultados ou remove linhas excluídas do conjunto de resultados, ele aparece como se ele detecta essas alterações somente quando ele busca dados. Isso inclui o caso quando **SQLFetchScroll** é chamado com FetchOrientation definido como SQL_FETCH_RELATIVE e FetchOffset definido como 0 para buscar novamente o mesmo conjunto de linhas, mas não inclui o caso quando SQLSetPos é chamado com fOption definido como SQL _ ATUALIZAÇÃO. No último caso, os dados nos buffers de conjunto de linhas são atualizados, mas não refetched e as linhas excluídas não são removidas do conjunto de resultados. Assim, quando uma linha é excluída do ou inserida no conjunto de linhas atual, o cursor não modifica os buffers de conjunto de linhas. Em vez disso, ele detecta a alteração quando ele busca qualquer conjunto de linhas que incluídas anteriormente a linha excluída ou agora inclui a linha inserida.  
  
 Por exemplo:  
  
```  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 Quando **SQLFetchScroll** retorna um novo conjunto de linhas que tem uma posição em relação ao conjunto de linhas atual — ou seja, FetchOrientation é SQL_FETCH_NEXT, SQL_FETCH_PRIOR ou SQL_FETCH_RELATIVE — ele não inclui alterações no conjunto de linhas atual ao calcular a posição inicial do novo conjunto de linhas. No entanto, ele inclui alterações fora do conjunto de linhas atual se ele é capaz de detectá-las. Além disso, quando **SQLFetchScroll** retorna um novo conjunto de linhas que tem uma posição independente do conjunto de linhas atual — ou seja, FetchOrientation é SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE ou SQL_FETCH_BOOKMARK — ele inclui todas as alterações, que ele é capaz de detectar, mesmo se estiverem no conjunto de linhas atual.  
  
 Ao determinar se as linhas adicionadas recentemente são dentro ou fora do conjunto de linhas atual, um conjunto de linhas parcial é considerado para terminar a última linha válido; ou seja, a última linha para o qual o status de linha não está SQL_ROW_NOROW. Por exemplo, suponha que o cursor é capaz de detectar linhas adicionadas recentemente, o conjunto de linhas atual é um conjunto de linhas parcial, o aplicativo adiciona novas linhas e o cursor adiciona essas linhas ao final do conjunto de resultados. Se o aplicativo chamar **SQLFetchScroll** com FetchOrientation definido como SQL_FETCH_NEXT, **SQLFetchScroll** retorna o conjunto de linhas começando com a primeira linha recém-adicionada.  
  
 Por exemplo, suponha que o conjunto de linhas atual consiste em linhas 21 a 30, o tamanho do conjunto de linhas é 10, o cursor remove linhas excluídas do conjunto de resultados e cursor detecta linhas adicionadas ao conjunto de resultados. A tabela a seguir mostra as linhas **SQLFetchScroll** retorna em várias situações.  
  
|Alterar|Tipo de busca|FetchOffset|Novo conjunto de linhas [1]|  
|------------|----------------|-----------------|---------------------|  
|Excluir linha 21|NEXT|0|31 a 40|  
|Excluir linha 31|NEXT|0|32 para 41|  
|Inserir uma linha entre as linhas 21 e 22|NEXT|0|31 a 40|  
|Inserir uma linha entre as linhas 30 e 31|NEXT|0|Linha inserida, 31 a 39|  
|Excluir linha 21|PRIOR|0|11 a 20|  
|Excluir linha 20|PRIOR|0|10 a 19|  
|Inserir uma linha entre as linhas 21 e 22|PRIOR|0|11 a 20|  
|Inserir uma linha entre as linhas 20 e 21|PRIOR|0|linha de 12 a 20, inserida|  
|Excluir linha 21|RELATIVE|0|22 a 31<sup>[2]</sup>|  
|Excluir linha 21|RELATIVE|1|22 a 31|  
|Inserir uma linha entre as linhas 21 e 22|RELATIVE|0|linha inserida 21, 22 a 29|  
|Inserir uma linha entre as linhas 21 e 22|RELATIVE|1|22 a 31|  
|Excluir linha 21|ABSOLUTE|21|22 a 31<sup>[2]</sup>|  
|Excluir linha 22|ABSOLUTE|21|21, 23 a 31|  
|Inserir uma linha entre as linhas 21 e 22|ABSOLUTE|22|Linha inserida, 22 a 29|  
  
 [1] essa coluna usa os números de linha antes de todas as linhas foram inseridas ou excluídas.  
  
 [2]] nesse caso, o cursor tenta retornar as linhas a partir da linha 21. Porque a linha 21 foi excluída, a primeira linha, que ela retorna é linha 22.  
  
 Linhas de erro (ou seja, as linhas com um status de SQL_ROW_ERROR) não afetam o movimento do cursor. Por exemplo, se o conjunto de linhas atual começa com a linha 11 e o status da linha 11 é SQL_ROW_ERROR, chamando **SQLFetchScroll** com FetchOrientation definido como SQL_FETCH_RELATIVE e FetchOffset definido como 5 retorna o conjunto de linhas a partir da linha 16, Assim como faria se o status da linha 11 foi SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Retornando dados em colunas associadas  
 **SQLFetchScroll** retorna dados em colunas associadas a mesma forma que **SQLFetch**. Para obter mais informações, consulte "Retornando dados em associado colunas no" [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Se nenhuma coluna estiver associada, **SQLFetchScroll** não retornar dados, mas move o cursor em bloco para a posição especificada. Se os dados podem ser recuperados de colunas não associadas de um cursor em bloco com **SQLGetData** depende do driver. Esse recurso tem suporte se uma chamada para **SQLGetInfo** retorna o SQL_GD_BLOCK de bits para o tipo de informação SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Endereços de buffer  
 **SQLFetchScroll** usa a mesma fórmula para determinar o endereço de buffers de dados e comprimento/indicador conforme **SQLFetch**. Para obter mais informações, consulte "Endereços de Buffer" na [função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matriz de status da linha  
 **SQLFetchScroll** define os valores na matriz de status de linha da mesma maneira como SQLFetch. Para obter mais informações, consulte "Matriz de Status de linha" em [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Buffer de linhas buscadas  
 **SQLFetchScroll** retorna o número de linhas buscadas no buffer de linhas buscadas da mesma maneira como **SQLFetch**. Para obter mais informações, consulte "Linhas buscadas Buffer" na [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 Quando um aplicativo chama **SQLFetchScroll** em um driver do ODBC 3. x, chama o Gerenciador de Driver **SQLFetchScroll** no driver. Quando um aplicativo chama **SQLFetchScroll** em um driver do ODBC 2. x, o Gerenciador de Driver chama SQLExtendedFetch no driver. Porque **SQLFetchScroll** e SQLExtendedFetch manipular erros de maneira ligeiramente diferente, o aplicativo vê o comportamento de erro ligeiramente diferente quando ele chama **SQLFetchScroll** no ODBC 2.x e ODBC drivers 3.x.  
  
 **SQLFetchScroll** retorna erros e avisos da mesma maneira como **SQLFetch**; para obter mais informações, consulte "Tratamento de erros" na **SQLFetch**. **SQLExtendedFetch** retorna erros da mesma maneira como **SQLFetch**, com as seguintes exceções:  
  
 Quando ocorre um aviso se aplica a uma linha específica no conjunto de linhas, SQLExtendedFetch define a entrada correspondente na matriz de status de linha para SQL_ROW_SUCCESS, não SQL_ROW_SUCCESS_WITH_INFO.  
  
 Se ocorrerem erros em cada linha no conjunto de linhas, SQLExtendedFetch retorna SQL_SUCCESS_WITH_INFO, não SQL_ERROR.  
  
 Em cada grupo de registros de status que se aplica a uma linha individual, o primeiro registro de status retornado pelo SQLExtendedFetch deve conter o SQLSTATE 01S01 (erro na linha); **SQLFetchScroll** não retorna este SQLSTATE. Se não puder retornar SQLSTATEs adicionais SQLExtendedFetch, ele deve retornar essa SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll e simultaneidade otimista  
 Se um cursor usa a simultaneidade otimista — ou seja, o atributo de instrução SQL_ATTR_CONCURRENCY tem um valor de SQL_CONCUR_VALUES ou SQL_CONCUR_ROWVER — **SQLFetchScroll** atualiza os valores de simultaneidade otimista usados pelos dados o código-fonte para detectar se uma linha foi alterada. Isso acontece sempre que **SQLFetchScroll** busca um novo conjunto de linhas, incluindo quando ele refetches o conjunto de linhas atual. (Ele é chamado com FetchOrientation definido como SQL_FETCH_RELATIVE e FetchOffset definido como 0.)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll e ODBC Drivers de 2. x  
 Quando um aplicativo chama **SQLFetchScroll** em um driver do ODBC 2. x, o Gerenciador de Driver mapeia essa chamada para **SQLExtendedFetch**. Ele passa os seguintes valores para os argumentos de **SQLExtendedFetch**.  
  
|Argumento SQLExtendedFetch|Valor|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle na **SQLFetchScroll**.|  
|FetchOrientation|FetchOrientation na **SQLFetchScroll**.|  
|FetchOffset|Se FetchOrientation não for SQL_FETCH_BOOKMARK, o valor do argumento FetchOffset na **SQLFetchScroll** é usado.<br /><br /> Se FetchOrientation for SQL_FETCH_BOOKMARK, o valor armazenado no endereço especificado pelo atributo de instrução SQL_ATTR_FETCH_BOOKMARK_PTR é usado.|  
|RowCountPtr|O endereço especificado pelo atributo SQL_ATTR_ROWS_FETCHED_PTR instrução.|  
|RowStatusArray|O endereço especificado pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.|  
  
 Para obter mais informações, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) no Apêndice g: Driver diretrizes para compatibilidade com versões anteriores.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descritores e SQLFetchScroll  
 **SQLFetchScroll** interage com descritores da mesma maneira como **SQLFetch**. Para obter mais informações, consulte a seção "Descritores e SQLFetchScroll" [função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Exemplo de código  
 Ver [a associação por coluna](../../../odbc/reference/develop-app/column-wise-binding.md), [associação por linha](../../../odbc/reference/develop-app/row-wise-binding.md), [posicionado instruções Update e Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), e [atualizando linhas no conjunto de linhas com SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Um buffer de associação a uma coluna em um conjunto de resultados|[Função SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Executando operações de exclusão, atualização ou inserção em massa|[Função SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Cancelando o processamento de instrução|[Função SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Retornando informações sobre uma coluna em um conjunto de resultados|[Função SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Executar uma instrução SQL|[Função SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Executar uma instrução SQL preparada|[Função SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Buscando uma única linha ou um bloco de dados em uma direção de somente avanço|[Função SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Fechando o cursor na instrução|[Função SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Colunas de conjunto de retorno do número de resultados|[Função SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Posicionando o cursor, a atualização de dados no conjunto de linhas, ou a atualização ou exclusão de dados no conjunto de resultados|[Função SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Definir um atributo de instrução|[Função SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)
