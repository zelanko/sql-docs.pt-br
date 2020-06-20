---
title: Várias restrições de precedência | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 61939b09b4a4365c09089df2b52026e96f9427ee
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965146"
---
# <a name="multiple-precedence-constraints"></a>Várias restrições de precedência
  Uma restrição de precedência conecta dois executáveis: duas tarefas, dois contêineres, ou um de cada. Eles são conhecidos como o executável de precedência e o executável restrito. Um executável restrito pode ter múltiplas restrições de precedência. Para obter informações, consulte [Restrições de precedência](control-flow/precedence-constraints.md).  
  
 Reunir cenários de restrição complexos por agrupamento de restrições permite que você implemente o fluxo de controle complexo em pacotes. Por exemplo, na ilustração a seguir, a Tarefa D está vinculada à Tarefa A por uma restrição `Success`, a Tarefa D está vinculada à Tarefa B por uma restrição `Failure` e a Tarefa D está vinculada à Tarefa C por uma restrição `Success`. As restrições de precedência entre as Tarefas D e A, entre as Tarefas D e B e entre as Tarefas D e C participam de uma relação lógica *and* . Portanto, para que a Tarefa D seja executada, a Tarefa A deve ser executada com êxito, a Tarefa B deve falhar e a Tarefa C deve ser executada com êxito.  
  
 ![Tarefas vinculadas por restrições de precedência](media/precedenceconstraints.gif "Tarefas vinculadas por restrições de precedência")  
  
## <a name="logicaland-property"></a>Propriedade LogicalAnd  
 Se uma tarefa ou contêiner tiver múltiplas restrições, a propriedade `LogicalAnd` especificará se uma restrição de precedência é avaliada isoladamente ou junto com outras restrições.  
  
 Você pode definir a `LogicalAnd` propriedade usando o **Editor de restrição de precedência** no [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer ou na janela Propriedades que o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de uma restrição de precedência](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
