---
title: Desenvolvimento com o Analysis Services Scripting Language (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1e12f03e96618a530c4f62f6a26cca904efeb43c
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145571"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Desenvolvendo com ASSL (linguagem de script do Analysis Services)
  ASSL (Linguagem de scripts do Analysis Services) é uma extensão ao XMLA que adiciona uma linguagem de definição de objeto e linguagem de comandos para criar e gerenciar as estruturas do Analysis Services diretamente no servidor. Você pode usar o ASSL em um aplicativo personalizado para comunicar-se com o Analysis Services em um protocolo XMLA. O ASSL é composto de duas partes:  
  
-   Uma DDL (Linguagem de Definição de Dados), ou linguagem de definição de objeto, define e descreve uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], além de bancos de dados e de objetos de banco de dados contidos na instância.  
  
-   Uma linguagem de comandos que envia comandos de ação, como `Create`, `Alter`ou `Process`, para uma instância do Analysis Services. Essa linguagem de comandos é discutida a [XML for Analysis &#40;XMLA&#41; referência](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Para exibir o ASSL que descreve uma solução multidimensional no [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], você pode usar o comando de Código de Exibição no nível do projeto. Ainda é possível criar ou editar script ASSL no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] usando o editor de consultas XMLA. Os scripts que você cria podem ser usados para gerenciar objetos ou executar comandos no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos e características de objeto ASSL](assl-objects-and-object-characteristics.md)   
 [Convenções de XML do ASSL](assl-xml-conventions.md)   
 [Fontes de dados e associações &#40;SSAS multidimensional&#41;](../data-sources-and-bindings-ssas-multidimensional.md)  
  
  
