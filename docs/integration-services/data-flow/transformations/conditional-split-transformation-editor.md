---
title: "Editor de transformação de divisão condicional | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split Transformation Editor
ms.assetid: c30e1633-537a-4837-9991-6203c6f2a21e
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 769f9562af7bac75a488854319ba87ff8088329c
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="conditional-split-transformation-editor"></a>Editor de Transformação Divisão Condicional
  Use a caixa de diálogo **Editor de Transformação Divisão Condicional** para criar expressões, definir a ordem na qual as expressões são avaliadas e nomear as saídas de uma divisão condicional. Essa caixa de diálogo inclui funções matemáticas, de cadeia de caracteres e de data/hora e operadores que você pode usar para criar expressões. A primeira condição avaliada como verdadeira determina a saída para a qual uma linha é direcionada.  
  
> [!NOTE]  
>  A transformação Divisão Condicional direciona cada fila de entrada para uma única de saída. Se você digitar condições múltiplas, a transformação enviará cada fila à primeira saída para a qual a condição é verdadeira e desconsiderará condições subsequentes para aquela fila. Se for necessário avaliar várias condições sucessivamente, você poderá ter que concatenar transformações de Divisão Condicional múltiplas no fluxo de dados.  
  
 Para saber mais sobre a transformação Divisão Condicional, consulte [Transformação Divisão Condicional](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
## <a name="options"></a>Opções  
 **Order**  
 Selecione uma fila e use as teclas de seta à direita para alterar a ordem de avaliação de expressões.  
  
 **Nome de Saída**  
 Forneça um nome de saída. O padrão é uma lista numerada de casos; entretanto, você pode escolher qualquer nome exclusivo e descritivo.  
  
 **Condição**  
 Digite uma expressão ou compile uma arrastando da lista de colunas, variáveis, funções e operadores disponíveis.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Tópicos relacionados**: [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Operadores &#40;Expressão SSIS&#41;](../../../integration-services/expressions/operators-ssis-expression.md) e [Funções &#40;Expressão SSIS&#41;](../../../integration-services/expressions/functions-ssis-expression.md)  
  
 **Nome de saída padrão**  
 Digite um nome para a saída padrão ou use o padrão.  
  
 **Configurar saída de erro**  
 Especifique como tratar os erros usando a caixa de diálogo [Configurar Saída de Erro](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Dividir um conjunto de dados usando a transformação divisão condicional](../../../integration-services/data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
