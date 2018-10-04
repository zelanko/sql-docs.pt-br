---
title: Várias restrições de precedência | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- multiple precedence constraints
- precedence executables [Integration Services]
- precedence constraints [Integration Services], multiple
- constrained executables [Integration Services]
ms.assetid: 71c53ead-3d19-4bc1-aafd-e5b32595b420
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 368d8faf917094ce1dd306cc4ffd385eb3254363
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084856"
---
# <a name="multiple-precedence-constraints"></a>Várias restrições de precedência
  Uma restrição de precedência conecta dois executáveis: duas tarefas, dois contêineres, ou um de cada. Eles são conhecidos como o executável de precedência e o executável restrito. Um executável restrito pode ter múltiplas restrições de precedência. Para obter mais informações, consulte [Precedence Constraints](control-flow/precedence-constraints.md).  
  
 Reunir cenários de restrição complexos por agrupamento de restrições permite que você implemente o fluxo de controle complexo em pacotes. Por exemplo, na ilustração a seguir, tarefa D está vinculada à tarefa A por uma `Success` restrição, a tarefa D está vinculada à tarefa B por uma `Failure` restrição e a tarefa D está vinculada à tarefa C por uma `Success` restrição. As restrições de precedência entre as Tarefas D e A, entre as Tarefas D e B e entre as Tarefas D e C participam de uma relação lógica *and* . Portanto, para que a Tarefa D seja executada, a Tarefa A deve ser executada com êxito, a Tarefa B deve falhar e a Tarefa C deve ser executada com êxito.  
  
 ![Tarefas vinculadas por restrições de precedência](media/precedenceconstraints.gif "Tarefas vinculadas por restrições de precedência")  
  
## <a name="logicaland-property"></a>Propriedade LogicalAnd  
 Se uma tarefa ou contêiner tiver múltiplas restrições, a propriedade `LogicalAnd` especificará se uma restrição de precedência é avaliada isoladamente ou junto com outras restrições.  
  
 Você pode definir as `LogicalAnd` propriedade usando o **Editor de restrição de precedência** na [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, ou na janela Propriedades que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fornece.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de uma restrição de precedência](../../2014/integration-services/set-the-properties-of-a-precedence-constraint.md)  
  
  
