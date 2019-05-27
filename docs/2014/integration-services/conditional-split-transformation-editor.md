---
title: Editor de transformação de divisão condicional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.conditionalsplittransformation.f1
helpviewer_keywords:
- Conditional Split Transformation Editor
ms.assetid: c30e1633-537a-4837-9991-6203c6f2a21e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 920ec41ae30d53853cfb757fb7fc33610953dc86
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66060892"
---
# <a name="conditional-split-transformation-editor"></a>Editor de Transformação Divisão Condicional
  Use a caixa de diálogo **Editor de Transformação Divisão Condicional** para criar expressões, definir a ordem na qual as expressões são avaliadas e nomear as saídas de uma divisão condicional. Essa caixa de diálogo inclui funções matemáticas, de cadeia de caracteres e de data/hora e operadores que você pode usar para criar expressões. A primeira condição avaliada como verdadeira determina a saída para a qual uma linha é direcionada.  
  
> [!NOTE]  
>  A transformação Divisão Condicional direciona cada fila de entrada para uma única de saída. Se você digitar condições múltiplas, a transformação enviará cada fila à primeira saída para a qual a condição é verdadeira e desconsiderará condições subsequentes para aquela fila. Se for necessário avaliar várias condições sucessivamente, você poderá ter que concatenar transformações de Divisão Condicional múltiplas no fluxo de dados.  
  
 Para saber mais sobre a transformação Divisão Condicional, consulte [Transformação Divisão Condicional](data-flow/transformations/conditional-split-transformation.md).  
  
## <a name="options"></a>Opções  
 **Order**  
 Selecione uma fila e use as teclas de seta à direita para alterar a ordem de avaliação de expressões.  
  
 **Nome de Saída**  
 Forneça um nome de saída. O padrão é uma lista numerada de casos; entretanto, você pode escolher qualquer nome exclusivo e descritivo.  
  
 **Condição**  
 Digite uma expressão ou compile uma arrastando da lista de colunas, variáveis, funções e operadores disponíveis.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Tópicos relacionados:**  [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md), [Operadores &#40;SSIS Expressão&#41;](expressions/operators-ssis-expression.md) e [Funções &#40;SSIS Expressão&#41;](expressions/functions-ssis-expression.md)  
  
 **Nome de saída padrão**  
 Digite um nome para a saída padrão ou use o padrão.  
  
 **Configurar saída de erro**  
 Especifique como tratar os erros usando a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Dividir um conjunto de dados por meio da transformação Divisão Condicional](data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
