---
title: SET OFFSETS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET_OFFSETS_TSQL
- OFFSETS_TSQL
- SET OFFSETS
- OFFSETS
dev_langs:
- TSQL
helpviewer_keywords:
- position relative to start of statement [SQL Server]
- OFFSETS option
- offsets [SQL Server]
- SET OFFSETS statement
ms.assetid: c7bcc697-0930-4630-acae-d8ccbfa4414c
caps.latest.revision: 25
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b40204e252142b7b72962326ccc37e2174d3a811
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045824"
---
# <a name="set-offsets-transact-sql"></a>SET OFFSETS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna o deslocamento (posição relativa ao início de uma instrução) das palavras-chave especificadas nas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para aplicativos DB-Library.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET OFFSETS keyword_list { ON | OFF }  
```  
  
## <a name="arguments"></a>Argumentos  
 *keyword_list*  
 É uma lista separada por vírgula de construções [!INCLUDE[tsql](../../includes/tsql-md.md)] incluindo SELECT, FROM, ORDER, TABLE, PROCEDURE, STATEMENT, PARAM e EXECUTE.  
  
## <a name="remarks"></a>Remarks  
 SET OFFSETS é usado somente em aplicativos DB-Library.  
  
 A configuração de OFFSETS é definida no momento da análise e não no momento de execução ou em tempo de execução. Definir no momento da análise significa que, se a instrução SET estiver presente no procedimento em lote ou armazenado, a configuração entra em vigor, mesmo que a execução de código não tenha realmente alcançado aquele ponto; e a instrução SET entra em vigor antes de qualquer instrução ser executada. Por exemplo, mesmo que a instrução esteja em um bloco IF...ELSE que nunca é alcançado durante a execução, a instrução SET ainda entrará em vigor porque o bloco de instrução IF...ELSE é analisado.  
  
 Se SET OFFSETS for definido em um procedimento armazenado, seu valor é restaurado depois que o controle é retornado do procedimento armazenado. Portanto, uma instrução SET OFFSETS especificada em SQL dinâmico não causa nenhum efeito em qualquer instrução depois da instrução de SQL dinâmico.  
  
 SET PARSEONLY retornará deslocamentos se a opção OFFSETS for ON e nenhum erro ocorrer.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET PARSEONLY &#40;Transact-SQL&#41;](../../t-sql/statements/set-parseonly-transact-sql.md)  
  
  
