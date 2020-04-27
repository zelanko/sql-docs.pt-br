---
title: Definindo e identificando objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: ad6c8de47577eccd7797517c8080957d7afe1abd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727526"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definindo e identificando objetos (XMLA)
  Os objetos são identificados nos comandos XMLA (XML for Analysis) pela utilização de identificadores de objeto e de referências de objeto, definidas por elementos da ASSL (Analysis Services Scripting Language) e por comandos XMLA.  
  
## <a name="object-identifiers"></a>Identificadores de objeto  
 Um objeto é identificado usando o identificador exclusivo do objeto, conforme definido em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Identificadores de objeto podem ser explicitamente especificados ou podem ser determinados pela instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o objeto. Você pode usar o método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) para recuperar identificadores de objeto para `Discover` as chamadas de método subsequentes ou [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
## <a name="object-references"></a>Referências de objeto  
 Vários comandos XMLA, como [delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) ou [process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla), usam uma referência de objeto para se referir a um objeto de maneira não ambígua. Uma referência de objeto contém o identificador do objeto no qual um comando é executado e os identificadores do objeto de seus ancestrais. Por exemplo, a referência de objeto de uma partição contém o identificador do objeto da partição, além de identificadores de objeto do grupo de medidas, do cubo e do banco de dados pais dessa partição.  
  
## <a name="object-definitions"></a>Definições do objeto  
 Os comandos [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) e [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) no XMLA Create ou ALTER, respectivamente, objetos em uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. As definições desses objetos são representadas por um elemento [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) que contém elementos de ASSL. Os identificadores de objeto podem ser especificados explicitamente para todos os principais e muitos objetos secundários usando o elemento [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) . Se o elemento `ID` não for usado, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecerá um identificador exclusivo, com uma convenção de nomenclatura que dependerá do objeto a ser identificado. Para obter mais informações sobre como usar os `Create` comandos `Alter` e para definir objetos, consulte [criando e alterando objetos &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento Object &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento ParentObject &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento de origem &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Elemento de destino &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
