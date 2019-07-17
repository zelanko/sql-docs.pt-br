---
title: sp_cursoropen (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5127d041817a41dcf2d6fb4ed65070c87d05dd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108480"
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Abre um cursor. sp_cursoropen define a instrução SQL associada com o cursor e opções de cursor e, em seguida, popula o cursor. sp_cursoropen é equivalente à combinação da [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções DECLARE_CURSOR e OPEN. Esse procedimento é invocado pela especificação de ID = 2 em um pacote TDS.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor*  
 Um identificador de cursor gerado pelo SQL Server. *cursor* é um *manipular* valor deve ser fornecido em todos os procedimentos subsequentes relacionados ao cursor, por exemplo, sp_cursorfetch. *cursor* é um parâmetro obrigatório com um **int** valor de retorno.  
  
 *cursor* permite vários cursores ativos em uma conexão de banco de dados individual.  
  
 *stmt*  
 É um parâmetro obrigatório que define o conjunto de resultados do cursor. Qualquer cadeia de consulta válida (sintaxe e associação) de qualquer tipo de cadeia de caracteres (independentemente de Unicode, tamanho, etc.) pode servir como uma opção válida *stmt* tipo de valor.  
  
 *scrollopt*  
 Opção de rolagem. *scrollopt* é um parâmetro opcional que requer um dos seguintes **int** valores de entrada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 Devido à possibilidade de que o valor solicitado não é apropriado para o cursor definido por *stmt*, este parâmetro serve como entrada e saída. Nesses casos, o SQL Server atribui um valor apropriado.  
  
 *ccopt*  
 Opção de controle de simultaneidade. *ccopt* é um parâmetro opcional que requer um dos seguintes **int** valores de entrada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (anteriormente conhecido como LOCKCC)|  
|0x0004|**OTIMISTA** (anteriormente conhecido como OPTCC)|  
|0x0008|OPTIMISTIC (anteriormente conhecido como OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 Assim como acontece com *scrollopt*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode substituir o solicitada *ccopt* valores.  
  
 *rowcount*  
 O número de linhas do buffer de busca a serem usadas com AUTO_FETCH. O padrão é 20 linhas. *número de linhas* tem um comportamento diferente quando atribuído como um valor de entrada versus um valor de retorno.  
  
|Como valor de entrada|Como valor de retorno|  
|--------------------|---------------------|  
|Quando o AUTO_FETCH *scrollopt* valor for especificado *rowcount* representa o número de linhas a serem colocadas no buffer de busca.<br /><br /> Observação: > 0 é um valor válido quando AUTO_FETCH é especificado, mas é ignorado.|Representa o número de linhas no resultado definido, exceto quando o *scrollopt* valor AUTO_FETCH é especificado.|  
  
-  
  
 *boundparam*  
 Significa o uso de parâmetros adicionais. *boundparam* é um parâmetro opcional que deverá ser especificado se o *scrollopt* valor PARAMETERIZED_STMT for definida como ON.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Se nenhum erro ocorrer, sp_cursoropen retornará um dos valores a seguir.  
  
 0  
 O procedimento executado com êxito.  
  
 0x0001  
 Ocorreu um erro durante a execução (um erro secundário, não grave o bastante para gerar um erro na operação).  
  
 0x0002  
 Uma operação síncrona está em andamento.  
  
 0x0002  
 Uma operação FETCH está em andamento.  
  
 Um  
 Este cursor foi desalocado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não está disponível.  
  
 Quando um erro ocorrer, os valores de retorno poderão estar inconsistentes e a exatidão não pode ser garantida.  
  
 Quando o *rowcount* parâmetro for especificado como um valor de retorno, ocorre o seguinte conjunto de resultados.  
  
 -1  
 Retornado se o número de linhas for desconhecido ou não aplicável.  
  
 -n  
 Retornado quando uma população assíncrona está em vigor. Representa o número de linhas que foram colocados em busca de buffer quando o *scrollopt* valor AUTO_FETCH é especificado.  
  
 Se o RPC estiver em uso, os valores de retorno serão como se segue.  
  
 0  
 Procedimento bem-sucedido.  
  
 1  
 Falha no procedimento.  
  
 2  
 Um cursor de conjunto de chaves está sendo gerado de forma assíncrona.  
  
 16  
 Um cursor de avanço foi fechado automaticamente.  
  
> [!NOTE]  
>  Se o procedimento sp_cursoropen for executado com êxito, o RPC retornar parâmetros e um conjunto de resultados com informações de formato de coluna TDS (0xa0 e 0xa1 mensagens) são enviadas. Caso contrário, uma ou mais mensagens de erro TDS serão enviadas. Em ambos os casos, nenhum dado de linha será retornado e o *feito* contagem de mensagens será zero. Se você estiver usando uma versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anterior à 7.0, 0xa0 e 0xa1 (padrão para instruções SELECT) serão retornadas junto com os fluxos de token 0xa5 e 0xa4. Se você estiver usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, 0x81 será retornado (padrão para instruções SELECT) junto com os fluxos de token 0xa5 e 0xa4.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="stmt-parameter"></a>Parâmetro stmt  
 Se *stmt* Especifica a execução de um procedimento armazenado, os parâmetros de entrada poderão ser definidos como constantes como parte do *stmt* cadeia de caracteres ou especificado como *boundparam* argumentos. Variáveis declaradas podem ser passadas como parâmetros associados dessa forma.  
  
 Os conteúdo permitido do *stmt* parâmetro dependem se deseja ou não a *ccopt* ALLOW_DIRECT retornar valor tem sido vinculado por OR ao restante dos *ccopt* valores, ou seja:  
  
-   Se ALLOW_DIRECT não for especificado, ou um [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT ou EXECUTE a instrução de chamada para um procedimento armazenado que contém uma única instrução SELECT deve ser usado. Além disso, a instrução SELECT deve estar qualificada como um cursor; ou seja, ele não pode conter as palavras-chave SELECT INTO ou FOR BROWSE.  
  
-   Se ALLOW_DIRECT for especificado, isso poderá resultar em uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], inclusive aquelas que, por sua vez, executam outros procedimentos armazenados com várias instruções. As instruções diferentes de SELECT ou qualquer instrução SELECT que contenha as palavras-chave SELECT INTO ou FOR BROWSE serão simplesmente executadas e não resultarão na criação de um cursor. O mesmo ocorre para qualquer instrução SELECT incluída em um lote de várias instruções. Nos casos em que uma instrução SELECT contém cláusulas que só pertencem a cursores, essas cláusulas são ignoradas. Por exemplo, quando o valor de *ccopt* for 0x2002, essa é uma solicitação para:  
  
    -   Um cursor com bloqueios de rolagem, se houver somente uma única instrução SELECT qualificada como um cursor, ou  
  
    -   Uma execução de instrução direta se houver várias instruções, uma única instrução não SELECT ou uma instrução SELECT que não esteja qualificada como um cursor.  
  
## <a name="scrollopt-parameter"></a>Parâmetro scrollopt  
 Os primeiros cinco *scrollopt* valores (KEYSEY, DYNAMIC, FORWARD_ONLY, STATIC e FAST_FORWARD) são mutuamente exclusivos.  
  
 PARAMETERIZED_STMT e CHECK_ACCEPTED_TYPES podem ser vinculados por OR a qualquer um dos cinco primeiros valores.  
  
 AUTO_FETCH e AUTO_CLOSE podem ser vinculados por OR a FAST_FORWARD.  
  
 Se CHECK_ACCEPTED_TYPES for ON, pelo menos um dos últimos cinco *scrollopt* valores (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE, FORWARD_ONLY_ACCEPTABLE, STATIC_ACCEPTABLE ou FAST_FORWARD_ACCEPTABLE) também deverá ser ON.  
  
 Os cursores STATIC são sempre abertos como READ_ONLY. Isso significa que a tabela subjacente não pode ser atualizada por meio desse cursor.  
  
## <a name="ccopt-parameter"></a>Parâmetro ccopt  
 Os primeiros quatro *ccopt* valores (READ_ONLY, SCROLL_LOCKS e ambos os valores OPTIMISTIC) são mutuamente exclusivos.  
  
> [!NOTE]  
>  Escolhendo um dos quatro primeiros *ccopt* valores determina se o cursor é somente leitura ou se os métodos de bloqueio ou otimistas são usados para impedir atualizações perdidas. Se um *ccopt* valor não for especificado, o valor padrão será OPTIMISTIC.  
  
 ALLOW_DIRECT e CHECK_ACCEPTED_TYPES podem ser vinculados por OR a qualquer um dos quatro primeiros valores.  
  
 UPDT_IN_PLACE pode ser vinculado por OR a READ_ONLY, SCROLL_LOCKS ou qualquer um dos valores OPTIMISTIC.  
  
 Se CHECK_ACCEPTED_TYPES for ON, pelo menos um dos últimos quatro *ccopt* valores (READ_ONLY_ACCEPTABLE, SCROLL_LOCKS_ACCEPTABLE e qualquer um dos valores OPTIMISTIC_ACCEPTABLE) também deverá ser ON.  
  
 Funções UPDATE e DELETE posicionadas podem ser executadas apenas dentro do buffer de busca e somente se o *ccopt* valor é igual a SCROLL_LOCKS ou OPTIMISTIC. Se SCROLL_LOCKS for o valor especificado, a operação terá êxito garantido. Se OPTIMISTIC for o valor especificado, a operação falhará se a linha tiver sido alterada desde que foi buscada pela última vez.  
  
 O motivo dessa falha é que, quando OPTIMISTIC é o valor especificado, uma função de controle de moeda otimista é executada comparando carimbos de data/hora ou valores da soma de verificação, conforme determinado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se qualquer uma dessas linhas não corresponder, a operação falhará.  
  
 A especificação de UPDT_IN_PLACE como o valor de retorno controla os seguintes resultados:  
  
-   Se não estiver definido durante a execução de uma atualização posicionada em uma tabela com um índice exclusivo, o cursor excluirá a linha de sua tabela de trabalho e a inserirá ao final de qualquer uma das colunas de chave usadas pelo cursor, alterando assim essas colunas.  
  
-   Se estiver definido como ON, o cursor simplesmente atualizará as colunas de chave na linha original da tabela de trabalho.  
  
## <a name="boundparam-parameter"></a>Parâmetro bound_param  
 O nome do parâmetro deve ser *paramdef* quando PARAMETERIZED_STMT for especificado, acordo com a mensagem de erro no código. Quando PARAMETERIZED_STMT não é especificado, nenhum nome é especificado na mensagem de erro.  
  
## <a name="rpc-considerations"></a>Considerações sobre RPC:  
 O sinalizador de entrada RPC RETURN_METADATA pode ser definido como 0x0001 para solicitar que os metadados da lista de seleção de cursor sejam retornados no fluxo TDS.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="boundparam-parameter"></a>Parâmetro bound_param  
 Quaisquer parâmetros após o quinto são passados para o plano de instrução como parâmetros de entrada. O primeiro desses parâmetros deve ser uma cadeia de caracteres neste formato:  
  
 *{nome da variável local de tipo de dados} [,... n]*  
  
 Os parâmetros subsequentes são usados para passar os valores a serem substituídos para o *nome da variável local* na instrução.  
  
## <a name="see-also"></a>Consulte também  
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
