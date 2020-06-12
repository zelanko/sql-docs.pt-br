---
title: 'Lição 8: definindo ações | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 15459396-83c9-48a0-b10a-99ae38768c79
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5299599a2431d68e3ea13370f51aceef58efaf14
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542228"
---
# <a name="lesson-8-defining-actions"></a>Lição 8: Como definir ações
  Nesta lição, você aprenderá a definir ações em seu projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Uma ação é como uma instrução MDX que é armazenada no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e que pode ser incorporada em aplicativos cliente e iniciada por um usuário.  
  
> [!NOTE]  
>  Projetos concluídos de todas as lições deste tutorial estão disponíveis online. Você pode avançar para qualquer lição com o uso do projeto concluído na lição anterior como um ponto de partida. [Clique aqui](https://go.microsoft.com/fwlink/?LinkID=221866) para baixar os projetos de exemplo fornecidos com este tutorial.  
  
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
 [Lição 9: Como definir perspectivas e traduções](lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cenário do tutorial de Analysis Services](analysis-services-tutorial-scenario.md)   
 [Modelagem multidimensional &#40;tutorial do Adventure Works&#41;](multidimensional-modeling-adventure-works-tutorial.md)   
 [Ações &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md)   
 [Ações em modelos multidimensionais](multidimensional-models/actions-in-multidimensional-models.md)  
  
  
