---
title: Simultaneidade otimista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95593c35e55f899c3fb062adf4f5edde197f813c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="optimistic-concurrency"></a>Simultaneidade otimista
*Simultaneidade otimista* deriva seu nome a suposição otimista de que raramente ocorrerão conflitos entre transações; uma colisão é considerada ocorreram quando outra transação atualiza ou exclui uma linha de dados entre o momento em que ele seja lido a transação atual e a hora, ela é atualizada ou excluída. É o oposto do *simultaneidade pessimista,* ou bloqueio, em que o desenvolvedor do aplicativo acredita que tal colisões são comuns.  
  
 No modo de simultaneidade otimista, uma linha é deixada desbloqueada até chegar a hora de atualização ou excluí-lo. Nesse ponto, a linha é reler e verificada para ver se ele tiver sido alterado desde a última leitura. Se a linha foi alterada, a falha de atualização ou exclusão e deve ser tentada novamente.  
  
 Para determinar se uma linha tiver sido alterada, a nova versão é verificada em relação a uma versão em cache da linha. Essa verificação pode ser baseada em versão de linha, como a coluna de carimbo de hora no SQL Server ou os valores de cada coluna na linha. Muitos DBMSs não dão suporte a versões de linha.  
  
 Simultaneidade otimista pode ser implementada por fonte de dados ou o aplicativo. Em ambos os casos, o aplicativo deve usar um nível de isolamento de transação baixa como leitura confirmada; usar um nível mais alto nega o aprimoramento de simultaneidade obtido usando simultaneidade otimista.  
  
 Se a simultaneidade otimista é implementada pela fonte de dados, o aplicativo define o atributo de instrução SQL_ATTR_CONCURRENCY SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES. Para atualizar ou excluir uma linha, ele executa uma atualização posicionada ou instrução delete ou chamadas **SQLSetPos** como faria com simultaneidade pessimista; a fonte de dados ou driver retornará SQLSTATE 01001 (conflito de operação de Cursor) se a atualização ou exclusão falha devido a uma colisão.  
  
 Se o aplicativo em si implementa simultaneidade otimista, ela define o atributo de instrução SQL_ATTR_CONCURRENCY como SQL_CONCUR_READ_ONLY para ler uma linha. Se ele irá comparar versões de linha e não sabe qual é a coluna de versão de linha, ele chama **SQLSpecialColumns** com a opção SQL_ROWVER para determinar o nome dessa coluna.  
  
 O aplicativo atualiza ou exclui a linha, aumentando a simultaneidade SQL_CONCUR_LOCK (para obter acesso de gravação para a linha) e executar um **atualização** ou **excluir** instrução com um **onde**  cláusula que especifica a versão ou os valores de linha tinha quando o aplicativo lê-lo. Se a linha foi alterada desde então, a instrução falhará. Se o **onde** cláusula não identifica exclusivamente a linha, a instrução também pode atualizar ou excluir outras linhas; versões de linha sempre identificam linhas, mas valores de linha identificam exclusivamente linhas somente se elas incluem a chave primária.
