---
title: sp_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 36e188370f32702544ccef4b18d0398e5c8fddfd
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Solicita atualizações posicionadas. Este procedimento executa operações em uma ou mais linhas no buffer de busca de um cursor. sp_cursor é invocado pela especificação de ID = 1 em um pacote de protocolo TDS de dados tabulares.  
  
||  
|-|  
|**Aplica-se a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 O identificador do cursor. *cursor* é um parâmetro obrigatório que chama uma **int** valor de entrada. *cursor* é o *tratar* valor gerado pelo SQL Server e retornado pelo procedimento sp_cursoropen.  
  
 *optype*  
 É um parâmetro necessário que designa qual operação o cursor executará. *optype* requer um dos seguintes **int** valores de entrada.  
  
|Value|Nome|Description|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|É usado para atualizar uma ou mais linhas no buffer de busca.  As linhas especificadas em *rownum* são novamente acessadas e atualizadas.|  
|0x0002|DELETE|É usado para excluir uma ou mais linhas no buffer de busca. As linhas especificadas em *rownum* são novamente acessadas e excluídas.|  
|0X0004|INSERT|Insere dados sem criar um SQL **inserir** instrução.|  
|0X0008|REFRESH|É usado para preencher novamente o buffer a partir de tabelas subjacentes e pode ser usado para atualizar a linha se uma atualização ou exclusão falhar devido a controle de simultaneidade otimista, ou após UPDATE.|  
|0X10|LOCK|Faz com que um SQL Server U bloqueio adquirido na página que contém a linha especificada. Esse bloqueio é compatível com Bloqueios S, mas não com Bloqueios X ou outros Bloqueios U. Pode ser usado para implementar bloqueio a curto prazo.|  
|0X20|SETPOSITION|É usado somente quando o programa for emitir um SQL Server subsequentes posicionado instrução DELETE ou UPDATE.|  
|0X40|ABSOLUTE|Pode ser usado apenas junto com UPDATE ou DELETE.  ABSOLUTE é usado apenas com cursores KEYSET (é ignorado para cursores DYNAMIC e cursores STATIC não podem ser atualizados).<br /><br /> Observação: Se ABSOLUTE é especificado em uma linha no conjunto de chaves que não tiverem sido buscado, a operação poderá falhar na verificação de simultaneidade e o resultado de retorno não pode ser garantido.|  
  
 *rowNum*  
 Especifica qual das linhas no buffer de busca o cursor irá afetar, atualizar ou excluir.  
  
> [!NOTE]  
>  Isso não afeta o ponto de partida de qualquer operação de busca RELATIVE, NEXT ou PREVIOUS, nem as atualizações ou exclusões executadas com sp_cursor.  
  
 *rowNum* é um parâmetro obrigatório que chama uma **int** valor de entrada.  
  
 1  
 Significa a primeira linha no buffer de busca.  
  
 2  
 Significa a segunda linha no buffer de busca.  
  
 3, 4, 5  
 Significa a terceira linha, e assim por diante.  
  
 n  
 Significa a enésima linha no buffer de busca.  
  
 0  
 Significa todas as linhas no buffer de busca.  
  
> [!NOTE]  
>  Só é válida para uso com a atualização, exclusão, atualização ou bloqueio *optype* valores.  
  
 *table*  
 Nome da tabela que identifica a tabela que *optype* aplica-se quando a definição de cursor envolve uma junção ou nomes de coluna ambíguos são retornados pelo *valor* parâmetro. Se nenhuma tabela específica for designada, o padrão será a primeira tabela da cláusula FROM. *tabela* é um parâmetro opcional que requer um valor de cadeia de caracteres de entrada. É possível especificar a cadeia de caracteres como qualquer tipo de dados de caractere ou UNICODE. *tabela* pode ser um nome de tabela de várias partes.  
  
 *value*  
 Usado inserir ou atualizar valores. O *valor* parâmetro de cadeia de caracteres é usado apenas com UPDATE e INSERT *optype* valores. É possível especificar a cadeia de caracteres como qualquer tipo de dados de caractere ou UNICODE.  
  
> [!NOTE]  
>  Os nomes de parâmetro para *valor* podem ser atribuídos pelo usuário.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Ao usar uma RPC, uma operação posicionada DELETE ou UPDATE com um número de buffer 0 retornará uma mensagem DONE com um *rowcount* 0 (falha) ou 1 (êxito) para cada linha no buffer de busca.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="optype-parameter"></a>Parâmetro optype  
 Com exceção das combinações de SETPOSITION com UPDATE, DELETE, atualização ou bloqueio; ou ABSOLUTO com UPDATE ou DELETE, o *optype* valores são mutuamente exclusivos.  
  
 A cláusula SET do valor UPDATE é construída a partir de *valor* parâmetro.  
  
 Uma vantagem de usar a inserção *optype* valor é que você pode evitar a conversão de dados de caractere não em formato de caractere para inserções. Os valores são especificados da mesma maneira como UPDATE. Se qualquer coluna obrigatório não for incluída, INSERT falhará.  
  
-   O valor SETPOSITION não afeta o ponto de partida de qualquer operação de busca RELATIVE, NEXT ou PREVIOUS, nem as atualizações ou exclusões executadas com a interface sp_cursor. Qualquer número que não especificar uma linha no buffer de busca resultará na posição sendo definida como 1 sem erro sendo retornado. Quando SETPOSITION for executado, a posição permanecerá em vigor até a próxima operação sp_cursorfetch, T-SQL **BUSCAR** operação ou operação SETPOSITION sp_cursor pelo mesmo cursor. Uma operação sp_cursorfetch subsequente definirá a posição do cursor como a primeira linha no novo buffer de busca, enquanto outras chamadas de cursor não afetarão o valor da posição. SETPOSITION pode ser vinculado por uma cláusula OR com REFRESH, UPDATE, DELETE ou LOCK para definir o valor da posição como a última linha modificada.  
  
 Se uma linha no buffer de busca não for especificada por meio de *rownum* parâmetro, a posição será definida como 1, nenhum erro retornado. Uma vez que a posição seja definida, ela permanecerá em vigor até a próxima operação sp_cursorfetch, operação T-SQL ou operação SETPOSITION sp_cursor ser executada no mesmo cursor.  
  
 SETPOSITION pode ser vinculado por uma cláusula OR com REFRESH, UPDATE, DELETE ou LOCK para definir a posição do cursor como a última linha modificada.  
  
## <a name="rownum-parameter"></a>Parâmetro rownum  
 Se especificado, o *rownum* parâmetro pode ser interpretado como o número da linha no conjunto de chaves em vez do número de linha no buffer de busca. O usuário é responsável para assegurar que o controle de simultaneidade seja mantido. Isso significa que, para cursores SCROLL_LOCKS, você deve manter um bloqueio de forma independente na linha determinada (isso pode ser feito por meio de uma transação). Para cursores OPTIMISTIC, você deve ter buscado previamente a linha para executar essa operação.  
  
## <a name="table-parameter"></a>Parâmetro table  
 Se o *optype* valor for UPDATE ou INSERT e uma instrução de inserção ou atualização completa é enviada como o *valor* parâmetro, o valor especificado para *tabela* será ignorado.  
  
> [!NOTE]  
>  Com relação a exibições, somente uma tabela participante da exibição pode ser modificada. O *valor* nomes de coluna de parâmetro devem refletir os nomes de coluna no modo de exibição, mas o nome da tabela pode ser que a tabela base subjacente (caso em que sp_cursor substituirá o nome de exibição).  
  
## <a name="value-parameter"></a>Parâmetro value  
 Há duas alternativas para as regras para usar *valor* conforme mencionado anteriormente na seção argumentos:  
  
1.  Você pode usar um nome que seja ' @' anexado ao nome da coluna na lista de seleção para qualquer chamada *valor* parâmetros. Uma vantagem dessa alternativa é que a conversão de dados pode não ser necessária.  
  
2.  Use um parâmetro para enviar uma instrução UPDATE ou INSERT completa ou usar vários parâmetros para enviar partes de uma instrução UPDATE ou INSERT que o SQL Server criará em uma instrução completa. Você encontrará exemplos disso na seção Exemplos, posteriormente neste tópico.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="alternative-value-parameter-uses"></a>Usos alternativos do parâmetro value  
 Para UPDATE:  
  
 Quando um único parâmetro é usado, uma instrução UPDATE pode ser enviada com a seguinte sintaxe:  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,…n]`  
  
> [!NOTE]  
>  Se UPDATE \<nome da tabela > for especificado, qualquer valor especificado para o *tabela* parâmetro será ignorado.  
  
 Quando são usados vários parâmetros, o primeiro deve ser uma cadeia de caracteres no seguinte formato:  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 e os parâmetros subsequentes devem estar neste formato:  
  
 `<column name> = expression  [,...n]`  
  
 Nesse caso, o \<nome da tabela > na atualização construída instrução é aquele especificado ou usado como padrão pelo *tabela* parâmetro.  
  
 Para INSERT:  
  
 Quando um único parâmetro é usado, uma instrução INSERT pode ser enviada com a seguinte sintaxe:  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  Se inserir  *\<nome da tabela >* for especificado, qualquer valor especificado para o *tabela* parâmetro será ignorado.  
  
 Quando são usados vários parâmetros, o primeiro deve ser uma cadeia de caracteres no seguinte formato:  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 e os parâmetros subsequentes devem estar neste formato:  
  
 `expression [,...n]`  
  
 exceto onde VALUES foi especificado, quando deverá haver um ")" à direita após a última expressão. Nesse caso, o  *\<nome da tabela >* instrução Update construída é aquele especificado ou usado como padrão pelo *tabela* parâmetro.  
  
> [!NOTE]  
>  É possível enviar um parâmetro como um parâmetro nomeado, isto é, "`@VALUES`". Neste caso, nenhum outro parâmetro nomeado pode ser usado.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
