---
title: A simultaneidade otimista | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa80ff3359e3bbbed9e28044cce7514006c40f10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446208"
---
# <a name="optimistic-concurrency"></a>Simultaneidade otimista
*A simultaneidade otimista* deriva seu nome a suposição otimista que raramente ocorrerão conflitos entre transações; uma colisão deve ter ocorrido quando outra transação atualiza ou exclui uma linha de dados entre a hora em que ele é lido a transação atual e o tempo seja atualizado ou excluído. Ele é o oposto da *simultaneidade pessimista,* ou bloqueio, em que o desenvolvedor do aplicativo acredita que tal colisões são comuns.  
  
 No modo de simultaneidade otimista, uma linha é deixada desbloqueada até chegar a hora de atualização ou excluí-lo. Nesse ponto, a linha é reler e verificada para ver se ele foi alterado desde a última leitura. Se a linha tiver sido alterado, a atualização ou exclusão falhará e deve ser tentada novamente.  
  
 Para determinar se uma linha foi alterada, sua nova versão é verificado em relação a uma versão em cache da linha. Essa verificação pode ser baseada na versão de linha, como a coluna de carimbo de hora no SQL Server ou os valores de cada coluna na linha. Muitos DBMSs não dão suporte a versões de linha.  
  
 A simultaneidade otimista pode ser implementada por fonte de dados ou o aplicativo. Em ambos os casos, o aplicativo deve usar um nível de isolamento da transação baixa, como leitura confirmada; usar um nível mais alto nega a simultaneidade aumentada obtida com o uso de simultaneidade otimista.  
  
 Se a simultaneidade otimista é implementada pela fonte de dados, o aplicativo define o atributo de instrução SQL_ATTR_CONCURRENCY SQL_CONCUR_ROWVER ou SQL_CONCUR_VALUES. Para atualizar ou excluir uma linha, ele executa uma atualização posicionada ou instrução delete ou chamadas **SQLSetPos** como faria com simultaneidade pessimista; a driver ou fonte de dados retornará SQLSTATE 01001 (conflito de operação do Cursor) se a atualização ou exclusão falha devido a uma colisão.  
  
 Se o aplicativo em si implementa a simultaneidade otimista, ela define o atributo de instrução SQL_ATTR_CONCURRENCY como SQL_CONCUR_READ_ONLY para ler uma linha. Se ele irá comparar as versões de linha e não sabe a coluna de versão de linha, ele chama **SQLSpecialColumns** com a opção SQL_ROWVER para determinar o nome desta coluna.  
  
 O aplicativo atualiza ou exclui a linha, aumentando a simultaneidade SQL_CONCUR_LOCK (para acesso de gravação para a linha) e executar uma **atualização** ou **excluir** instrução com um **onde**  cláusula que especifica a versão ou valores de linha tinha quando o aplicativo lê-lo. Se a linha foi alterada desde então, a instrução falhará. Se o **onde** cláusula não identifica exclusivamente a linha, a instrução também pode atualizar ou excluir as outras linhas; as versões de linha sempre identificam linhas, mas valores de linha identificam exclusivamente linhas somente se elas incluem a chave primária.
