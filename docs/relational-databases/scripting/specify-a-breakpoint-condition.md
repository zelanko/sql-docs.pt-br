---
title: "Especificar uma condição de ponto de interrupção | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.breakpt.condition
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 087070d0e19d777b6ac2d457303e9e9962073ead
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="specify-a-breakpoint-condition"></a>Especificar uma condição de ponto de interrupção
  Uma condição de ponto de interrupção é uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] que é avaliada pelo depurador ao atingir o ponto de interrupção. Se a condição for atendida e qualquer contagem de ocorrências especificada for atingida, o depurador será interrompido ou executará a ação especificada para o ponto de interrupção.  
  
## <a name="specifying-conditions"></a>Especificando condições  
 A expressão especificada deve ser uma expressão Transact-SQL válida que seja avaliada como um valor Booliano. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 Se você especificar uma condição de ponto de interrupção com sintaxe inválida, será exibida uma mensagem de aviso imediatamente. Se você especificar uma condição com sintaxe válida, mas semântica inválidas, será exibida uma mensagem de aviso da primeira vez que o ponto de interrupção for atingido. Em qualquer um dos casos, o depurador interromperá a execução quando o ponto de interrupção inválido for atingido.  
  
#### <a name="to-specify-a-condition"></a>Para especificar uma condição  
  
1.  Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Condição** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Condição** no menu de atalho.  
  
2.  Na caixa de diálogo **Condição de Ponto de Interrupção** , insira uma expressão Booliana válida na caixa **Condição** .  
  
3.  Escolha **Is true** para interromper quando a expressão for avaliada como **true**ou escolha **Has changed** para interromper quando o valor da expressão for alterado.  
  
    > [!NOTE]  
    >  O depurador não avalia a expressão Booliana até a primeira vez que o ponto de interrupção é atingido. Se você escolher **Has changed**, o depurador não considerará a primeira avaliação como uma alteração, então o depurador não interromperá na primeira avaliação.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar uma contagem de ocorrências](../../relational-databases/scripting/specify-a-hit-count.md)   
 [Especificar uma ação de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-action.md)  
  
  
