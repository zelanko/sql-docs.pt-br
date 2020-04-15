---
title: Concorrência Otimista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30eba3ea03b4c798a74a8cb928014b582846607b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282476"
---
# <a name="optimistic-concurrency"></a>Simultaneidade otimista
*A concorrência otimista* deriva seu nome da suposição otimista de que colisões entre transações raramente ocorrerão; diz-se que uma colisão ocorreu quando outra transação atualiza ou exclui uma linha de dados entre o momento em que é lido pela transação atual e o momento em que é atualizado ou excluído. É o oposto de *concorrência pessimista,* ou bloqueio, em que o desenvolvedor de aplicativos acredita que tais colisões são comuns.  
  
 Na concorrência otimista, uma linha é deixada desbloqueada até a hora de atualizá-la ou excluí-la. Nesse ponto, a linha é relida e verificada para ver se foi alterada desde que foi lida pela última vez. Se a linha tiver sido alterada, a atualização ou exclusão falhará e deve ser julgada novamente.  
  
 Para determinar se uma linha foi alterada, sua nova versão é verificada em uma versão em cache da linha. Essa verificação pode ser baseada na versão de linha, como a coluna carimbo de tempo no SQL Server ou os valores de cada coluna na linha. Muitos DBMSs não suportam versões de linha.  
  
 A concorrência otimista pode ser implementada pela fonte de dados ou pelo aplicativo. Em ambos os casos, o aplicativo deve usar um baixo nível de isolamento de transações, como Read Committed; usando um nível mais alto nega o aumento da concorrência adquirida usando uma concorrência otimista.  
  
 Se a concorrência otimista for implementada pela fonte de dados, o aplicativo define o atributo de declaração SQL_ATTR_CONCURRENCY para SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES. Para atualizar ou excluir uma linha, ele executa uma atualização posicionada ou exclui a declaração ou chama **SQLSetPos** assim como seria com a concorrência pessimista; o driver ou fonte de dados retorna SQLSTATE 01001 (conflito de operação cursor) se a atualização ou exclusão falhar devido a uma colisão.  
  
 Se o próprio aplicativo implementar uma concorrência otimista, ele define o atributo de declaração SQL_ATTR_CONCURRENCY para SQL_CONCUR_READ_ONLY ler uma linha. Se ele comparar versões de linha e não conhecer a coluna de versões da linha, ele chamará **SQLSpecialColumns** com a opção SQL_ROWVER de determinar o nome desta coluna.  
  
 O aplicativo atualiza ou exclui a linha aumentando a concorrência para SQL_CONCUR_LOCK (para obter acesso à linha) e executando uma declaração **UPDATE** ou **DELETE** com uma cláusula **WHERE** que especifica a versão ou os valores que a linha tinha quando o aplicativo a leu. Se a linha mudou desde então, a declaração falhará. Se a cláusula **WHERE** não identificar exclusivamente a linha, a declaração também poderá atualizar ou excluir outras linhas; Versões de linha sempre identificam linhas exclusivamente, mas os valores de linha identificam exclusivamente as linhas apenas se elas incluem a chave principal.
