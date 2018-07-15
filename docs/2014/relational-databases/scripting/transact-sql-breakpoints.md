---
title: Pontos de interrupção de Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dda48465dd65350c0326a07d3ee3696b90118619
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280672"
---
# <a name="transact-sql-breakpoints"></a>Pontos de interrupção Transact-SQL
  Os pontos de interrupção especificam que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] pause a execução em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] específica, para que você possa ver o estado dos elementos do código nesse ponto.  
  
## <a name="breakpoints"></a>Pontos de interrupção  
 Ao executar o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] , você pode alternar um ponto de interrupção em instruções específicas. Quando a execução alcançar uma instrução com um ponto de interrupção, o depurador pausará a execução para que você possa exibir informações de depuração, como os valores presentes em variáveis e parâmetros.  
  
 Você pode gerenciar pontos de interrupção individualmente na janela de editor, ou em conjunto, usando a janela **Pontos de interrupção** . Você pode editar pontos de interrupção para especificar itens, como as condições específicas sob as quais a execução deve pausar, ou as ações a serem adotadas se o ponto de interrupção for executado.  
  
## <a name="breakpoint-tasks"></a>Tarefas de ponto de interrupção  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como especificar a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] na qual você deseja que o depurador pause.|[Alternar um ponto de interrupção](../spatial/point.md)|  
|Descreve como desativar um ponto de interrupção temporariamente e, posteriormente, reativá-lo. Também descreve como excluir um ponto de interrupção.|[Habilitar, desabilitar e excluir pontos de interrupção](enable-disable-and-delete-breakpoints.md)|  
|Descreve como especificar uma condição, que define se o ponto de interrupção é interrompido com base na avaliação de uma expressão Transact-SQL especificada.|[Especificar uma condição de ponto de interrupção](specify-a-breakpoint-condition.md)|  
|Descreve como especificar uma contagem de ocorrências, que leva um ponto de interrupção a ser interrompido somente quando a instrução que contém o ponto de interrupção é executada um número especificado de vezes.|[Especificar uma contagem de ocorrências](specify-a-hit-count.md)|  
|Descreve como especificar um filtro, o que leva um ponto de interrupção a ser interrompido somente para processos ou threads especificados.|[Especificar um filtro de ponto de interrupção](specify-a-breakpoint-filter.md)|  
|Descreve como especificar uma ação **When Hit** , que é uma operação personalizada executada quando a instrução de ponto de interrupção é executada. Um exemplo seria a impressão de uma mensagem.|[Especificar uma ação de ponto de interrupção](specify-a-breakpoint-action.md)|  
|Descreve como editar o local de um ponto de interrupção.|[Editar um local de ponto de interrupção](edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Informações do depurador Transact-SQL](transact-sql-debugger-information.md)  
  
  
