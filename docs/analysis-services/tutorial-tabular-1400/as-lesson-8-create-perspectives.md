---
title: Análise de 8 perspectivas de criação de lição do tutorial de serviços | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6de14f79ab00f489913153abefa1ae40aa5608e7
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="create-perspectives"></a>Criar perspectivas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você criará uma perspectiva de vendas pela Internet. Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. Quando um usuário se conecta a um modelo usando uma perspectiva, eles veem apenas os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspectiva. Para obter mais informações, consulte [perspectivas](../tabular-models/perspectives-ssas-tabular.md).
  
A perspectiva de vendas pela Internet criado nesta lição exclui o objeto de tabela DimCustomer. Quando você cria uma perspectiva que exclui determinados objetos de exibição, esse objeto ainda existe no modelo. No entanto, não é visível na lista de campos relatórios do cliente. Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem ser calculadas de dados de objeto que são excluídos.  
  
A finalidade desta lição é descrever como criar perspectivas e se familiarizar com as ferramentas de criação de modelo de tabela. Se você expandir este modelo para incluir tabelas adicionais posteriormente, você poderá criar perspectivas adicionais para definir diferentes pontos de vista do modelo, por exemplo, inventário e vendas.  
  
Tempo estimado para concluir esta lição: **cinco minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 7: criar indicadores chave de desempenho](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Criar perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para criar uma perspectiva Vendas pela Internet  
  
1.  Clique o **modelo** menu > **perspectivas** > **criar e gerenciar**.  
  
2.  Na caixa de diálogo **Perspectivas** , clique em **Nova Perspectiva**.  
  
3.  Clique duas vezes o **nova perspectiva** título de coluna e, em seguida, renomeie **vendas pela Internet**.  
  
4.  Selecione todas as tabelas *exceto* **DimCustomer**.  
  
    ![perspectivas como lesson8](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    Em uma lição posterior, você usa o recurso analisar no Excel para testar esta perspectiva. A lista de campos de tabela dinâmica do Excel inclui cada tabela exceto a tabela DimCustomer.  

## <a name="whats-next"></a>O que vem a seguir?

[Lição 9: Criar hierarquias](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).
  
  
  
  
