---
title: 'Análise de tutorial dos serviços lição 8: criar perspectivas | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: c74e457d29f39201601a3a62d651cce97c52fa70
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207314"
---
# <a name="create-perspectives"></a>Criar perspectivas

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você criará uma perspectiva de vendas pela Internet. Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. Quando um usuário se conecta a um modelo usando uma perspectiva, eles veem apenas os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspectiva. Para saber mais, consulte [Perspectivas](../tabular-models/perspectives-ssas-tabular.md).
  
A perspectiva de vendas pela Internet que você criou nesta lição exclui o objeto de tabela DimCustomer. Quando você cria uma perspectiva que exclui determinados objetos de exibição, esse objeto ainda existe no modelo. No entanto, não é visível em uma lista de campo do cliente relatório. Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem ser calculadas de dados de objeto que são excluídos.  
  
A finalidade desta lição é descrever como criar perspectivas e se familiarizar com as ferramentas de criação de modelo de tabela. Se você expandir este modelo para incluir tabelas adicionais posteriormente, você pode criar perspectivas adicionais para definir diferentes pontos de vista do modelo, por exemplo, vendas e inventário.  
  
Tempo estimado para concluir esta lição: **Cinco minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 7: Criar indicadores chave de desempenho](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Criar perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para criar uma perspectiva Vendas pela Internet  
  
1.  Clique o **modelo** menu > **perspectivas** > **criar e gerenciar**.  
  
2.  Na caixa de diálogo **Perspectivas** , clique em **Nova Perspectiva**.  
  
3.  Clique duas vezes o **nova perspectiva** título de coluna e renomeie **vendas pela Internet**.  
  
4.  Selecione todas as tabelas *exceto* **DimCustomer**.  
  
    ![perspectivas como lesson8](../tutorial-tabular-1400/media/as-lesson8-perspectives.png)
  
    Uma lição posterior, você usa o analisar no recurso do Excel para testar essa perspectiva. A lista de campos de tabela dinâmica do Excel incluirá cada tabela, com exceção da tabela DimCustomer.  

## <a name="whats-next"></a>O que vem a seguir?

[Lição 9: Criar hierarquias](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).
  
  
  
  
