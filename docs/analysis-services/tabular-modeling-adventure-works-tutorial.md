---
title: "Modelagem de tabela (Tutorial do Adventure Works) | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
keywords: 
  - "Analysis Services"
  - "Modelo de tabela"
  - "Tutorial"
  - "SSAS"
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# Modelagem de tabela (Tutorial do Adventure Works)
Este tutorial fornece lições sobre como criar um modelo de tabela do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
  
## O que você aprenderá  
No decorrer deste tutorial, você aprenderá o seguinte:  
  
-   Como criar um novo projeto de modelo de tabela no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Como importar dados de um banco de dados relacional do SQL Server em um projeto de modelo de tabela.  
  
-   Como criar e gerenciar relações entre tabelas no modelo.  
  
-   Como criar e gerenciar cálculos, medidas e Indicadores Chave de Desempenho que ajudam os usuários a analisar dados de modelo.  
  
-   Como criar e gerenciar perspectivas e hierarquias que ajudam os usuários a navegar com mais facilidade pelos dados de modelo, fornecendo pontos de vista específicos de empresas e aplicativos.  
  
-   Como criar partições que dividem dados de tabela em partes lógicas menores que podem ser processadas independentemente de outras partições.  
  
-   Como proteger dados e objetos de modelo criando funções com membros de usuário.  
  
-   Como implantar um modelo tabular em uma área restrita ou instância de produção do Analysis Services em execução no modo Tabular.  
  
## Cenário  
Este tutorial baseia-se na [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], uma empresa fictícia. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é uma grande empresa multinacional que produz e distribui bicicletas de metal e compostos para mercados comerciais da América do Norte, Europa e Ásia. A sede da [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] é em Bothell, Washington, onde emprega 500 funcionários. Além disso, a [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] emprega várias equipes de vendas regionais por toda a sua base de mercado.  
  
Para respaldar melhor as necessidades de análise de dados das equipes de vendas e de marketing e da gerência sênior, você fica encarregado de criar um modelo de tabela para que os usuários analisem dados de vendas pela Internet no banco de dados de exemplo AdventureWorksDW.  
  
Para concluir o tutorial e o modelo de tabela Adventure Works Internet Sales, você deve concluir várias lições. Em cada lição, há várias tarefas; a execução de cada uma delas na ordem é necessária para concluir a lição. Embora em uma lição específica possa haver várias tarefas que geram um resultado semelhante, no entanto, o modo como você conclui cada tarefa é ligeiramente diferente. Isso acontece para mostrar que geralmente há mais de uma maneira de concluir uma tarefa específica e para desafiá-lo a usar as habilidades adquiridas nas tarefas anteriores.  
  
A finalidade das lições é conduzi-lo pelo processo de criação de um modelo tabular básico executado no modo Em Memória usando muitos dos recursos incluídos em [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Como cada lição é criada após a lição anterior, você deve concluir as lições na ordem. Depois que você tiver concluído todas as lições, terá criado e implantado o modelo de tabela de exemplo Adventure Works Internet Sales em um servidor do Analysis Services.  
  
Este tutorial não fornece lições ou informações sobre como gerenciar um banco de dados modelo de tabela implantado usando o SQL Server Management Studio ou usando um aplicativo cliente de relatórios para se conectar a um modelo implantado para procurar dados de modelo.  
  
## Pré-requisitos  
Para concluir este tutorial, você deve ter os seguintes pré-requisitos instalados:  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Instância do Analysis Services em execução no modo de Tabela.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. [Obtenha a versão mais recente.](https://msdn.microsoft.com/library/mt204009.aspx)  
  
-   Banco de dados de exemplo do Adventure Works DW 2014. Este banco de dados de exemplo inclui os dados necessários para concluir este tutorial. Para baixar o banco de dados de exemplo, vá para [http://go.microsoft.com/fwlink/?LinkID=335807](http://go.microsoft.com/fwlink/?LinkID=335807).  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 ou posterior (para uso com o recurso Analisar no Excel na lição 11).  
  
## Lições  
Este tutorial inclui as seguintes lições:  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[Lição 1: Criar um novo projeto de modelo de tabela](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[Lição 2: Adicionar dados](../analysis-services/lesson-2-add-data.md)|20 minutos|  
|[Lição 3: Renomear colunas](../analysis-services/lesson-3-rename-columns.md)|20 minutos|  
|[Lição 4: Marcar como Tabela de Data](../analysis-services/lesson-4-mark-as-date-table.md)|3 minutos|  
|[Lição 5: Criar relações](../analysis-services/lesson-5-create-relationships.md)|10 minutos|  
|[Lição 6: Criar colunas calculadas](../analysis-services/lesson-6-create-calculated-columns.md)|15 minutos|  
|[Lição 7: Criar medidas](../analysis-services/lesson-7-create-measures.md)|30 minutos|  
|[Lição 8: Criar indicadores chave de desempenho](../analysis-services/lesson-8-create-key-performance-indicators.md)|15 minutos|  
|[Lição 9: Criar perspectivas](../Topic/Lesson%209:%20Create%20Perspectives.md)|5 minutos|  
|[Lição 10: Criar hierarquias](../analysis-services/lesson-10-create-hierarchies.md)|20 minutos|  
|[Lição 11: Criar partições](../analysis-services/lesson-11-create-partitions.md)|15 minutos|  
|[Lição 12: Criar funções](../analysis-services/lesson-12-create-roles.md)|15 minutos|  
|[Lição 13: Analisar no Excel](../analysis-services/lesson-13-analyze-in-excel.md)|20 minutos|  
|[Lição 14: Implantar](../analysis-services/lesson-14-deploy.md)|5 minutos|  
  
## Lições complementares  
Este tutorial também inclui [Lições complementares](../Topic/Supplemental%20Lessons.md). Os tópicos desta seção não são necessários para concluir o tutorial, mas podem ser úteis para a melhor compreensão dos recursos de criação do modelo de tabela avançado.  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[Implementar a segurança dinâmica usando filtros de linha](../analysis-services/implement-dynamic-security-by-using-row-filters.md)|30 minutos|  
|[Configurar propriedades de relatório para relatórios do Power View](../analysis-services/configure-reporting-properties-for-power-view-reports.md)|30 minutos|  
  
## Próxima etapa  
Para iniciar o tutorial, vá para a primeira lição: [Lição 1: Criar um novo projeto de modelo de tabela](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
  
  
