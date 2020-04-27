---
title: Funcionalidade de Analysis Services descontinuada no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- discontinued functionality [Analysis Services]
- unsupported features [Analysis Services]
ms.assetid: 39406be1-9819-4629-9c29-b32fb20bab2e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 616c39d03ff8081c209a80dcca912d831bcef1ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081682"
---
# <a name="discontinued-analysis-services-functionality-in-sql-server-2014"></a>Funcionalidade descontinuada do Analysis Services no SQL Server 2014
  Este tópico descreve os recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-sssql14"></a>Recursos descontinuados no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
|Categoria|Recurso substituído|Substituição|  
|--------------|------------------------|-----------------|  
|Cubos locais|Propriedade da cadeia de conexão InsertInto|A sintaxe da cadeia de conexão original para popular cubos locais foi substituída pela instrução Criar Cubo Global. Para obter mais informações, consulte [criar instrução de cubo GLOBAL &#40;&#41;MDX ](/sql/mdx/mdx-data-definition-create-global-cube).|  
|Cubos locais|Propriedade da cadeia de conexão CreateCube|A sintaxe da cadeia de conexão original para popular cubos locais foi substituída pela instrução Criar Cubo Global. Para obter mais informações, consulte [criar instrução de cubo GLOBAL &#40;&#41;MDX ](/sql/mdx/mdx-data-definition-create-global-cube).|  
|Mineração de dados|SQL Server 2000 PMML|O recurso SQL Server 2000 PMML gerou um formulário de PMML que teve extensões proprietárias para dar suporte a recursos exclusivos fornecidos por algoritmos de Mineração de Dados que não estavam disponíveis na especificação PMML. No SQL Server 2005, o Analysis Services atualizou o recurso PMML para o padrão mais recente PMML 2.1. Como resultado, as extensões proprietárias adicionadas ao SQL Server 2000 não são mais necessárias, embora ainda tenham suporte nessa versão.|  
|Instrução MDX|Instrução Criar Ação|Esta instrução é incluída para compatibilidade com versões anteriores. Ela foi substituída pelo objeto Ação. Para obter mais informações sobre como criar ações em versões recentes do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], consulte [ações &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).|  
  
## <a name="discontinued-features-in-previous-releases"></a>Recursos descontinuados em versões anteriores  
 O Assistente de Migração, usado para migrar os bancos de dados do SQL Server 2000 Analysis Services para versões mais recentes, será descontinuado porque o SQL Server 2000 não conta mais com suporte.  
  
 A biblioteca DSO (Decision Support Objects) que fornecia compatibilidade com os bancos de dados do SQL Server 2000 Analysis Services também será descontinuada e não faz mais parte do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services Backward Compatibility](analysis-services-backward-compatibility.md)  
  
  
