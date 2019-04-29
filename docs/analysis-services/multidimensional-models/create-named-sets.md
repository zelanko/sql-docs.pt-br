---
title: Criar conjuntos nomeados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4eb82cba133f572e996f460be04661bfe511492e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020068"
---
# <a name="create-named-sets"></a>Criar conjuntos nomeados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Um conjunto nomeado é um conjunto de membros ou uma expressão de conjunto que é criado(a) para ser reutilizado(a), por exemplo, em consultas multidimensionais. É possível criar conjuntos nomeados combinando dados de cubo, operadores aritméticos, números e funções. Por exemplo, você pode criar um conjunto nomeado chamado Dez Maiores Fábricas que contém os dez membros da dimensão Fábricas com os valores mais altos para a medida Produção. Os usuários finais podem usar o conjunto Dez Maiores Fábricas em consultas. Por exemplo, um usuário final pode colocar o conjunto Dez Maiores Fábricas em um eixo e a dimensão Medidas, incluindo Produção, em outro. Para obter mais informações, consulte [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md), e [Criando conjuntos nomeados em MDX &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md).  
  
 Para criar um conjunto nomeado, use o comando **Novo Conjunto Nomeado** da guia **Cálculos** do Designer de Cubo. Esse comando pode ser chamado pelo menu **Cubo** na barra de ferramentas da guia **Cálculos** . Ele exibe um formulário para você especificar as seguintes opções para o conjunto nomeado:  
  
 **Nome**  
 Selecione o nome do conjunto nomeado. Ele aparecerá para os usuários finais quando eles procurarem o cubo.  
  
 **Expression**  
 Especifique a expressão que produz o conjunto nomeado. Pode ser escrita em MDX. A expressão pode conter uma das seguintes opções:  
  
-   Expressões de dados que representam componentes de cubo, como dimensões, níveis, medidas, etc.  
  
-   Operadores aritméticos.  
  
-   Números.  
  
-   Funções.  
  
 É possível copiar ou arrastar os componentes do cubo da guia **Metadados** no painel **Ferramentas de Cálculo** para a caixa **Expressão** do painel **Editor de Formulário de Conjunto de Nomeado** . É possível copiar ou arrastar as funções da guia **Funções** no painel **Ferramentas de Cálculo** para a caixa **Expressão** do painel **Editor de Formulário de Conjunto de Nomeado** .  
  
> [!IMPORTANT]  
>  Se você criar a expressão de conjunto nomeando explicitamente os membros no conjunto, coloque a lista de membros em um par de chaves ({}).  
  
## <a name="see-also"></a>Consulte também  
 [Cálculos em modelos multidimensionais](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
