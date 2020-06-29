---
title: Editor de transformação não dinâmica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.unpivottransformation.f1
helpviewer_keywords:
- Unpivot Transformation Editor
ms.assetid: 72a36ef0-4070-4f6c-9c74-0720109617dd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 45aeb428f0905b7bf96900b6d592ff11963d8f4d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420313"
---
# <a name="unpivot-transformation-editor"></a>Editor de Transformação Não Dinâmica
  Use a caixa de diálogo **Editor de Transformação Não Dinâmica** para selecionar as colunas que serão dinamizadas em linhas, e para especificar as colunas de dados e a nova coluna de saída de valor dinâmico.  
  
> [!NOTE]  
>   Este tópico se baseia no cenário Não Dinâmico descrito em [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md) para ilustrar o uso das opções.  
  
 Para saber mais sobre transformação não dinâmica, consulte [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Usando as caixas de seleção, especifique as colunas que serão dinamizadas em linhas.  
  
 **Nome**  
 Exiba o nome da coluna de entrada disponível.  
  
 **Passagem**  
 Indique se a coluna deve ser incluída na saída não dinâmica.  
  
 **Coluna de Entrada**  
 Selecione colunas para cada linha na lista de colunas de entrada disponíveis. As seleções se refletem naquelas da caixa de seleção da tabela **Colunas de Entrada Disponíveis** .  
  
 No cenário Não Dinâmico descrito em [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), as Colunas de Entrada são as colunas **Ham**, **Soda**, **Milk**, **Beer**e **Chips** .  
  
 **Coluna de destino**  
 Forneça um nome para a coluna de dados.  
  
 No cenário Não Dinâmico descrito em [Transformação Não Dinâmica](data-flow/transformations/unpivot-transformation.md), a Coluna de Destino é a coluna de quantidade (**Qtd**).  
  
 **Valor de Chave Dinâmica**  
 Forneça um nome para o valor dinâmico. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 No cenário Não Dinâmico descrito em [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), os valores dinâmicos aparecerão na nova coluna Product designada pela opção **Nome da Coluna de Valores de Chaves Dinâmicas** , como os valores de texto **Ham**, **Soda**, **Milk**, **Beer**e **Chips**.  
  
 **Nome da Coluna de Valores de Chaves Dinâmicas**  
 Forneça um nome para a coluna de valor dinâmico. O padrão é "Valor da Chave Dinâmica"; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 No cenário Não Dinâmico descrito em [Unpivot Transformation](data-flow/transformations/unpivot-transformation.md), o nome de coluna de chave dinâmica é **Product** e designa a nova coluna **Product** , na qual as colunas **Ham**, **Soda**, **Milk**, **Beer**e **Chips** são não dinâmicos.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Transformação Dinâmica](data-flow/transformations/pivot-transformation.md)  
  
  
