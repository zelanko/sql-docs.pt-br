---
title: Sobre o SQL Server Analysis Services | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: overview
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 704c2f1638676bd838c7aac367a1b610143fd85d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="about-sql-server-analysis-services"></a>Sobre o SQL Server Analysis Services

Analysis Services é um mecanismo de dados analíticos usado na análise de negócios e suporte de decisão. Ele fornece modelos de semântica de dados empresariais para relatórios de negócios e aplicativos cliente, como o Power BI, Excel, Reporting Services relatórios e outras ferramentas de visualização de dados.  

Um fluxo de trabalho típico inclui criando um projeto de modelo de dados tabular ou multidimensional no Visual Studio, implantando o modelo como um banco de dados para uma instância de servidor, configurar o processamento de dados recorrente e atribuir permissões para permitir o acesso a dados por usuários finais. Quando estiver pronto para começar, o modelo de dados semântico pode ser acessado por aplicativos cliente com suporte do Analysis Services como uma fonte de dados.  

Analysis Services está disponível em duas diferentes plataformas: 

**Serviços de análise do Azure** -dá suporte a modelos de tabela nos níveis de compatibilidade 1200 e superior. DirectQuery, partições, segurança de nível de linha, relações bidirecionais e traduções todas têm suporte. Para obter mais informações, consulte [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).

**SQL Server Analysis Services** -dá suporte a modelos de tabela em todos os níveis de compatibilidade, modelos multidimensionais, mineração de dados e o PowerPivot para SharePoint.
 
 ## <a name="documentation-by-area"></a>Documentação por área  
Em geral, [documentação do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/) está incluído com a documentação do Azure. Se você estiver interessado em seus modelos de tabela que tem na nuvem, é melhor iniciar de lá. Esse artigo e a documentação nesta seção é principalmente para o SQL Server Analysis Services. No entanto, pelo menos para modelos de tabela, como criar e implantar seus projetos de modelo de tabela é muito o mesmo, independentemente da plataforma que você está usando. Consulte estas seções para obter mais informações:

   
*  [Comparando soluções tabulares e multidimensionais](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [Instalar o SQL Server Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md)
*  [Modelos de tabela](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [Modelos multidimensionais](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [Mineração de dados](../analysis-services/data-mining/data-mining-ssas.md)  
*  [Power Pivot para SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [Tutoriais](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [Gerenciamento de servidor](../analysis-services/instances/analysis-services-instance-management.md)    
*  [Documentação do desenvolvedor](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [Referência técnica](../analysis-services/powershell/technical-reference-ssas.md)

Consulte também

[Documentação do Azure do Analysis Services](https://docs.microsoft.com/azure/analysis-services/)   
[SQL Server, documentação](../sql-server/sql-server-technical-documentation.md)
