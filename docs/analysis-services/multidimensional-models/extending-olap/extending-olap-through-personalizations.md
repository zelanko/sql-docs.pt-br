---
title: Estendendo OLAP por meio de personalizações | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a8c5cda445e9dc7b67fa2a646909918f152d1fbd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="extending-olap-through-personalizations"></a>Estendendo OLAP por meio de personalizações
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Analysis Services fornece muitas funções intrínsecas para uso com as linguagens MDX (Multidimensional Expressions) e extensões DMX (Data Mining). Essas funções são designadas para executar todas as operações, desde cálculos estatísticos padrão ao desvio de membros em uma hierarquia. No entanto, como em qualquer outro produto complexo, há sempre a necessidade de estender a funcionalidade para o produto.  
  
 Assim, o Analysis Services oferece a capacidade de adicionar assemblies e extensões personalizadas a uma instância do serviço, para atender suas necessidades comerciais sempre que a funcionalidade padrão não for suficiente.  
  
## <a name="assemblies"></a>Assemblies  
 Os assemblies permitem estender a funcionalidade empresarial de MDX e DMX. É possível criar a funcionalidade desejada em uma biblioteca, como uma DLL (biblioteca de vínculo dinâmico) e adicionar a biblioteca como um assembly a uma instância ou a um banco de dados do Analysis Services. Em seguida, os métodos públicos na biblioteca são expostos como funções definidas pelo usuário para expressões MDX e DMX, procedimentos, cálculos, ações e aplicativos cliente.  
  
## <a name="personalized-extensions"></a>Extensões personalizadas  
 As extensões de personalização do SQL Server Analysis Services são a base do conceito de implementação de uma arquitetura de plug-in. As extensões de personalização do Analysis Services fazem uma modificação simples e discreta na arquitetura de assemblies gerenciados existente e são expostas através do modelo de objeto <xref:Microsoft.AnalysisServices.AdomdServer> do Analysis Services, da sintaxe MDX e de conjuntos de linhas de esquema.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de Assemblies de modelo multidimensional](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Extensões de personalização do Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
  
