---
title: (Nível de compatibilidade 1200) de modelagem de tabela | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b0b8d60c6c365d48f8eccc46cbc9a3b0f5222ff5
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054683"
---
# <a name="tabular-modeling-1200-compatibility-level"></a>Modelagem tabular (nível de compatibilidade 1200)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Este tutorial fornece lições sobre como criar um modelo de tabela do Analysis Services na [nível de compatibilidade 1200](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) usando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)e implantar o modelo para um Analysis Services servidor local ou no Azure.  
 
Se você estiver usando o SQL Server 2017 ou o Azure Analysis Services, e você deseja criar seu modelo de compatibilidade 1400 nível, use o [(nível de compatibilidade 1400) de modelagem de tabela](tutorial-tabular-1400/as-adventure-works-tutorial.md). Essa versão atualizada usa o recurso moderno obter dados para se conectar e importar dados de origem, usa a linguagem M configurar partições e inclui lições suplementares adicionais.

> [!IMPORTANT]
> Você deve criar seus modelos de tabela no nível de compatibilidade mais recente com suporte pelo seu servidor. Modelos de nível de compatibilidade mais recente oferecem melhor desempenho, recursos adicionais e atualizarão mais facilmente os níveis de compatibilidade futura.
 
  
## <a name="what-you-learn"></a>O que você aprenderá   
  
-   Como criar um novo projeto de modelo de tabela no SSDT.
  
-   Como importar dados de um banco de dados relacional do SQL Server em um projeto de modelo de tabela.  
  
-   Como criar e gerenciar relações entre tabelas no modelo.  
  
-   Como criar e gerenciar cálculos, medidas e Indicadores Chave de Desempenho que ajudam os usuários a analisar dados de modelo.  
  
-   Como criar e gerenciar perspectivas e hierarquias que ajudam os usuários mais facilmente procurar dados de modelo, fornecendo pontos de vista específicos do aplicativo e de negócios.  
  
-   Como criar partições para dividir os dados de tabela em partes lógicas menores, que podem ser processadas independentemente de outras partições.  
  
-   Como proteger dados e objetos de modelo criando funções com membros de usuário.  
  
-   Como implantar um modelo de tabela para um Analysis Services server no local ou no Azure.  
  
## <a name="scenario"></a>Cenário  
Este tutorial se baseia na Adventure Works Cycles, uma empresa fictícia. Adventure Works é uma empresa de fabricação grande empresa industrial e multinacional que produz Bicicletas, peças e Acessórios para mercados comerciais na América do Norte, Europa e Ásia. Com sede em Bothell, Washington, a empresa emprega 500 trabalhadores. Além disso, a Adventure Works emprega várias equipes regionais de vendas em toda a sua base de mercado.  
  
Para respaldar melhor as necessidades de análise de dados das equipes de vendas e de marketing e da gerência sênior, você fica encarregado de criar um modelo de tabela para que os usuários analisem dados de vendas pela Internet no banco de dados de exemplo AdventureWorksDW.  
  
Para concluir o tutorial e o modelo de tabela Adventure Works Internet Sales, você deve concluir várias lições. Em cada lição é um número de tarefas; a conclusão de cada tarefa na ordem é necessário para concluir a lição. Embora em uma lição específica pode haver várias tarefas que geram um resultado semelhante, mas como você conclui cada tarefa é ligeiramente diferente. Isso é para mostrar que geralmente há mais de uma maneira para concluir uma tarefa específica e para desafiá-lo usando as habilidades que você aprendeu em tarefas anteriores.  
  
A finalidade das lições é orientá-lo a criar um modelo tabular básico executado no modo na memória usando muitos dos recursos incluídos no SSDT. Como cada lição é criada após a lição anterior, você deve concluir as lições na ordem. Depois de concluir todas as lições, você ter criado e implantado o modelo de tabela de exemplo do Adventure Works Internet Sales em um servidor do Analysis Services.  
  
Este tutorial não fornece lições ou informações sobre como gerenciar um banco de dados modelo de tabela implantado usando o SQL Server Management Studio ou usando um aplicativo cliente de relatórios para se conectar a um modelo implantado para procurar dados de modelo.  
  
## <a name="prerequisites"></a>Prerequisites  
Para concluir este tutorial, você precisará dos seguintes pré-requisitos:  
  
-   A versão mais recente do [SSDT](../ssdt/download-sql-server-data-tools-ssdt.md).

-   A versão mais recente do SQL Server Management Studio. [Obter a versão mais recente](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 
  
-   Um aplicativo cliente, como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel.    
  
-   Uma instância do SQL Server com o banco de dados de exemplo do Adventure Works DW. Este banco de dados de exemplo inclui os dados necessários para concluir este tutorial. [Obter a versão mais recente](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  

-   Um Azure Analysis Services ou SQL Server 2016 ou posterior instância do Analysis Services para implantar seu modelo. [Inscreva-se para uma avaliação gratuita do Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/).
  
## <a name="lessons"></a>Lições  
Este tutorial inclui as seguintes lições:  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[Lição 1: Criar um novo projeto de modelo de tabela](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[Lição 2: Adicionar dados](../analysis-services/lesson-2-add-data.md)|20 minutos|  
|[Lição 3: marcar como tabela de data](../analysis-services/lesson-3-mark-as-date-table.md)|3 minutos|  
|[Lição 4: Criar relações](../analysis-services/lesson-4-create-relationships.md)|10 minutos|  
|[Lição 5: Criar colunas calculadas](../analysis-services/lesson-5-create-calculated-columns.md)|15 minutos|
|[Lição 6: Criar medidas](../analysis-services/lesson-6-create-measures.md)|30 minutos|  
|[Lição 7: criar indicadores chave de desempenho](../analysis-services/lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[Lição 8: Criar perspectivas](../analysis-services/lesson-8-create-perspectives.md)|5 minutos|  
|[Lição 9: Criar hierarquias](../analysis-services/lesson-9-create-hierarchies.md)|20 minutos|  
|[Lição 10: Criar partições](../analysis-services/lesson-10-create-partitions.md)|15 minutos|  
|[Lição 11: Criar funções](../analysis-services/lesson-11-create-roles.md)|15 minutos|  
|[Lição 12: analisar no Excel](../analysis-services/lesson-12-analyze-in-excel.md)|20 minutos| 
|[Lição 13: implantar](../analysis-services/lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lições complementares  
Este tutorial também inclui [Lições complementares](http://msdn.microsoft.com/library/2018456f-b4a6-496c-89fb-043c62d8b82e). Os tópicos desta seção não são necessários para concluir o tutorial, mas podem ser úteis para a melhor compreensão dos recursos de criação do modelo de tabela avançado.  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[Implementar a segurança dinâmica usando filtros de linha](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 minutos|  

  
## <a name="next-step"></a>Próxima etapa  
Para iniciar o tutorial, vá para a primeira lição: [Lição 1: Criar um novo projeto de modelo de tabela](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

