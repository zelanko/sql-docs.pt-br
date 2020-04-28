---
title: sp_cursorfetch (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4635bffa5b5b681d0ff202c4231c4d8b8d10ae26
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108508"
---
# <a name="sp_cursorfetch-transact-sql"></a>sp_cursorfetch (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Busca um buffer de uma ou mais linhas no banco de dados. O grupo de linhas nesse buffer é chamado de *buffer de busca*do cursor. sp_cursorfetch é invocado especificando ID = 7 em um pacote TDS (tabela de dados tabulares).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 É um valor de *identificador* gerado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por e retornado por sp_cursoropen. *cursor* é um parâmetro necessário que chama um valor de entrada **int** . Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 *fetchtype*  
 Especifica o buffer de cursor a ser buscado. *fetchtype* é um parâmetro opcional que requer um dos seguintes valores de entrada de inteiro.  
  
|Valor|Nome|Descrição|  
|-----------|----------|-----------------|  
|0x0001|FIRST|Busca o primeiro buffer de linhas *nRows* . Se *nRows* for igual a 0, o cursor será posicionado antes do conjunto de resultados e nenhuma linha será retornada.|  
|0x0002|NEXT|Busca o próximo buffer de linhas *nRows* .|  
|0x0004|PREV|Busca o buffer anterior de linhas *nRows* .<br /><br /> Observação: usar anterior para um FORWARD_ONLY cursor retorna uma mensagem de erro porque FORWARD_ONLY dá suporte apenas à rolagem em uma direção.|  
|0x0008|LAST|Busca o último buffer de linhas *nRows* . Se *nRows* for igual a 0, o cursor será posicionado após o conjunto de resultados e nenhuma linha será retornada.<br /><br /> Observação: usar LAST para um FORWARD_ONLY cursor retorna uma mensagem de erro porque FORWARD_ONLY dá suporte apenas à rolagem em uma direção.|  
|0x10|ABSOLUTE|Busca um buffer de linhas *nRows* começando com a linha *rownum* .<br /><br /> Observação: usar ABSOLUTE para um cursor dinâmico ou um cursor de FORWARD_ONLY retorna uma mensagem de erro porque FORWARD_ONLY dá suporte apenas à rolagem em uma direção.|  
|0x20|RELATIVE|Busca o buffer de linhas *nRows* começando com a linha que é especificada como sendo o valor de *rownum* de linhas da primeira linha no bloco atual. Nesse caso, *rownum* pode ser um número negativo.<br /><br /> Observação: o uso de relativo para um FORWARD_ONLY cursor retorna uma mensagem de erro porque FORWARD_ONLY dá suporte apenas à rolagem em uma direção.|  
|0x80|REFRESH|Torna a encher o buffer a partir de tabelas subjacentes.|  
|0x100|INFO|Recupera informações sobre o cursor. Essas informações são retornadas usando os parâmetros *rownum* e *nRows* . Portanto, quando as informações são especificadas, *rownum* e *nRows* se tornam parâmetros de saída.|  
|0x200|PREV_NOADJUST|É usado como PREV. Porém, se a parte superior do conjunto de resultados for encontrada prematuramente, os resultados poderão variar.|  
|0x400|SKIP_UPDT_CNCY|Deve ser usado com um dos outros valores *fetchtype* , exceto para informações.|  
  
> [!NOTE]  
>  Não há suporte para o valor 0x40.  
  
 Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 *rownum*  
 É um parâmetro opcional que é usado para especificar a posição da linha para os valores absoluto e INFO *fetchtype* usando apenas valores inteiros para entrada ou saída, ou ambos. *rownum* serve como o deslocamento de linha para o valor de bit *fetchtype* relativo. *rownum* é ignorado para todos os outros valores. Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
 *nrows*  
 É um parâmetro opcional usado para especificar o número de linhas a serem buscadas. Se *nRows* não for especificado, o valor padrão será 20 linhas. Para definir a posição sem retornar os dados, especifique um valor de 0. Quando *nRows* é aplicado à consulta de informações *fetchtype* , ele retorna o número total de linhas nessa consulta.  
  
> [!NOTE]  
>  *nRows* é ignorado pelo valor de bit de *busca* de atualização.  
>   
>  Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Quando você especificar o valor de bit INFO, os valores que podem ser retornados são mostrados nas tabelas a seguir.  
  
> [!NOTE]  
>  :   Se nenhuma linha for retornada, os conteúdo do buffer permanecerá como era.  
  
|*\<>rownum*|Definir como|  
|------------------|------------|  
|Se não abrir|0|  
|Se posicionado antes do conjunto de resultados|0|  
|Se posicionado após o conjunto de resultados|-1|  
|Para cursores KEYSET e STATIC|O número de linha absoluto da posição atual no conjunto de resultados|  
|Para cursores DYNAMIC|1|  
|Para ABSOLUTE|-1 retorna a última linha de um conjunto.<br /><br /> -2 retorna da segunda à última linha de um conjunto, e assim por diante.<br /><br /> Observação: se mais de uma linha for solicitada para ser buscada nesse caso, as duas últimas linhas do conjunto de resultados serão retornadas.|  
  
|*\<>nRows*|Definir como|  
|-----------------|------------|  
|Se não abrir|0|  
|Para cursores KEYSET e STATIC|Normalmente, o tamanho do conjunto de chaves atual.<br /><br /> **-m** se o cursor estiver na criação assíncrona com *m* linhas encontradas para esse ponto.|  
|Para cursores DYNAMIC|-1|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="cursor-parameter"></a>Parâmetro cursor  
 Antes de haver qualquer operação de busca, a posição padrão de um cursor é antes da primeira linha do conjunto de resultados.  
  
## <a name="fetchtype-parameter"></a>Parâmetro fetchtype  
 Exceto para SKIP_UPD_CNCY, os valores *fetchtype* são mutuamente exclusivos.  
  
 Quando SKIP_UPDT_CNCY é especificado, os valores da coluna de carimbo de data/hora não são gravados na tabela de conjuntos de chaves quando uma linha é buscada ou atualizada. Se a linha de conjunto de chaves estiver sendo atualizada, os valores das colunas de carimbo de data/hora permanecerão como o valor anterior. Se a linha de conjunto de linhas estiver sendo inserida, os valores das colunas de carimbo de data/hora serão indefinidos.  
  
 Para cursores KEYSET, isso significa que a tabela de conjuntos de chaves tem os valores definidos durante o último FETCH sem salto, caso um seja realizado. Caso contrário, terá os valores definidos durante a população.  
  
 Para cursores DYNAMIC, isso significa que se o salto for executado com uma atualização, gerará os mesmos resultados que KEYSET. Para qualquer outro tipo de busca, uma tabela de conjuntos de chaves truncada. Isso significa que as linhas estão sendo inseridas e os valores da(s) colunas de carimbo de data/hora são indefinidos. Portanto, quando você executar sp_cursorfetch para cursores DYNAMIC, evite usar SKIP_UPDT_CNCY para qualquer operação que não seja REFRESH.  
  
 Se uma operação de busca falhar porque a posição do cursor solicitado está além do conjunto de resultados, a posição do cursor será definida para logo após a última linha. Se uma operação de busca falhar porque a posição do cursor solicitado está antes do conjunto de resultados, a posição do cursor será definida para antes da primeira linha.  
  
## <a name="rownum-parameter"></a>Parâmetro rownum  
 Quando você usa *rownum*, o buffer é preenchido começando com a linha especificada.  
  
 O valor de *fetchtype* absoluto refere-se à posição de *rownum* em todo o conjunto de resultados. Um número negativo com ABSOLUTE especifica que a operação conta linhas a partir do final do conjunto de resultados.  
  
 O valor de *fetchtype* relativo refere-se à posição de *rownum* em relação à posição do cursor no início do buffer atual. Um número negativo com RELATIVE especifica que o cursor retroceda a partir da posição atual.  
  
## <a name="nrows-parameter"></a>Parâmetro nrows  
 Os valores *fetchtype* atualizar e informações ignoram esse parâmetro.  
  
 Quando você especifica um valor *fetchtype* de First que tem um valor de *nrow* de 0, o cursor é posicionado antes do conjunto de resultados que não tem nenhuma linha no buffer de busca.  
  
 Quando você especifica um valor de *fetchtype* de Last que tem um valor de *nrow* de 0, o cursor é posicionado após o conjunto de resultados que não tem linhas no buffer de busca atual.  
  
 Para os valores *fetchtype* de Next, anterior, Absolute, RELATIVE e PREV_NOADJUST, um valor de *nrow* de 0 não é válido.  
  
## <a name="rpc-considerations"></a>Considerações sobre RPC:  
 O status de retorno RPC indica se o parâmetro de tamanho de conjunto de chaves é final ou não, ou seja, se a tabela de conjuntos de chaves ou temporária está sendo populada de forma assíncrona.  
  
 O parâmetro de status RPC é definido como um dos valores mostrados na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|Procedimento executado com êxito.|  
|0x0001|Falha no procedimento.|  
|0x0002|Uma busca em uma direção negativa fez com que a posição do cursor fosse definida no início do conjunto de resultados, quando a busca logicamente teria sido antes dos resultados.|  
|0x10|Um cursor de avanço rápido foi fechado automaticamente.|  
  
 As linhas são retornadas como um conjunto de resultados comum, ou seja, formato de coluna (0x2a), linhas (0xd1), seguidas de Done (0xfd). Tokens de metadados são enviados no mesmo formato que o especificado para sp_cursoropen, ou seja, 0x81, 0xa5 e 0xa4 para usuários do SQL Server 7.0, e assim por diante. Os indicadores de status de linha são enviados como colunas ocultas, semelhante ao modo BROWSE, ao final de cada linha com o nome de coluna rowstat e o tipo de dados INT4. Essa coluna rowstat tem um dos valores mostrados na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 Como o protocolo TDS não oferece nenhuma forma de enviar a coluna de status à direita sem enviar as colunas anteriores, são enviados dados fictícios para linhas ausentes (campos que permitem valor nulo definidos como nulos, campos de comprimento fixo definidos como 0, em branco ou o padrão para aquela coluna, conforme apropriado).  
  
 A contagem de linhas DONE sempre será zero. A mensagem DONE contém a contagem de linhas do conjunto de resultados real, e mensagens de erro ou informativas poderão aparecer entre quaisquer mensagens TDS.  
  
 Para solicitar que os metadados sobre a lista de seleção do cursor sejam retornados no fluxo TDS, defina o sinalizador de entrada RPC RETURN_METADATA como 1.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>a. Usando PREV para alterar uma posição de cursor  
 Suponha que um cursor h2 gerasse um conjunto de resultados com o conteúdo a seguir com uma posição atual conforme é mostrado:  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 Em seguida, um sp_cursorfetch anterior que tem um valor de *nRows* de 5 posicionaria logicamente as duas linhas do cursor antes da primeira linha do conjunto de resultados. Nesses casos, o cursor é ajustado para iniciar na primeira linha e retornar o número de linhas solicitado. Em geral, isso significa que ele retornará linhas que estavam no buffer de busca PRIOR.  
  
> [!NOTE]  
>  Esse é o caso exato em que o parâmetro de status RPC é definido como 2.  
  
### <a name="b-using-prev_noadjust-to-return-fewer-rows-than-prev"></a>B. Usando PREV_NOADJUST para retornar menos linhas que PREV  
 PREV_NOADJUST nunca inclui nenhuma das linhas na posição do cursor atual, ou após, no bloco de linhas que retorna. Nos casos em que o anterior retorna linhas após a posição atual, PREV_NOADJUST retorna menos linhas do que o solicitado em *nRows*. Dada a posição atual no Exemplo A anterior, quando PREV é aplicado, sp_cursorfetch (h2, 4, 1, 5) busca as seguintes linhas:  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 Porém, quando PREV_NOADJUST é aplicado, sp_cursorfetch (h2, 512, 6, 5) busca somente as seguintes linhas:  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cursoropen](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
