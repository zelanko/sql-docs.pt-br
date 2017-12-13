---
title: Desenvolvimento com o Analysis Services Scripting Language (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45b116586a0ce328815d8139b751547045fa85f8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Desenvolvendo com ASSL (linguagem de script do Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Analysis Services Scripting Language (ASSL) é uma extensão ao XMLA que adiciona uma linguagem de definição de objeto e linguagem de comandos para criar e gerenciar estruturas do Analysis Services diretamente no servidor. Você pode usar o ASSL em um aplicativo personalizado para comunicar-se com o Analysis Services em um protocolo XMLA. O ASSL é composto de duas partes:  
  
-   Uma DDL (Linguagem de Definição de Dados), ou linguagem de definição de objeto, define e descreve uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], além de bancos de dados e de objetos de banco de dados contidos na instância.  
  
-   Uma linguagem de comandos que envia comandos de ação, como **criar**, **Alter**, ou **processo**, para uma instância do Analysis Services. Essa linguagem de comandos é discutida no [XML for Analysis &#40; XMLA &#41; Referência](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md).  
  
 Para exibir o ASSL que descreve uma solução multidimensional no [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], você pode usar o comando de Código de Exibição no nível do projeto. Ainda é possível criar ou editar script ASSL no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] usando o editor de consultas XMLA. Os scripts que você cria podem ser usados para gerenciar objetos ou executar comandos no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [Convenções de XML do ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [Fontes de dados e associações &#40; SSAS Multidimensional &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
