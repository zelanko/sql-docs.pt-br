---
title: sp_cursorfetch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 66343bef328a2194ed825152b64a7a9ba600d707
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spcursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Busca um buffer de uma ou mais linhas no banco de dados. O grupo de linhas nesse buffer é chamado do cursor *buffer de busca*. sp_cursorfetch é invocado pela especificação de ID = 7 em um pacote de protocolo TDS de dados tabulares.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um *tratar* valor gerado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e retornado por sp_cursoropen. *cursor* é um parâmetro obrigatório que chama uma **int** valor de entrada. Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 *fetchType*  
 Especifica o buffer de cursor a ser buscado. *fetchType* é um parâmetro opcional que requer um dos seguintes valores de entrada de número inteiro.  
  
|Value|Nome|Description|  
|-----------|----------|-----------------|  
|0x0001|FIRST|Busca o primeiro buffer de *nrows* linhas. Se *nrows* é igual a 0, o cursor é posicionado antes do conjunto de resultados e nenhuma linha será retornada.|  
|0x0002|NEXT|Busca o próximo buffer de *nrows* linhas.|  
|0x0004|PREV|Busca o buffer anterior de *nrows* linhas.<br /><br /> Observação: Usar PREV para um cursor FORWARD_ONLY retorna uma mensagem de erro, pois FORWARD_ONLY oferece suporte apenas à rolagem em uma única direção.|  
|0x0008|LAST|Busca o último buffer de *nrows* linhas. Se *nrows* é igual a 0, o cursor é posicionado após o conjunto de resultados e nenhuma linha será retornada.<br /><br /> Observação: O uso de LAST para um cursor FORWARD_ONLY retorna uma mensagem de erro, pois FORWARD_ONLY oferece suporte apenas à rolagem em uma única direção.|  
|0x10|ABSOLUTE|Busca um buffer de *nrows* linhas começando com o *rownum* linha.<br /><br /> Observação: O uso de ABSOLUTE para um cursor dinâmico ou um cursor FORWARD_ONLY retorna uma mensagem de erro pois FORWARD_ONLY oferece suporte apenas à rolagem em uma única direção.|  
|0x20|RELATIVE|Busca o buffer de *nrows* linhas começando com a linha que é especificada como sendo o *rownum* valor das linhas da primeira linha no bloco atual. Nesse caso *rownum* pode ser um número negativo.<br /><br /> Observação: O uso de RELATIVE para um cursor FORWARD_ONLY retorna uma mensagem de erro pois FORWARD_ONLY oferece suporte apenas à rolagem em uma direção.|  
|0x80|REFRESH|Torna a encher o buffer a partir de tabelas subjacentes.|  
|0x100|INFO|Recupera informações sobre o cursor. Essas informações são retornadas usando o *rownum* e *nrows* parâmetros. Portanto, quando INFO é especificado, *rownum* e *nrows* se tornam parâmetros de saída.|  
|0x200|PREV_NOADJUST|É usado como PREV. Porém, se a parte superior do conjunto de resultados for encontrada prematuramente, os resultados poderão variar.|  
|0x400|SKIP_UPDT_CNCY|Deve ser usado com um dos outros *fetchtype* valores, com exceção de INFO.|  
  
> [!NOTE]  
>  Não há suporte para o valor 0x40.  
  
 Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 *rowNum*  
 É um parâmetro opcional que é usado para especificar a posição de linha para o ABSOLUTE e INFO *fetchtype* valores usando somente valores inteiros para entrada ou saída ou ambos. *rowNum* serve como o deslocamento da linha para o *fetchtype* valor relativo de bit. *rowNum* é ignorado para todos os outros valores. Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 *nrows*  
 É um parâmetro opcional usado para especificar o número de linhas a serem buscadas. Se *nrows* não for especificado, o valor padrão é 20 linhas. Para definir a posição sem retornar dados, especifique um valor de 0. Quando *nrows* é aplicada para o *fetchtype* consulta INFO, ele retorna o número total de linhas na consulta.  
  
> [!NOTE]  
>  *nrows* é ignorada pela atualização *fetchtype* valor de bit.  
>   
>  Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Quando você especificar o valor de bit INFO, os valores que podem ser retornados são mostrados nas tabelas a seguir.  
  
> [!NOTE]  
>  : Se nenhuma linha será retornada, o conteúdo do buffer permanece como estavam.  
  
|*\<rowNum >*|Definir como|  
|------------------|------------|  
|Se não abrir|0|  
|Se posicionado antes do conjunto de resultados|0|  
|Se posicionado após o conjunto de resultados|-1|  
|Para cursores KEYSET e STATIC|O número de linha absoluto da posição atual no conjunto de resultados|  
|Para cursores DYNAMIC|1|  
|Para ABSOLUTE|-1 retorna a última linha de um conjunto.<br /><br /> -2 retorna da segunda à última linha de um conjunto, e assim por diante.<br /><br /> Observação: Se mais de uma linha for solicitada a ser buscada neste caso, as duas últimas linhas do conjunto de resultados são retornadas.|  
  
|*\<nrows >*|Definir como|  
|-----------------|------------|  
|Se não abrir|0|  
|Para cursores KEYSET e STATIC|Normalmente, o tamanho do conjunto de chaves atual.<br /><br /> **– m** se o cursor estiver em criação assíncrona com *m* linhas encontradas para este ponto.|  
|Para cursores DYNAMIC|-1|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="cursor-parameter"></a>Parâmetro cursor  
 Antes de haver qualquer operação de busca, a posição padrão de um cursor é antes da primeira linha do conjunto de resultados.  
  
## <a name="fetchtype-parameter"></a>Parâmetro fetchtype  
 Com exceção de SKIP_UPD_CNCY, o *fetchtype* valores são mutuamente exclusivos.  
  
 Quando SKIP_UPDT_CNCY é especificado, os valores da coluna de carimbo de data/hora não são gravados na tabela de conjuntos de chaves quando uma linha é buscada ou atualizada. Se a linha de conjunto de chaves estiver sendo atualizada, os valores das colunas de carimbo de data/hora permanecerão como o valor anterior. Se a linha de conjunto de linhas estiver sendo inserida, os valores das colunas de carimbo de data/hora serão indefinidos.  
  
 Para cursores KEYSET, isso significa que a tabela de conjuntos de chaves tem os valores definidos durante o último FETCH sem salto, caso um seja realizado. Caso contrário, terá os valores definidos durante a população.  
  
 Para cursores DYNAMIC, isso significa que se o salto for executado com uma atualização, gerará os mesmos resultados que KEYSET. Para qualquer outro tipo de busca, uma tabela de conjuntos de chaves truncada. Isso significa que as linhas estão sendo inseridas e os valores da(s) colunas de carimbo de data/hora são indefinidos. Portanto, quando você executar sp_cursorfetch para cursores DYNAMIC, evite usar SKIP_UPDT_CNCY para qualquer operação que não seja REFRESH.  
  
 Se uma operação de busca falhar porque a posição do cursor solicitado está além do conjunto de resultados, a posição do cursor será definida para logo após a última linha. Se uma operação de busca falhar porque a posição do cursor solicitado está antes do conjunto de resultados, a posição do cursor será definida para antes da primeira linha.  
  
## <a name="rownum-parameter"></a>Parâmetro rownum  
 Quando você usa *rownum*, o buffer será preenchido a partir da linha especificada.  
  
 O *fetchtype* valor ABSOLUTO refere-se à posição de *rownum* em todo o resultado definido. Um número negativo com ABSOLUTE especifica que a operação conta linhas a partir do final do conjunto de resultados.  
  
 O *fetchtype* valor RELATIVE refere-se à posição de *rownum* em relação à posição do cursor no início do buffer atual. Um número negativo com RELATIVE especifica que o cursor retroceda a partir da posição atual.  
  
## <a name="nrows-parameter"></a>Parâmetro nrows  
 O *fetchtype* valores REFRESH e INFO ignoram esse parâmetro.  
  
 Quando você especifica um *fetchtype* valor First com um *nrow* valor de 0, o cursor é posicionado antes do conjunto de resultados que não tem nenhuma linha no buffer de busca.  
  
 Quando você especifica um *fetchtype* valor do último que tem um *nrow* valor de 0, o cursor é posicionado após o conjunto de resultados que não tem nenhuma linha no buffer de busca atual.  
  
 Para o *fetchtype* valores de NEXT, PREV, ABSOLUTO, relativo e PREV_NOADJUST, um *nrow* valor 0 não é válido.  
  
## <a name="rpc-considerations"></a>Considerações sobre RPC:  
 O status de retorno RPC indica se o parâmetro de tamanho de conjunto de chaves é final ou não, ou seja, se a tabela de conjuntos de chaves ou temporária está sendo populada de forma assíncrona.  
  
 O parâmetro de status RPC é definido como um dos valores mostrados na tabela a seguir.  
  
|Value|Descrição|  
|-----------|-----------------|  
|0|Procedimento executado com êxito.|  
|0x0001|Falha no procedimento.|  
|0x0002|Uma busca em uma direção negativa fez com que a posição do cursor fosse definida no início do conjunto de resultados, quando a busca logicamente teria sido antes dos resultados.|  
|0x10|Um cursor de avanço foi fechado automaticamente.|  
  
 As linhas são retornadas como um conjunto de resultados comum, ou seja, formato de coluna (0x2a), linhas (0xd1), seguidas de Done (0xfd). Tokens de metadados são enviados no mesmo formato que o especificado para sp_cursoropen, ou seja, 0x81, 0xa5 e 0xa4 para usuários do SQL Server 7.0, e assim por diante. Os indicadores de status de linha são enviados como colunas ocultas, semelhante ao modo BROWSE, ao final de cada linha com o nome de coluna rowstat e o tipo de dados INT4. Essa coluna rowstat tem um dos valores mostrados na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 Como o protocolo TDS não oferece nenhuma forma de enviar a coluna de status à direita sem enviar as colunas anteriores, são enviados dados fictícios para linhas ausentes (campos que permitem valor nulo definidos como nulos, campos de comprimento fixo definidos como 0, em branco ou o padrão para aquela coluna, conforme apropriado).  
  
 A contagem de linhas DONE sempre será zero. A mensagem DONE contém a contagem de linhas do conjunto de resultados real, e mensagens de erro ou informativas poderão aparecer entre quaisquer mensagens TDS.  
  
 Para solicitar que os metadados sobre a lista de seleção do cursor sejam retornados no fluxo TDS, defina o sinalizador de entrada RPC RETURN_METADATA como 1.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. Usando PREV para alterar uma posição de cursor  
 Suponha que um cursor h2 gerasse um conjunto de resultados com o conteúdo a seguir com uma posição atual conforme é mostrado:  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 Em seguida, um sp_cursorfetch PREV com um *nrows* valor 5 logicamente posicionaria o cursor duas linhas antes da primeira linha do conjunto de resultados. Nesses casos, o cursor é ajustado para iniciar na primeira linha e retornar o número de linhas solicitado. Em geral, isso significa que ele retornará linhas que estavam no buffer de busca PRIOR.  
  
> [!NOTE]  
>  Esse é o caso exato em que o parâmetro de status RPC é definido como 2.  
  
### <a name="b-using-prevnoadjust-to-return-fewer-rows-than-prev"></a>B. Usando PREV_NOADJUST para retornar menos linhas que PREV  
 PREV_NOADJUST nunca inclui nenhuma das linhas na posição do cursor atual, ou após, no bloco de linhas que retorna. Em casos em que PREV retorna linhas após a posição atual, PREV_NOADJUST retorna menos linhas do que o solicitado no *nrows*. Dada a posição atual no exemplo A anterior, quando PREV é aplicado, sp_cursorfetch (h2, 4, 1, 5) busca as seguintes linhas:  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 No entanto, quando PREV_NOADJUST é aplicado, sp_cursorfetch (h2, 512, 6, 5) busca somente as seguintes linhas:  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
