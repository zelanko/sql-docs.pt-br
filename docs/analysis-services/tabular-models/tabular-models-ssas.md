---
title: Modelos de tabela (SSAS) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f1f324d1ba1b4ba9299c4d29e565d09d1f71fb2c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-modeling-ssas"></a>Modelagem tabular (SSAS)
  Os modelos Tabulares são bancos de dados do Analysis Services que são executados na memória ou no modo DirectQuery, acessando os dados diretamente a partir de fontes de dados relacionais de back-end.  
  
 Na memória é o padrão. Usando algoritmos de compactação de última geração e processador de consulta multi-threaded, o mecanismo de análise na memória oferece acesso rápido a objetos e dados modelo tabular relatando aplicativos cliente como o Microsoft Excel e o Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
 O DirectQuery é um modo alternativo de consulta para modelos que são muito grandes para caber na memória, ou quando uma estratégia de processamento razoável impede a volatilidade dos dados. Nesta versão, o DirectQuery atinge mais paridade com modelos na memória por meio do suporte a fontes de dados adicionais, da capacidade de manipular colunas e tabelas calculadas em um modelo DirectQuery, da segurança em nível de linha por meio de expressões DAX, que acessam o banco de dados de back-end, e por meio de otimizações da consulta que resultam em uma taxa de transferência mais rápida em relação às versões anteriores.
  
 Os modelos Tabulares são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usando o modelo de projeto de modelo Tabular que fornece uma superfície de design para criar um modelo, tabelas, relações e expressões DAX. Você pode importar dados de várias origens e enriquecer o modelo adicionando relações, colunas e tabelas calculadas, medidas, KPIs, hierarquias e traduções.  
  
 Os modelos podem ser implantados em uma instância do Analysis Services configurada para o modo do servidor Tabular, na qual os aplicativos de relatório de cliente podem conectar-se a eles. Os modelos implantados podem ser gerenciados n SQL Server Management Studio da mesma forma que modelos multidimensionais. Eles também podem ser particionados para processamento otimizado e protegido no nível de linha usando segurança baseada em função.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Soluções de modelo de tabela &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md) – os tópicos nesta seção descrevem a criação e implantação de soluções de modelo de tabela.
  
 [Bancos de dados de modelo de tabela &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md) – os tópicos nesta seção descrevem a criação e implantação de soluções de modelo de tabela.
  
 [Acesso aos dados do modelo tabular](../../analysis-services/tabular-models/tabular-model-data-access.md) – os tópicos nesta seção descrevem a conexão a soluções de modelo de tabela implantadas.
  
## <a name="see-also"></a>Consulte também  
 [Novidades do Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Comparando soluções tabulares e multidimensionais &#40;SSAS&#41;](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Ferramentas e aplicativos usados no Analysis Services](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [Modo DirectQuery &#40;SSAS de tabela&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Nível de compatibilidade para modelos de tabela no Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  

