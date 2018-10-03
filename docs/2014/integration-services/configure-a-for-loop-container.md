---
title: Configurar um contêiner Loop For | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: b9cd7ea7-b198-4a35-8b16-6acf09611ca5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2adcb3e79e3733b5fb8151bfa7f65e7bebb4d910
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126157"
---
# <a name="configure-a-for-loop-container"></a>Configurar um contêiner Loop For
  Este procedimento descreve como configurar um contêiner Loop For usando a caixa de diálogo **Editor do Loop For**.  
  
 Para obter um exemplo do contêiner Loop For, consulte [Loops SSIS que não falham](http://go.microsoft.com/fwlink/?LinkId=240295) em bimonkey.com.  
  
### <a name="to-configure-the-for-loop-container"></a>Para configurar um contêiner Loop For  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique duas vezes em contêiner Loop For para abrir o **Editor do Loop For**.  
  
2.  Como alternativa, modifique o nome e a descrição do contêiner Loop For.  
  
3.  Como alternativa, digite uma expressão de inicialização na caixa de texto **InitExpression** .  
  
4.  Como alternativa, digite uma expressão de inicialização na caixa de texto **EvalExpression** .  
  
    > [!NOTE]  
    >  A expressão deve ser avaliada como um booliano. Quando a expressão for avaliada como `false`, o loop irá parar sua execução.  
  
5.  Como alternativa, digite uma expressão de atribuição na caixa de texto **AssignExpression** .  
  
6.  Como alternativa, clique em **Expressões** e, na página **Expressões** , crie expressões de propriedade para as propriedades do contêiner Loop For. Para obter mais informações, consulte [Adicionar ou alterar uma expressão de propriedade](expressions/add-or-change-a-property-expression.md).  
  
7.  Clique em **OK** para fechar o **Editor do Loop For**.  
  
## <a name="see-also"></a>Consulte também  
 [Contêiner Loop for](control-flow/for-loop-container.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](expressions/integration-services-ssis-expressions.md)   
 [Usar expressões de propriedade em pacotes](expressions/use-property-expressions-in-packages.md)  
  
  
