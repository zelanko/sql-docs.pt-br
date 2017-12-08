---
title: "A atualização dinâmica de dados de energia | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: ac8358a3-ee71-44c7-8ee6-ac7afe3ebaa4
caps.latest.revision: "24"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c5bc570e1f4f72fe932a8e5b2d0fa08c32f7949
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="power-pivot-data-refresh"></a>Atualização de Dados PowerPivot
  Depois de criar uma pasta de trabalho que contém dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , você pode atualizar os dados periodicamente executando novamente uma consulta ou um comando para obter informações atualizadas das origens usadas inicialmente para criar a pasta de trabalho. Esse processo é denominado **atualização de dados**, e você pode atualizar dados sob demanda no [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)]ou como uma operação agendada executada como um processo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em um servidor de aplicativos em um farm do SharePoint. Para obter mais informações, consulte:  
  
-   [Atualização de dados PowerPivot com o SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)  
  
-   [Configurar a conta da atualização de dados autônoma PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)  
  
-   [Configurar credenciais armazenadas para atualização de dados do Power Pivot (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75)  
  
-   [Agendar uma Atualização de Dados (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/8571208f-6aae-4058-83c6-9f916f5e2f9b)  
  
-   [Exibir o histórico de atualizações de dados &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]e serviços do Excel do SharePoint Server 2013 usam uma arquitetura diferente para a atualização de dados de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] modelos de dados. A arquitetura com suporte do SharePoint 2013 utiliza os Serviços do Excel como componente primário para carregar modelos de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . A arquitetura de atualização de dados anterior utilizada baseava-se em um servidor que executava o Serviço do Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no modo do SharePoint para carregar modelos de dados. Para obter mais informações, consulte o seguinte:  
>   
>  -   [Atualização de dados do Power Pivot com o SharePoint 2013](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md)  
> -   [Atualizar pastas de trabalho e a atualização de dados agendada &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md)  
  
  
