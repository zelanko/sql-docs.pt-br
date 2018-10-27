---
title: Definindo e identificando objetos (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 48223f9718ae4eb87b0880c2f266c886ec7abbb0
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145262"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definindo e identificando objetos (XMLA)
  Os objetos são identificados nos comandos XMLA (XML for Analysis) pela utilização de identificadores de objeto e de referências de objeto, definidas por elementos da ASSL (Analysis Services Scripting Language) e por comandos XMLA.  
  
## <a name="object-identifiers"></a>Identificadores de objeto  
 Um objeto é identificado usando o identificador exclusivo do objeto, conforme definido em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Identificadores de objeto podem ser explicitamente especificados ou podem ser determinados pela instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o objeto. Você pode usar o [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) método para recuperar identificadores de objeto para subsequentes **Discover** ou [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) chamadas de método.  
  
## <a name="object-references"></a>Referências de objeto  
 Vários comandos XMLA, como [exclua](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) ou [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla), use uma referência de objeto para se referir a um objeto de maneira não ambígua. Uma referência de objeto contém o identificador do objeto no qual um comando é executado e os identificadores do objeto de seus ancestrais. Por exemplo, a referência de objeto de uma partição contém o identificador do objeto da partição, além de identificadores de objeto do grupo de medidas, do cubo e do banco de dados pais dessa partição.  
  
## <a name="object-definitions"></a>Definições do objeto  
 O [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) e [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comandos no XMLA criam ou alteram, respectivamente, objetos em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. As definições para esses objetos são representadas por uma [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento que contém elementos da ASSL. Identificadores de objeto podem ser especificados explicitamente para todos os principais e muitos dos objetos secundários usando o [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) elemento. Se o **identificação** elemento não for usado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância fornece um identificador exclusivo, com uma convenção de nomenclatura que depende do objeto a ser identificado. Para obter mais informações sobre como usar o **Create** e **Alter** comandos para definir objetos, consulte [criando e alterando objetos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento do objeto &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento ParentObject &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento Source &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Elemento de destino &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
