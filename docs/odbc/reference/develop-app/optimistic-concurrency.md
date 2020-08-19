---
description: Simultaneidade otimista
title: Simultaneidade otimista | Microsoft Docs
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
ms.openlocfilehash: dce1982edbb8f5a417404c6e24e8a40d25b58e0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429128"
---
# <a name="optimistic-concurrency"></a>Simultaneidade otimista
A *simultaneidade otimista* deriva seu nome da pressuposição otimista de que as colisões entre as transações raramente ocorrerão; uma colisão deve ter ocorrido quando outra transação atualiza ou exclui uma linha de dados entre a hora em que é lida pela transação atual e a hora em que ela é atualizada ou excluída. É o oposto da *simultaneidade pessimista* ou do bloqueio, em que o desenvolvedor do aplicativo acredita que essas colisões são comuns.  
  
 Na simultaneidade otimista, uma linha é deixada desbloqueada até que a hora seja atualizada ou excluída. Nesse ponto, a linha é relida e verificada para ver se ela foi alterada desde a última leitura. Se a linha tiver sido alterada, a atualização ou exclusão falhará e deverá ser tentada novamente.  
  
 Para determinar se uma linha foi alterada, sua nova versão é verificada em relação a uma versão armazenada em cache da linha. Essa verificação pode ser baseada na versão de linha, como a coluna timestamp em SQL Server ou os valores de cada coluna na linha. Muitos DBMSs não oferecem suporte a versões de linha.  
  
 A simultaneidade otimista pode ser implementada pela fonte de dados ou pelo aplicativo. Em ambos os casos, o aplicativo deve usar um nível de isolamento de transação baixo, como leitura confirmada; o uso de um nível superior nega a simultaneidade aumentada obtida usando simultaneidade otimista.  
  
 Se a simultaneidade otimista for implementada pela fonte de dados, o aplicativo definirá o atributo SQL_ATTR_CONCURRENCY instrução como SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES. Para atualizar ou excluir uma linha, ela executa uma instrução UPDATE ou DELETE posicionada ou chama **SQLSetPos** exatamente como faria com a simultaneidade pessimista; o driver ou a fonte de dados retorna SQLSTATE 01001 (conflito de operação do cursor) se a atualização ou exclusão falhar devido a uma colisão.  
  
 Se o próprio aplicativo implementar a simultaneidade otimista, ele definirá o atributo SQL_ATTR_CONCURRENCY Statement como SQL_CONCUR_READ_ONLY para ler uma linha. Se ele comparar versões de linha e não souber a coluna de versão de linha, ele chamará **SQLSpecialColumns** com a opção SQL_ROWVER para determinar o nome dessa coluna.  
  
 O aplicativo atualiza ou exclui a linha aumentando a simultaneidade para SQL_CONCUR_LOCK (para obter acesso de gravação à linha) e executar uma instrução **Update** ou **delete** com uma cláusula **Where** que especifica a versão ou os valores que a linha tinha quando o aplicativo a leu. Se a linha foi alterada desde então, a instrução falhará. Se a cláusula **Where** não identificar exclusivamente a linha, a instrução também poderá atualizar ou excluir outras linhas; as versões de linha sempre identificam linhas exclusivamente, mas os valores de linha identificam exclusivamente as linhas somente se incluírem a chave primária.
