---
title: Analysis Services | Microsoft Docs
ms.date: 05/11/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: "60"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 0a11280eca74da75737d30fe795c856988d422ae
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="what-is-analysis-services"></a>Novidades do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]Analysis Services é um mecanismo de dados analíticos usado em suporte a decisões e análise de negócios, fornecendo os dados analíticos para relatórios de negócios e aplicativos cliente, como o Power BI, Excel, relatórios do Reporting Services e outras ferramentas de visualização de dados.  
  
 Um fluxo de trabalho típico inclui a criação de um modelo de dados multidimensional ou tabular, implantando o modelo como um banco de dados a uma instância de servidor local do SQL Server Analysis Services ou do Azure Analysis Services, configurar o processamento de dados recorrente e atribuir permissões para permitir o acesso a dados por usuários finais. Quando ele estiver pronto, o modelo de semântica de dados pode ser acessado por qualquer aplicativo cliente com suporte do Analysis Services como uma fonte de dados.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services local e na nuvem
Analysis Services agora está disponível na nuvem como um serviço do Azure. Serviços de análise do Azure oferece suporte a modelos de tabela nos níveis de compatibilidade 1200 e superior. DirectQuery, partições, segurança de nível de linha, relações bidirecionais e traduções todas têm suporte. Para saber mais e experimentar gratuitamente, consulte [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Modo do Servidor  
 Ao instalar o Analysis Services usando a instalação do SQL Server, durante a configuração você especificar um modo de servidor para essa instância.  Cada modo inclui diferentes recursos exclusivos para uma solução específica do Analysis Services.   
  
-   **Modo de tabela** - implementar na memória relacional modelagem de dados construções (modelo, tabelas, colunas, medidas, hierarquias).  

-   **Modo de mineração de dados e multidimensional** – Implemente construções de modelagem OLAP (cubos, dimensões, medidas). 

-   **Power Pivot Mode** -modelos de dados de implementar o Power Pivot e do Excel no SharePoint (PowerPivot para SharePoint é um mecanismo de dados de camada intermediária que carrega, consulta e atualiza modelos de dados hospedados no SharePoint).  
  
 Uma única instância pode ser configurada com apenas um modo, e não pode ser alterada posteriormente.  Você pode instalar várias instâncias com modos diferentes no mesmo servidor, mas precisará executar a Instalação e especificar as definições de configuração para cada instância. Para obter informações detalhadas e uma comparação de diferentes recursos oferecidos em cada um dos modos, consulte [comparando tabulares e multidimensionais soluções](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).
  
## <a name="authoring-and-managing-solutions"></a>Criação e gerenciamento de soluções  
 Para criar um modelo e implantá-lo em um servidor, você deve usar as ferramentas de dados do SQL Server, escolha uma tabela ou Multidimensional e mineração de dados modelo de projeto. O modelo de projeto contém pastas de todos os objetos necessários em um modelo. Designers e assistentes o ajudam a criar muitos dos elementos básicos, como se conectar a fontes de dados, relações, medidas e funções. Depois que o banco de dados de modelo é implantado em um servidor, você usar o SQL Server Management Studio (SSMS) para configurar o processamento de dados, monitorar e gerenciar o servidor e bancos de dados. Para obter mais informações, consulte [ferramentas e aplicativos usados no Analysis Services](../analysis-services/tools-and-applications-used-in-analysis-services.md). 
  
## <a name="documentation-by-area"></a>Documentação por área  
Em geral, a documentação do Azure Analysis Services está incluída com a documentação do Azure. E, documentação do SQL Server Analysis Services está incluída na documentação do SQL. No entanto, pelo menos para modelos de tabela, como criar e implantar seus projetos é muito o mesmo, independentemente da plataforma que você está usando.  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [O que há de novo no SQL Server Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)   
*  [Comparando soluções tabulares e multidimensionais](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [Modelos de Tabela](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [Modelos Multidimensionais](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [Mineração de Dados](../analysis-services/data-mining/data-mining-ssas.md)  
*  [PowerPivot para SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [Gerenciamento de instâncias](../analysis-services/instances/analysis-services-instance-management.md)    
*  [Tutoriais](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [Documentação do desenvolvedor](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [Referência técnica (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)
