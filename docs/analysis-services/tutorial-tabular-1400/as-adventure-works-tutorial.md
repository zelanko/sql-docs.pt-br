---
title: Tutorial do Analysis Services Adventure Works (1400) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28aa401eb037fecadca17ededf041ab82a4bc498
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044570"
---
# <a name="tabular-modeling-1400-compatibility-level"></a>Modelagem de tabela (nível de compatibilidade 1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Este tutorial fornece lições sobre como criar e implantar um modelo de tabela no [o nível de compatibilidade 1400](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md). Se você estiver familiarizado com serviços de análise e modelagem de tabela, concluir este tutorial é a maneira mais rápida para aprender a criar e implantar um modelo de tabela básico usando o Visual Studio. Uma vez que os pré-requisitos no local, ele deve levar duas a três horas para ser concluído.  
  
## <a name="what-you-learn"></a>O que você aprenderá   
  
-   Como criar um novo projeto de modelo de tabela no **o nível de compatibilidade 1400** no Visual Studio com o SSDT.
  
-   Como importar dados de um banco de dados relacional para um banco de dados de espaço de trabalho de projeto de modelo de tabela.  
  
-   Como criar e gerenciar relações entre tabelas no modelo.  
  
-   Como criar colunas calculadas, medidas e indicadores chave de desempenho que ajudam os usuários a analisar métricas comerciais críticas.  
  
-   Como criar e gerenciar perspectivas e hierarquias que ajudam os usuários mais facilmente procurar dados de modelo, fornecendo pontos de vista específicos do aplicativo e de negócios.  
  
-   Como criar partições que dividem dados de tabela em partes lógicas menores que podem ser processadas independentemente de outras partições.  
  
-   Como proteger dados e objetos de modelo criando funções com membros de usuário.  
  
-   Como implantar um modelo de tabela para uma **Azure Analysis Services** server ou **2017 Analysis Services do SQL Server** server usando o SSDT.  
  
## <a name="prerequisites"></a>Prerequisites  

Para concluir este tutorial, você precisa:  
  
-   Um servidor do Azure Analysis Services ou um servidor do SQL Server de 2017 Analysis Services no modo de tabela. Inscreva-se para uma livre [avaliação do Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) e [criar um servidor](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) ou baixar um livre [2017 Developer Edition do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).

-   Um [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) com o **banco de dados de exemplo AdventureWorksDW**, ou um local no SQL Server Data Warehouse com uma [banco de dados de exemplo AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Ao instalar um banco de dados AdventureWorksDW local SQL Server Data warehouse, use a versão do banco de exemplo que corresponde com a versão do servidor. 

    **Importante:** se você instalar o banco de dados de exemplo para um local no SQL Server Data Warehouse e implantar seu modelo em um servidor de serviços de análise do Azure, uma [gateway de dados no local](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) é necessária.

-   A versão mais recente do [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). Ou, se você já tiver o Visual Studio de 2017, você pode baixar e instalar [projetos do Microsoft Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) pacote (VSIX). Para este tutorial, as referências a SSDT e o Visual Studio são sinônimos. 

-   A versão mais recente do [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Um aplicativo cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel. 

## <a name="scenario"></a>Cenário  

Este tutorial baseia-se em Adventure Works Cycles, uma empresa fictícia. A Adventure Works é uma empresa de fabricação grande, empresa multinacional que produz e distribui Bicicletas, peças e Acessórios para mercados comerciais na América do Norte, Europa e Ásia. Emprega 500 funcionários. Além disso, a Adventure Works emprega várias equipes regionais de vendas em toda a sua base de mercado. O projeto é criar um modelo de tabela para que os usuários de vendas e marketing analisar dados de vendas pela Internet no banco de dados AdventureWorksDW.  
  
Para concluir o tutorial, você deve concluir várias lições. Cada lição, há tarefas. Conclusão de cada tarefa na ordem é necessária para concluir a lição. Enquanto em uma lição específica pode haver várias tarefas que geram um resultado semelhante, mas como você conclui cada tarefa é ligeiramente diferente. Esse método mostra geralmente é mais de uma maneira para concluir uma tarefa e para desafiá-lo a usar as habilidades que você aprendeu em tarefas e lições anteriores.  
  
A finalidade das lições é orientar você durante a criação de um modelo de tabela básico usando muitos dos recursos incluídos no SSDT. Como cada lição é criada após a lição anterior, você deve concluir as lições na ordem.
  
Este tutorial não fornece lições sobre como gerenciar um servidor no portal do Azure, gerenciar um servidor ou banco de dados usando o SSMS, ou usando um aplicativo cliente para procurar dados de modelo. 


## <a name="lessons"></a>Lições  

Este tutorial inclui as seguintes lições:  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[1 - criar um novo projeto de modelo de tabela](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[2 - Obter dados](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10 minutos|  
|[3 - Marcar como Tabela de Data](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3 minutos|  
|[4 - Criar relações](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10 minutos|  
|[5 - Criar colunas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15 minutos|
|[6 - Criar medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30 minutos|  
|[7 - criar indicadores chave de desempenho (KPI)](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[8 - Criar perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5 minutos|  
|[9 - Criar hierarquias](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20 minutos|  
|[10 - Criar partições](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15 minutos|  
|[11 - Criar funções](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15 minutos|  
|[12 - Analisar no Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5 minutos| 
|[13 - Implantar](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lições complementares  

Nestas lições não são necessárias para concluir o tutorial, mas podem ser útil para melhor compreensão advanced criação de modelo tabular recursos.  
  
|Lição|Tempo estimado para concluir|  
|----------|------------------------------|  
|[Linhas de detalhes](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 minutos|
|[Segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 minutos|
|[Hierarquias desbalanceadas](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 minutos| 

  
## <a name="next-steps"></a>Próximas etapas  

Para começar, consulte [lição 1: criar um novo projeto de modelo de tabela](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

