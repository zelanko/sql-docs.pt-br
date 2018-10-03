---
title: Editor de restrição de precedência | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.precedenceconstraint.f1
helpviewer_keywords:
- Precedence Constraint Editor dialog box
ms.assetid: b10d4330-6e35-4037-b309-ef56efcd60c5
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c321d7a3850cf91b996262265492b88a6773f446
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217296"
---
# <a name="precedence-constraint-editor"></a>Editor de Restrição de Precedência
  Use a caixa de diálogo **Editor de Restrição de Precedência** para configurar as restrições de precedência.  
  
## <a name="options"></a>Opções  
 **Operação de avaliação**  
 Especifica a operação de avaliação usada pela restrição de precedência. As operações são: **Constraint**, **Expression**, **Expression and Constraint**e **Expression or Constraint**.  
  
 **Value**  
 Especifique o valor de restrição: **Êxito**, **Falha**ou **Conclusão**.  
  
> [!NOTE]  
>  A linha de restrição de precedência é verde para **Sucesso**, realçado para **Falha**e azul para **Conclusão**.  
  
 **Expression**  
 Se usar as operações **Expressão**, **Expressão e Restrição**ou **Expressão ou Restrição**, digite uma expressão ou inicie o Construtor de Expressões para criar a expressão. A expressão deve ser avaliada como um booliano.  
  
 **Testar**  
 Valide a expressão.  
  
 **AND lógico**  
 Selecione para especificar que várias restrições de precedência no mesmo executável devem ser avaliadas juntas. Todas as restrições devem ser avaliadas como `True`.  
  
> [!NOTE]  
>  Este tipo de restrição de precedência aparece como uma linha sólida nas cores verde, realçado ou azul.  
  
 **OR lógico**  
 Selecione para especificar que várias restrições de precedência no mesmo executável devem ser avaliadas juntas. Pelo menos uma restrição deve ser avaliada como `True`.  
  
> [!NOTE]  
>  Este tipo de restrição de precedência aparece como uma linha pontilhada nas cores verde, realçado ou azul.  
  
## <a name="see-also"></a>Consulte também  
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Tarefas do Integration Services](control-flow/integration-services-tasks.md)   
 [Contêineres do Integration Services](control-flow/integration-services-containers.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](expressions/integration-services-ssis-expressions.md)  
  
  
