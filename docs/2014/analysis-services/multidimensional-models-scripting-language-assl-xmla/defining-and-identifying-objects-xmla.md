---
title: Definindo e identificando objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bf4e15816a2b25ee9d346d38972be73f760f1a7d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115729"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definindo e identificando objetos (XMLA)
  Os objetos são identificados nos comandos XMLA (XML for Analysis) pela utilização de identificadores de objeto e de referências de objeto, definidas por elementos da ASSL (Analysis Services Scripting Language) e por comandos XMLA.  
  
## <a name="object-identifiers"></a>Identificadores de objeto  
 Um objeto é identificado usando o identificador exclusivo do objeto conforme definido em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Identificadores de objeto podem ser explicitamente especificados ou podem ser determinados pela instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria o objeto. Você pode usar o [Discover](../xmla/xml-elements-methods-discover.md) método para recuperar identificadores de objeto para subsequentes `Discover` ou [Execute](../xmla/xml-elements-methods-execute.md) chamadas de método.  
  
## <a name="object-references"></a>Referências de objeto  
 Vários comandos XMLA, como [excluir](../xmla/xml-elements-commands/delete-element-xmla.md) ou [processo](../xmla/xml-elements-commands/process-element-xmla.md), use uma referência de objeto para fazer referência a um objeto de uma maneira não ambígua. Uma referência de objeto contém o identificador do objeto no qual um comando é executado e os identificadores do objeto de seus ancestrais. Por exemplo, a referência de objeto de uma partição contém o identificador do objeto da partição, além de identificadores de objeto do grupo de medidas, do cubo e do banco de dados pais dessa partição.  
  
## <a name="object-definitions"></a>Definições do objeto  
 O [criar](../xmla/xml-elements-commands/create-element-xmla.md) e [Alter](../xmla/xml-elements-commands/alter-element-xmla.md) comandos no XMLA criam ou alteram, respectivamente, objetos em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância. As definições para os objetos são representadas por um [ObjectDefinition](../xmla/xml-elements-properties/objectdefinition-element-xmla.md) elemento que contém elementos da ASSL. Identificadores de objeto podem ser especificados explicitamente para todos os principais e muitos dos objetos secundários por meio de [ID](../xmla/xml-elements-properties/id-element-xmla.md) elemento. Se o elemento `ID` não for usado, a instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornecerá um identificador exclusivo, com uma convenção de nomenclatura que dependerá do objeto a ser identificado. Para obter mais informações sobre como usar o `Create` e `Alter` comandos para definir objetos, consulte [criando e alterando objetos &#40;XMLA&#41;](../xmla/xml-elements-objects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Elemento do objeto &#40;XMLA&#41;](../xmla/xml-elements-properties/object-element-xmla.md)   
 [Elemento ParentObject &#40;XMLA&#41;](../xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Elemento Source &#40;XMLA&#41;](../xmla/xml-elements-properties/source-element-xmla.md)   
 [Elemento de destino &#40;XMLA&#41;](../xmla/xml-elements-properties/target-element-xmla.md)   
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  