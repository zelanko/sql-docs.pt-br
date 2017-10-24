---
title: "Excluir uma exibição da fonte de dados (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting data source views
- data source views [Analysis Services], deleting
- removing data source views
ms.assetid: ae3f5ca0-ecbf-4b52-8386-eb457719d854
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fe61cd6bf489a51e0f42454146c999f5520a3a57
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="delete-a-data-source-view-analysis-services"></a>Excluir uma exibição da fonte de dados (Analysis Services)
  Se você não estiver mais usando uma DSV (exibição da fonte de dados) em um projeto OLAP, poderá excluí-la do projeto no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 A exclusão de uma DSV é permanente. Não é possível restaurar uma DSV excluída para um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 As DSVs das quais outros objetos dependem não podem ser excluídas de um banco de dados aberto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online. Para excluir uma DSV de um projeto que está conectado a um banco de dados executado em um servidor, você primeiro deve excluir todos os objetos no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependem da DSV antes de excluir a própria DSV.  
  
 Excluir uma DSV invalidará outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependem dela; portanto, antes de excluir a DSV, consulte a lista de objetos que ficarão inválidos quando a DSV for removida. Examine esta lista com cuidado para ter certeza de que ela não inclui objetos que você ainda espera usar.  
  
 ![Caixa de diálogo de objetos excluir](../../analysis-services/multidimensional-models/media/ssas-olapdsv-deleteobjects.gif "caixa de diálogo Excluir objetos")  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Alterar propriedades em uma exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  

