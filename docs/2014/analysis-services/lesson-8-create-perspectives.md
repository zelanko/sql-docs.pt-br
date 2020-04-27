---
title: 'Lição 9: criar perspectivas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 55b0f0d0-1cdf-4876-9c3d-d0c848be3f5d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd395e605bfde9d34ed0dc4f16060812464efb56
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66078249"
---
# <a name="lesson-9-create-perspectives"></a>Lição 9: Criar perspectivas
  Nesta lição, você criará uma perspectiva de Vendas pela Internet. Uma perspectiva define um subconjunto exibível de um modelo que fornece pontos de vista concentrados, específicos da empresa ou específicos do aplicativo. Quando um usuário se conecta a um modelo usando uma perspectiva, ele vê apenas os objetos de modelo (tabelas, colunas, medidas e KPIs) como campos definidos nessa perspectiva.  
  
 A perspectiva Vendas pela Internet que você criou nesta lição excluirá o objeto de tabela Cliente. Quando você cria uma perspectiva que exclui determinados objetos da exibição, esse objeto ainda existe no modelo; porém, não está visível em uma lista de campo de cliente de relatório. Colunas calculadas e medidas incluídas ou não em uma perspectiva ainda podem ser calculadas de dados de objeto que são excluídos.  
  
 A finalidade desta lição é descrever como criar perspectivas e se familiarizar com as ferramentas de criação de modelo de tabela. Se você expandir este modelo posteriormente para incluir tabelas adicionais, poderá criar perspectivas adicionais para definir diferentes pontos de vista do modelo; por exemplo, Inventário e Força de Vendas.  
  
 Para saber mais, consulte [Perspectivas &#40;SSAS Tabular&#41;](tabular-models/perspectives-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deve ter concluído a lição anterior: [Lição 8: Criar Indicadores Chave de Desempenho](lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Criar perspectivas  
  
#### <a name="to-create-an-internet-sales-perspective"></a>Para criar uma perspectiva Vendas pela Internet  
  
1.  No designer de modelos, clique no menu **modelo** e em **perspectivas**.  
  
2.  Na caixa de diálogo **Perspectivas** , clique em **Nova Perspectiva**.  
  
3.  Para renomear a perspectiva, clique duas vezes no título da coluna **nova perspectiva 1** e `Internet Sales`digite.  
  
4.  Em **campos**, selecione a seguinte **Data**de tabelas, **geografia**, **produto**, **categoria de produto**, **subcategoria**de `Internet Sales`produto e.  
  
     Observe que você excluiu a tabela Cliente e todas as suas colunas desta perspectiva. Posteriormente, na Lição 12, você usará o recurso Analisar no Excel para testar esta perspectiva. A Lista de Campos da Tabela Dinâmica do Excel incluirá cada tabela exceto a tabela Cliente.  
  
5.  Verifique as seleções, garantindo que a tabela **Customer** não está marcada e clique em **OK**  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 10: Criar hierarquias](lesson-9-create-hierarchies.md).  
  
  
