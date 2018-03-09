---
title: Modelos de tabela | Microsoft Docs
ms.custom: 
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 2df607b47e4bb2a5a770e27d1bceb5a6d7e6ebbc
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/23/2018
---
# <a name="tabular-models"></a>Modelos de tabela
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
Os modelos Tabulares são bancos de dados do Analysis Services que são executados na memória ou no modo DirectQuery, acessando os dados diretamente a partir de fontes de dados relacionais de back-end. Usando algoritmos de compactação de última geração e processador de consulta multi-threaded, o mecanismo de análise fornece acesso rápido a dados e objetos de modelo tabular relatando aplicativos cliente, como o Power BI e Excel.  
  
 Embora modelos na memória são o padrão, o DirectQuery é um modo alternativo de consulta para modelos que são muito grandes para caber na memória, ou quando uma estratégia de processamento razoável impede a volatilidade dos dados. O DirectQuery atinge paridade com modelos na memória por meio do suporte para uma ampla variedade de fontes de dados, capacidade de lidar com tabelas calculadas e colunas em um modelo DirectQuery, a segurança em nível de linha por meio de expressões DAX que acessar o banco de dados de back-end e de consulta otimizações que resultam em uma taxa de transferência.
  
 Os modelos Tabulares são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o modelo de projeto de modelo Tabular que fornece uma superfície de design para criar um modelo, tabelas, relações e expressões DAX. Você pode importar dados de várias origens e enriquecer o modelo adicionando relações, colunas e tabelas calculadas, medidas, KPIs, hierarquias e traduções.  
  
 Modelos podem ser implantados com o Azure Analysis Services ou uma instância do SQL Server Analysis Services configurada para modo de servidor Tabular. Modelos de tabela implantados podem ser gerenciados no SQL Server Management Studio. Como os modelos de crescem, podem ser particionados para processamento otimizado e protegidos para o nível de linha usando segurança baseada em função.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Soluções de modelo tabular](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md) -artigos nesta seção descrevem a criar e implantar soluções de modelo tabular.
  
 [Bancos de dados de modelo de tabela](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md) -artigos nesta seção descrevem o gerenciamento de soluções de modelo tabular implantado.
  
 [Acesso de dados de modelo de tabela](../../analysis-services/tabular-models/tabular-model-data-access.md) -artigos nesta seção descrevem a se conectar ao implantado soluções de modelo tabular.
  
## <a name="see-also"></a>Consulte também  
 [Novidades no Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Comparando soluções tabulares e multidimensionais](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Ferramentas e aplicativos usados no Analysis Services](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Nível de compatibilidade](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
