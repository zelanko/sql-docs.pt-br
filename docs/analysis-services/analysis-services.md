---
title: Sobre o SQL Server Analysis Services | Microsoft Docs
ms.date: 12/05/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: overview
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2cd892ad41beba2b5715b3a7186ae5e44bb7911
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63206358"
---
# <a name="about-sql-server-analysis-services"></a>Sobre o SQL Server Analysis Services

Analysis Services é um mecanismo de dados analíticos usado na análise de negócios e suporte de decisão. Ele fornece modelos de dados semânticos empresarial para relatórios de negócios e aplicativos cliente, como relatórios do Power BI, Excel, relatórios de serviços e outras ferramentas de visualização de dados.

Um fluxo de trabalho típico inclui criar um projeto de modelo de dados tabular ou multidimensional no Visual Studio, implantar o modelo como um banco de dados para uma instância de servidor, como configurar o processamento de dados recorrente e atribuir permissões para permitir o acesso a dados pelos usuários finais. Quando ele estiver pronto para começar, seu modelo de dados semântico pode ser acessado por aplicativos cliente com suporte do Analysis Services como fonte de dados.

Analysis Services está disponível em duas diferentes plataformas:

**O Azure Analysis Services** -dá suporte a modelos tabulares nos níveis de compatibilidade 1200 e superior. DirectQuery, partições, segurança de nível de linha, relações bidirecionais e traduções todas têm suporte. Para obter mais informações, consulte [do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).

**SQL Server Analysis Services** -dá suporte a modelos de tabela em todos os níveis de compatibilidade, modelos multidimensionais, mineração de dados e do Power Pivot para SharePoint.

## <a name="documentation-by-area"></a>Documentação por área

Em geral, [documentação do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/) está incluído com a documentação do Azure. Se você estiver interessado em ter seus modelos de tabela na nuvem, é melhor começar por aqui. Neste artigo e a documentação nesta seção é principalmente para SQL Server Analysis Services. No entanto, pelo menos para modelos de tabela, como criar e implantar seus projetos de modelo tabular é muito parecidas, independentemente da plataforma que você está usando. Confira essas seções para saber mais:

- [Comparando soluções tabulares e multidimensionais](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)
- [Instalar o SQL Server Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md)
- [Modelos de tabela](../analysis-services/tabular-models/tabular-models-ssas.md)
- [Modelos multidimensionais](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)
- [Mineração de Dados](../analysis-services/data-mining/data-mining-ssas.md)
- [Power Pivot para SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)
- [Tutoriais](../analysis-services/analysis-services-tutorials-ssas.md)
- [Gerenciamento de servidor](../analysis-services/instances/analysis-services-instance-management.md)
- [Documentação do desenvolvedor](analysis-services-developer-documentation.md)
- [Referência técnica](https://docs.microsoft.com/bi-reference/)

#### <a name="see-also"></a>Confira também

[Documentação do Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
[documentação do SQL Server](../sql-server/sql-server-technical-documentation.md)
