---
title: Definindo e identificando objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 595a792e515e862297389faccc324fff8727b8da
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147981"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definindo e identificando objetos (XMLA)
  Os objetos são identificados nos comandos XMLA (XML for Analysis) pela utilização de identificadores de objeto e de referências de objeto, definidas por elementos da ASSL (Analysis Services Scripting Language) e por comandos XMLA.  
  
## <a name="object-identifiers"></a>Identificadores de objeto  
 Um objeto é identificado usando o identificador exclusivo do objeto, conforme definido em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Identificadores de objeto podem ser explicitamente especificados ou podem ser determinados pela instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o objeto. Você pode usar o [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) método para recuperar identificadores de objeto para subsequentes `Discover` ou [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) chamadas de método.  
  
## <a name="object-references"></a>Referências de objeto  
 Vários comandos XMLA, como [exclua](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) ou [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla), use uma referência de objeto para se referir a um objeto de maneira não ambígua. Uma referência de objeto contém o identificador do objeto no qual um comando é executado e os identificadores do objeto de seus ancestrais. Por exemplo, a referência de objeto de uma partição contém o identificador do objeto da partição, além de identificadores de objeto do grupo de medidas, do cubo e do banco de dados pais dessa partição.  
  
## <a name="object-definitions"></a>Definições do objeto  
 O [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) e [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comandos no XMLA criam ou alteram, respectivamente, objetos em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. As definições para esses objetos são representadas por uma [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento que contém elementos da ASSL. Identificadores de objeto podem ser especificados explicitamente para todos os principais e muitos dos objetos secundários usando o [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) elemento. Se o elemento `ID` não for usado, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecerá um identificador exclusivo, com uma convenção de nomenclatura que dependerá do objeto a ser identificado. Para obter mais informações sobre como usar o `Create` e `Alter` comandos para definir objetos, consulte [criando e alterando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento do objeto &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento ParentObject &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento Source &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Elemento de destino &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
