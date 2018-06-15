---
title: Níveis de programação de modelo de tabela para fins de compatibilidade 1050 por meio de 1103 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1e14033255d45eaacda1d553c71224e11dfe964
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34039060"
---
# <a name="tabular-model-programming-for-compatibility-levels-1050-through-1103"></a>Programação de modelo de tabela para compatibilidade 1050 1103 por meio de níveis
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Os modelos tabulares usam construções relacionais para modelar os dados do Analysis Services usados aplicativos analíticos e de relatório. Esses modelos são executados em uma instância do Analysis Services que é configurada para o modo tabular, usando um mecanismo analítico na memória para armazenamento e análises rápidas de tabelas que agregam e calculam dados conforme necessário.  
  
 Se os requisitos de sua solução de BI personalizada forem atendidos da melhor forma por um banco de dados modelo, poderá usar qualquer uma das bibliotecas de cliente e interfaces de programação do Analysis Services para integrar seu aplicativo com modelos tabulares em uma instância do Analysis Services. Para consultar e calcular dados de modelos tabulares, é possível usar MDX ou DAX inserido no código.  
  
 Para modelos de tabela criados em versões anteriores do Analysis Services, em modelos específicos nos níveis de compatibilidade 1050 por meio de 1103, os objetos que você trabalha com programaticamente no AMO, ADOMD.NET, XMLA ou OLE DB são basicamente os mesmos para tabular e soluções multidimensionais. Especificamente, os metadados de objeto definido para modelos multidimensionais também é usado para níveis de compatibilidade de modelo tabular 1050-1103.  
  
 Começando com o SQL Server 2016, modelos de tabela podem ser criados ou atualizados para o nível de compatibilidade 1200 ou superior, que usa os metadados de tabela para definir o modelo. Metadados e programação são fundamentalmente diferentes nesse nível. Consulte [tabela de modelo de programação para 1200 de nível de compatibilidade e superior](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md) e [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) para obter mais informações.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Anotações CSDL para Business Intelligence & #40; CSDLBI & #41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
 [Noções básicas sobre o modelo de objeto de tabela em compatibilidade 1050 1103 por meio de níveis](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
 [Referência técnica para anotações de BI para CSDL](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  

[Interface IMDEmbeddedData](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/imdembeddeddata-interface.md)


  
  
