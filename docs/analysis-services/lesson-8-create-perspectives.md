---
title: "Lição 9 criar perspectivas | Microsoft Docs"
ms.custom: 
ms.date: 03/27/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: dbeece52aab4ba77ceaebd03d42f72e6648c0d84
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-8-create-perspectives"></a>Lição 8: Criar perspectivas
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você criará uma perspectiva de Vendas pela Internet. Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos à empresa ou específicos ao aplicativo. Quando um usuário se conecta a um modelo usando uma perspectiva, eles veem apenas os objetos de modelo (tabelas, colunas, medidas, hierarquias e KPIs) como campos definidos nessa perspectiva.  
  
A perspectiva de vendas pela Internet criado nesta lição excluirá o objeto de tabela DimCustomer. Quando você cria uma perspectiva que exclui determinados objetos da exibição, esse objeto ainda existe no modelo; porém, não está visível em uma lista de campo de cliente de relatório. Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem ser calculadas de dados de objeto que são excluídos.  
  
A finalidade desta lição é descrever como criar perspectivas e se familiarizar com as ferramentas de criação de modelo de tabela. Se você expandir este modelo para incluir tabelas adicionais posteriormente, você poderá criar perspectivas adicionais para definir diferentes pontos de vista do modelo, por exemplo, inventário e vendas. Para saber mais, consulte [Perspectivas](../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 7: criar indicadores chave de desempenho](../analysis-services/lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Criar perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para criar uma perspectiva Vendas pela Internet  
  
1.  Clique o **modelo** menu > **perspectivas** > **criar e gerenciar**.  
  
2.  Na caixa de diálogo **Perspectivas** , clique em **Nova Perspectiva**.  
  
3.  Clique duas vezes o **nova perspectiva** título de coluna e, em seguida, renomeie **vendas pela Internet**.  
  
4.  Selecione todas as tabelas *exceto* **DimCustomer**.  
  
    ![como-tabela-lesson8-perspectivas](../analysis-services/media/as-tabular-lesson8-perspectives.png)
  
    Em uma lição posterior, você usará o analisar no recurso do Excel para testar esta perspectiva. A lista de campos de tabela dinâmica do Excel incluirá cada tabela, exceto a tabela DimCustomer.  

## <a name="whats-next"></a>O que vem a seguir?
Vá para a próxima lição: [lição 9: criar hierarquias](../analysis-services/lesson-9-create-hierarchies.md).
  
  
  
  
