---
title: 'Lição 8: Definindo ações | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: a57c6cc8d08d64c8f2498125f7df952c70adfd6d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115728"
---
# <a name="lesson-8-defining-actions"></a>Lição 8: Definindo ações
  Nesta lição, você aprenderá a definir ações em seu projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Uma ação é como uma instrução MDX que é armazenada no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e que pode ser incorporada em aplicativos cliente e iniciada por um usuário.  
  
> [!NOTE]  
>  Projetos concluídos de todas as lições deste tutorial estão disponíveis online. Você pode avançar para qualquer lição com o uso do projeto concluído na lição anterior como um ponto de partida. [Clique aqui](http://go.microsoft.com/fwlink/?LinkID=221866) para baixar os projetos de exemplo fornecidos com este tutorial.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dá suporte aos tipos de ações descritos na tabela a seguir.  
  
|||  
|-|-|  
|CommandLine|Executa um comando no prompt de comando.|  
|Dataset|Retorna um conjunto de dados a um aplicativo cliente.|  
|Detalhamento|Retorna uma instrução de detalhamento como uma expressão e que o cliente executa para retornar um conjunto de dados.|  
|Html|Executa um script HTML em um navegador de Internet.|  
|Proprietário|Executa uma operação usando uma interface diferente das listadas nesta tabela.|  
|Relatório|Envia uma solicitação com base em URL parametrizada para um servidor de relatórios e retorna um relatório a um aplicativo cliente.|  
|Conjunto de linhas|Retorna um conjunto de linhas a um aplicativo cliente.|  
|de|Executa um comando OLE DB.|  
|URL|Exibe uma página da Web dinâmica em um navegador de Internet.|  
  
 As ações permitem que os usuários iniciem um aplicativo ou executem outras etapas dentro do contexto de um item selecionado. Para obter mais informações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md), [Ações em modelos multidimensionais](multidimensional-models/actions-in-multidimensional-models.md)  
  
> [!NOTE]  
>  Para obter mais exemplos de ações, consulte os exemplos de ação na guia Modelo do painel Ferramentas de Cálculo ou nos exemplos do data warehouse de exemplo do DW da [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] . Para obter mais informações sobre como instalar esse banco de dados, consulte [Instalar dados de exemplo e projetos para o tutorial de modelagem multidimensional do Analysis Services](install-sample-data-and-projects.md).  
  
 Esta lição inclui a seguinte tarefa:  
  
 [Definindo e usando uma ação de detalhamento](lesson-8-1-defining-and-using-a-drillthrough-action.md)  
 Nesta tarefa, você definirá, usará e modificará uma ação de detalhamento através da relação de dimensão de fatos definida anteriormente neste tutorial.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 9: definindo perspectivas e traduções](lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>Consulte também  
 [Cenário do Tutorial do Analysis Services](analysis-services-tutorial-scenario.md)   
 [Modelagem multidimensional &#40;Tutorial da Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md)   
 [Ações &#40;Analysis Services - dados multidimensionais&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)   
 [Ações em modelos multidimensionais](multidimensional-models/actions-in-multidimensional-models.md)  
  
  