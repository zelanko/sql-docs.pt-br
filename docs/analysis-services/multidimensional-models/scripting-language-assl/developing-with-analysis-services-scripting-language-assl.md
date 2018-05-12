---
title: Desenvolvimento com o Analysis Services Scripting Language (ASSL) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1c01f567599353d360d8cf4a213e2abaa6c6cff
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Desenvolvendo com ASSL (linguagem de script do Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  ASSL (Linguagem de scripts do Analysis Services) é uma extensão ao XMLA que adiciona uma linguagem de definição de objeto e linguagem de comandos para criar e gerenciar as estruturas do Analysis Services diretamente no servidor. Você pode usar o ASSL em um aplicativo personalizado para comunicar-se com o Analysis Services em um protocolo XMLA. O ASSL é composto de duas partes:  
  
-   Uma DDL (Linguagem de Definição de Dados), ou linguagem de definição de objeto, define e descreve uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], além de bancos de dados e de objetos de banco de dados contidos na instância.  
  
-   Uma linguagem de comandos que envia comandos de ação, como **criar**, **Alter**, ou **processo**, para uma instância do Analysis Services. Essa linguagem de comandos é discutida no [XML for Analysis &#40;XMLA&#41; referência](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md).  
  
 Para exibir o ASSL que descreve uma solução multidimensional no [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], você pode usar o comando de Código de Exibição no nível do projeto. Ainda é possível criar ou editar script ASSL no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] usando o editor de consultas XMLA. Os scripts que você cria podem ser usados para gerenciar objetos ou executar comandos no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Objetos e características de objeto ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [Convenções de XML do ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [Fontes de dados e associações & #40; SSAS Multidimensional & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
