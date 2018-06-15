---
title: Excluir uma exibição da fonte de dados (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3b3486aacb727f002b004d079f5e4a17f235ef9c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022373"
---
# <a name="delete-a-data-source-view-analysis-services"></a>Excluir uma exibição da fonte de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se você não estiver mais usando uma DSV (exibição da fonte de dados) em um projeto OLAP, poderá excluí-la do projeto no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 A exclusão de uma DSV é permanente. Não é possível restaurar uma DSV excluída para um projeto ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 As DSVs das quais outros objetos dependem não podem ser excluídas de um banco de dados aberto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pelo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] em modo online. Para excluir uma DSV de um projeto que está conectado a um banco de dados executado em um servidor, você primeiro deve excluir todos os objetos no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependem da DSV antes de excluir a própria DSV.  
  
 Excluir uma DSV invalidará outros objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependem dela; portanto, antes de excluir a DSV, consulte a lista de objetos que ficarão inválidos quando a DSV for removida. Examine esta lista com cuidado para ter certeza de que ela não inclui objetos que você ainda espera usar.  
  
 ![Caixa de diálogo de objetos excluir](../../analysis-services/multidimensional-models/media/ssas-olapdsv-deleteobjects.gif "caixa de diálogo Excluir objetos")  
  
## <a name="see-also"></a>Consulte também  
 [Exibições da fonte de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Alterar propriedades em uma exibição da fonte de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
