---
title: Tabela de modelagem (Tutorial do Adventure Works) | Microsoft Docs
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
keywords:
- Analysis Services
- Modelo de tabela
- Tutorial
- SSAS
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 30028afc0a7d994441a0958b207b7ab70c40f133
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-modeling-adventure-works-tutorial"></a>Modelagem de tabela (Tutorial do Adventure Works)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Este tutorial fornece lições sobre como criar um modelo de tabela do Analysis Services no [nível de compatibilidade 1200](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) usando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)e implantar seu modelo para um Analysis Services servidor local ou no Azure.  
 
Se você estiver usando 2017 do SQL Server ou do Azure Analysis Services, e você deseja criar seu modelo na compatibilidade de 1400 nível, use o [Azure Analysis Services – tutorial do Adventure Works](https://review.docs.microsoft.com/azure/analysis-services/tutorials/aas-adventure-works-tutorial?branch=master). Essa versão atualizada usa o recurso obter dados novo e moderno para se conectar e importar dados de origem e usa a linguagem M configurar partições.
 
  
## <a name="what-youll-learn"></a>O que você aprenderá   
  
-   Como criar um novo projeto de modelo de tabela no SSDT.
  
-   Como importar dados de um banco de dados relacional do SQL Server em um projeto de modelo de tabela.  
  
-   Como criar e gerenciar relações entre tabelas no modelo.  
  
-   Como criar e gerenciar cálculos, medidas e Indicadores Chave de Desempenho que ajudam os usuários a analisar dados de modelo.  
  
-   Como criar e gerenciar perspectivas e hierarquias que ajudam os usuários a navegar com mais facilidade pelos dados de modelo, fornecendo pontos de vista específicos de empresas e aplicativos.  
  
-   Como criar partições que dividem dados de tabela em partes lógicas menores que podem ser processadas independentemente de outras partições.  
  
-   Como proteger dados e objetos de modelo criando funções com membros de usuário.  
  
-   Como implantar um modelo de tabela para um Analysis Services server no local ou no Azure.  
  
## <a name="scenario"></a>Cenário  
Este tutorial baseia-se em Adventure Works Cycles, uma empresa fictícia. A Adventure Works é uma empresa de grande empresa multinacional de manufatura que produz e distribui Bicicletas de metal e compostas para mercados comerciais na América do Norte, Europa e Ásia. Com sede em Bothell, Washington, emprega 500 funcionários. Além disso, a Adventure Works emprega várias equipes regionais de vendas em toda a sua base de mercado.  
  
Para respaldar melhor as necessidades de análise de dados das equipes de vendas e de marketing e da gerência sênior, você fica encarregado de criar um modelo de tabela para que os usuários analisem dados de vendas pela Internet no banco de dados de exemplo AdventureWorksDW.  
  
Para concluir o tutorial e o modelo de tabela Adventure Works Internet Sales, você deve concluir várias lições. Em cada lição, há várias tarefas; a execução de cada uma delas na ordem é necessária para concluir a lição. Enquanto em uma lição específica pode haver várias tarefas que geram um resultado semelhante, mas como você conclui cada tarefa é ligeiramente diferente. Isso é para mostrar que geralmente há mais de uma maneira para concluir uma tarefa específica e para desafiá-lo a usar as habilidades que você aprendeu nas tarefas anteriores.  
  
A finalidade das lições é orientar você durante a criação de um modelo de tabela básico executado no modo na memória usando muitos dos recursos incluídos no SSDT. Como cada lição é criada após a lição anterior, você deve concluir as lições na ordem. Depois de concluir todas as lições, você terá criado e implantado o modelo de tabela de exemplo Adventure Works Internet Sales em um servidor do Analysis Services.  
  
Este tutorial não fornece lições ou informações sobre como gerenciar um banco de dados modelo de tabela implantado usando o SQL Server Management Studio ou usando um aplicativo cliente de relatórios para se conectar a um modelo implantado para procurar dados de modelo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Para concluir este tutorial, você precisará dos seguintes pré-requisitos:  
  
-   A versão mais recente do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. [Obter a versão mais recente](https://msdn.microsoft.com/library/mt204009.aspx).

-   A versão mais recente do SQL Server Management Studio. [Obter a versão mais recente](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 
  
-   Um aplicativo cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel.    
  
-   Uma instância do SQL Server com o banco de dados de exemplo Adventure Works DW 2014. Este banco de dados de exemplo inclui os dados necessários para concluir este tutorial. [Obter a versão mais recente](http://go.microsoft.com/fwlink/?LinkID=335807).  
  

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
  
  
  


