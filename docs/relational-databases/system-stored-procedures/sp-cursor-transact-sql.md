---
title: sp_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a92b502368756fd86fc4facda7c0726260d88fea
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85869687"
---
# <a name="sp_cursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Solicita atualizações posicionadas. Este procedimento executa operações em uma ou mais linhas no buffer de busca de um cursor. sp_cursor é invocado especificando ID = 1 em um pacote TDS (tabela de dados tabulares).  
  
||  
|-|  
|**Aplica-se a**: SQL Server ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio da [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 O identificador do cursor. *cursor* é um parâmetro necessário que chama um valor de entrada **int** . *cursor* é o valor do *identificador* gerado por SQL Server e retornado pelo procedimento sp_cursoropen.  
  
 *OpType*  
 É um parâmetro necessário que designa qual operação o cursor executará. *OpType* requer um dos valores de entrada **int** a seguir.  
  
|Valor|Nome|Descrição|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|É usado para atualizar uma ou mais linhas no buffer de busca.  As linhas especificadas em *rownum* são acessadas novamente e atualizadas.|  
|0x0002|Delete (excluir)|É usado para excluir uma ou mais linhas no buffer de busca. As linhas especificadas em *rownum* são acessadas novamente e excluídas.|  
|0X0004|INSERT|Insere dados sem criar uma instrução SQL **Insert** .|  
|0X0008|REFRESH|É usado para preencher novamente o buffer a partir de tabelas subjacentes e pode ser usado para atualizar a linha se uma atualização ou exclusão falhar devido a controle de simultaneidade otimista, ou após UPDATE.|  
|0X10|LOCK|Faz com que um SQL Server bloqueio de U seja adquirido na página que contém a linha especificada. Esse bloqueio é compatível com Bloqueios S, mas não com Bloqueios X ou outros Bloqueios U. Pode ser usado para implementar bloqueio a curto prazo.|  
|0X20|SETPOSITION|É usado somente quando o programa vai emitir um subseqüente SQL Server a instrução DELETE ou UPDATE posicionada.|  
|0X40|ABSOLUTE|Pode ser usado apenas junto com UPDATE ou DELETE.  ABSOLUTE é usado apenas com cursores KEYSET (é ignorado para cursores DYNAMIC e cursores STATIC não podem ser atualizados).<br /><br /> Observação: se ABSOLUTE for especificado em uma linha no conjunto de chaves que não foi buscada, a operação poderá falhar na verificação de simultaneidade e o resultado de retorno não poderá ser garantido.|  
  
 *rownum*  
 Especifica qual das linhas no buffer de busca o cursor irá afetar, atualizar ou excluir.  
  
> [!NOTE]  
>  Isso não afeta o ponto de partida de qualquer operação de busca RELATIVE, NEXT ou PREVIOUS, nem as atualizações ou exclusões executadas com sp_cursor.  
  
 *rownum* é um parâmetro necessário que chama um valor de entrada **int** .  
  
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
>  Só é válido para uso com valores de UPDATE, DELETE, REFRESH ou LOCK *OpType* .  
  
 *table*  
 O nome da tabela que identifica a tabela à qual *OpType* se aplica quando a definição do cursor envolve uma junção ou nomes de coluna ambíguos são retornados pelo parâmetro de *valor* . Se nenhuma tabela específica for designada, o padrão será a primeira tabela da cláusula FROM. *Table* é um parâmetro opcional que requer um valor de entrada de cadeia de caracteres. É possível especificar a cadeia de caracteres como qualquer tipo de dados de caractere ou UNICODE. a *tabela* pode ser um nome de tabela de várias partes.  
  
 *value*  
 Usado inserir ou atualizar valores. O parâmetro de cadeia de caracteres *Value* é usado somente com os valores Update e Insert *OpType* . É possível especificar a cadeia de caracteres como qualquer tipo de dados de caractere ou UNICODE.  
  
> [!NOTE]  
>  Os nomes de parâmetro para o *valor* podem ser atribuídos pelo usuário.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Ao usar um RPC, uma operação de exclusão ou atualização posicionada com um número de buffer 0 retornará uma mensagem feita com um *RowCount* de 0 (falha) ou 1 (êxito) para cada linha no buffer de busca.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="optype-parameter"></a>Parâmetro optype  
 Exceção das combinações de SETPOSITION com atualização, exclusão, atualização ou bloqueio; ou absoluto com UPDATE ou DELETE, os valores de *OpType* são mutuamente exclusivos.  
  
 A cláusula SET do valor de atualização é construída a partir do parâmetro *Value* .  
  
 Um benefício de usar o valor de INSERT *OpType* é que você pode evitar a conversão de dados de não caractere em formato de caractere para inserções. Os valores são especificados da mesma maneira como UPDATE. Se qualquer coluna obrigatório não for incluída, INSERT falhará.  
  
-   O valor SETPOSITION não afeta o ponto de partida de qualquer operação de busca RELATIVE, NEXT ou PREVIOUS, nem as atualizações ou exclusões executadas com a interface sp_cursor. Qualquer número que não especificar uma linha no buffer de busca resultará na posição sendo definida como 1 sem erro sendo retornado. Depois que SETPOSITION é executada, a posição permanece em vigor até a próxima operação de sp_cursorfetch, a operação de **busca** do T-SQL ou sp_cursor operação SETPOSITION por meio do mesmo cursor. Uma operação sp_cursorfetch subsequente definirá a posição do cursor como a primeira linha no novo buffer de busca, enquanto outras chamadas de cursor não afetarão o valor da posição. SETPOSITION pode ser vinculado por uma cláusula OR com REFRESH, UPDATE, DELETE ou LOCK para definir o valor da posição como a última linha modificada.  
  
 Se uma linha no buffer de busca não for especificada por meio do parâmetro *rownum* , a posição será definida como 1, sem nenhum erro retornado. Uma vez que a posição seja definida, ela permanecerá em vigor até a próxima operação sp_cursorfetch, operação T-SQL ou operação SETPOSITION sp_cursor ser executada no mesmo cursor.  
  
 SETPOSITION pode ser vinculado por uma cláusula OR com REFRESH, UPDATE, DELETE ou LOCK para definir a posição do cursor como a última linha modificada.  
  
## <a name="rownum-parameter"></a>Parâmetro rownum  
 Se especificado, o parâmetro *rownum* poderá ser interpretado como o número da linha dentro do conjunto de chaves, em vez do número da linha dentro do buffer de busca. O usuário é responsável para assegurar que o controle de simultaneidade seja mantido. Isso significa que, para cursores SCROLL_LOCKS, você deve manter um bloqueio de forma independente na linha determinada (isso pode ser feito por meio de uma transação). Para cursores OPTIMISTIC, você deve ter buscado previamente a linha para executar essa operação.  
  
## <a name="table-parameter"></a>Parâmetro table  
 Se o valor de *OpType* for Update ou INSERT e uma instrução UPDATE ou INSERT completa for enviada como o parâmetro *Value* , o valor especificado para *Table* será ignorado.  
  
> [!NOTE]  
>  Com relação a exibições, somente uma tabela participante da exibição pode ser modificada. Os nomes de coluna de parâmetro de *valor* devem refletir os nomes de coluna na exibição, mas o nome da tabela pode ser o da tabela base subjacente (nesse caso sp_cursor substituirá o nome da exibição).  
  
## <a name="value-parameter"></a>Parâmetro value  
 Há duas alternativas às regras para usar o *valor* , conforme mencionado anteriormente na seção argumentos:  
  
1.  Você pode usar um nome que seja ' \@ ' pre-pendente para o nome da coluna na lista de seleção para qualquer parâmetro de *valor* nomeado. Uma vantagem dessa alternativa é que a conversão de dados pode não ser necessária.  
  
2.  Use um parâmetro para enviar uma instrução UPDATE ou INSERT completa ou use vários parâmetros para enviar partes de uma instrução UPDATE ou INSERT que SQL Server, em seguida, será criada em uma instrução completa. Você encontrará exemplos disso na seção Exemplos, posteriormente neste tópico.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="alternative-value-parameter-uses"></a>Usos alternativos do parâmetro value  
 Para UPDATE:  
  
 Quando um único parâmetro é usado, uma instrução UPDATE pode ser enviada com a seguinte sintaxe:  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,...n]`  
  
> [!NOTE]  
>  Se UPDATE \<table name> for especificado, qualquer valor especificado para o parâmetro *Table* será ignorado.  
  
 Quando são usados vários parâmetros, o primeiro deve ser uma cadeia de caracteres no seguinte formato:  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 e os parâmetros subsequentes devem estar neste formato:  
  
 `<column name> = expression  [,...n]`  
  
 Nesse caso, o \<table name> na instrução UPDATE construída é aquele especificado ou padronizado pelo parâmetro *Table* .  
  
 Para INSERT:  
  
 Quando um único parâmetro é usado, uma instrução INSERT pode ser enviada com a seguinte sintaxe:  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  Se INSERT *\<table name>* for especificado, qualquer valor especificado para o parâmetro *Table* será ignorado.  
  
 Quando são usados vários parâmetros, o primeiro deve ser uma cadeia de caracteres no seguinte formato:  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 e os parâmetros subsequentes devem estar neste formato:  
  
 `expression [,...n]`  
  
 exceto onde VALUES foi especificado, quando deverá haver um ")" à direita após a última expressão. Nesse caso, o *\<table name>* na instrução UPDATE construída é aquele especificado ou padronizado pelo parâmetro *Table* .  
  
> [!NOTE]  
>  É possível enviar um parâmetro como um parâmetro nomeado, isto é, "`@VALUES`". Neste caso, nenhum outro parâmetro nomeado pode ser usado.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_cursoropen](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_cursorfetch](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
