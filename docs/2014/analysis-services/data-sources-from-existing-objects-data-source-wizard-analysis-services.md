---
title: Fontes de dados de objetos existentes (Assistente de fonte de dados) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourcewizard.specifyobject.f1
ms.assetid: e6ef6dea-9db8-45c4-8959-f9febd7caf7b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5576e997023e5a00cdecc3c2079ce387c7062ebb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082375"
---
# <a name="data-sources-from-existing-objects-data-source-wizard-analysis-services"></a>Fontes de dados de objetos existentes (Assistente para Fonte de Dados) (Analysis Services)
  Use a página **Fontes de dados de objetos existentes** para especificar uma fonte de dados ou projeto existente no qual basear a nova fonte de dados.  
  
## <a name="options"></a>Opções  
 **Criar uma fonte de dados com base em uma fonte de dados existente em sua solução**  
 Selecione para basear a nova fonte de dados em uma fonte de dados existente na solução. Quando um projeto que usa a nova fonte de dados é criado, atualizado ou implantado, a nova fonte de dados adquire as configurações da origem de dados especificada quando essa opção é selecionada.  
  
 **Fonte de dados**  
 Selecione a fonte de dados na qual basear a nova fonte de dados na lista de fontes de dados que é agrupada por projeto.  
  
 **Criar uma fonte de dados com base em um projeto do Analysis Services**  
 Selecione para criar uma nova fonte de dados que faça [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] referência a outro projeto na solução atual. A nova fonte de dados adquire configurações das propriedades `TargetServer` e `TargetDatabase` do projeto selecionado. Quando um projeto que usa a nova fonte de dados é criado, atualizado ou implantado, a nova fonte de dados adquire as configurações da origem de dados especificada quando essa opção é selecionada.  
  
 **Project**  
 Selecione o projeto que você quer referenciar na nova fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de fonte de dados &#40;Analysis Services&#41;](data-source-wizard-f1-help-analysis-services.md)   
 [Fontes de dados em modelos multidimensionais](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Fontes de dados com suporte &#40;SSAS multidimensional&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
