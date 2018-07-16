---
title: 'Lição 6: Definindo cálculos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e0a1e354-e879-4eb8-bb2b-6c3809e32cb6
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dcc6179b4a0cc0a5b5ade735ef7272d265e35c24
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37326656"
---
# <a name="lesson-6-defining-calculations"></a>Lição 6: Definindo cálculos
  Nesta lição, você aprenderá a definir cálculos, que são scripts ou expressões MDX (Multidimensional Expressions). Os cálculos permitem que você defina membros calculados, conjuntos nomeados ou execute outros comandos de script para aumentar os recursos de um cubo do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Por exemplo, você pode executar um comando de script para definir um subcubo e depois atribuir um cálculo às células no subcubo.  
  
 Ao definir um novo cálculo no Designer de Cubo, o cálculo é adicionado ao painel **Organizador de Script** da guia **Cálculos** do Designer de Cubo, e os campos deste tipo específico de cálculo são exibidos em um formulário de cálculos no painel **Expressões de Cálculo** . Os cálculos são executados na ordem em que estão listados no painel **Organizador de Script** . Você pode reordenar os cálculos clicando com o botão direito do mouse em um cálculo específico e selecionando **Mover para Cima** ou **Mover para Baixo**, ou clicando em cálculo específico e usando os ícones **Mover para Cima** ou **Mover para Baixo** na barra de ferramentas da guia **Cálculos** .  
  
 Na guia **Cálculos** , você pode adicionar novos cálculos e exibir ou editar cálculos existentes nas seguintes exibições do painel **Expressões de Cálculo** :  
  
-   Exibição de formulário. Esta exibição mostra as expressões e propriedades de um único comando em um formato gráfico. Quando você edita um script MDX, uma caixa de expressão preenche a exibição Formulário.  
  
-   Exibição de script. Esta exibição mostra todos os scripts de cálculo em um editor de código que permite alterar os scripts de cálculo facilmente. Quando o painel **Expressões de Cálculo** está na Exibição de script, o **Organizador de Script** fica oculto. A Exibição de script fornece codificação por cor, correspondência de parênteses, preenchimento automático e regiões de código MDX. Você pode expandir ou recolher as regiões de código MDX para facilitar a edição.  
  
 Para alternar entre esses exibições no painel **Expressões de Cálculo** , clique em **Exibição de Formulário** ou **Exibição de Script** na barra de ferramentas da guia **Cálculos** .  
  
> [!NOTE]  
>  Se o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] detectar um erro de sintaxe em qualquer cálculo, a Exibição de formulário não será exibida até que o erro seja corrigido na Exibição de script.  
  
 Você também pode usar o Assistente de Business Intelligence para adicionar determinados cálculos a um cubo. Por exemplo, você pode usar esse assistente para adicionar inteligência de tempo a um cubo, o que significa definir membros calculados para cálculos relacionados ao tempo como período até esta data, médias de movimentação ou crescimento de período sobre período. Para obter mais informações, consulte [Definir cálculos de inteligência de tempo com o Assistente de Business Intelligence](multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!IMPORTANT]  
>  Na guia **Cálculos** , o script de cálculo inicia com o comando CALCULATE. O comando CALCULATE controla a agregação das células do cubo e deve ser editado apenas se você pretender especificar manualmente como as células do cubo devem ser agregadas.  
  
 Para obter mais informações, consulte [Cálculos](multidimensional-models-olap-logical-cube-objects/calculations.md)e [Cálculos em modelos multidimensionais](multidimensional-models/calculations-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Projetos concluídos de todas as lições deste tutorial estão disponíveis online. Você pode avançar para qualquer lição com o uso do projeto concluído na lição anterior como um ponto de partida. [Clique aqui](http://go.microsoft.com/fwlink/?LinkID=221866) para baixar os projetos de exemplo fornecidos com este tutorial.  
  
 Esta lição contém as seguintes tarefas:  
  
 [Definindo membros calculados](../analysis-services/lesson-6-1-defining-calculated-members.md)  
 Nesta tarefa, você aprenderá a definir membros calculados.  
  
 [Definindo conjuntos nomeados](../analysis-services/lesson-6-2-defining-named-sets.md)  
 Nesta tarefa, você aprenderá a definir conjuntos nomeados.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 7: Definindo KPIs &#40;Indicadores Chave de Desempenho&#41;](../analysis-services/lesson-7-defining-key-performance-indicators-kpis.md)  
  
## <a name="see-also"></a>Consulte também  
 [Cenário do Tutorial do Analysis Services](../analysis-services/analysis-services-tutorial-scenario.md)   
 [Modelagem multidimensional &#40;Tutorial da Adventure Works&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)   
 [Criar conjuntos nomeados](multidimensional-models/create-named-sets.md)   
 [Criar membros calculados](multidimensional-models/create-calculated-members.md)  
  
  
