---
title: Elemento Create (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Create Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 17
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 19e7673c63d7e305d706efb910222f8ba0da7215
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119792"
---
# <a name="create-element-xmla"></a>Elemento Create (XMLA)
  Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo `Execute` método para criar objetos em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|AllowOverwrite|Opcional `Boolean` atributo. Se definido como True, os objetos definidos no elemento `ObjectDefinition` podem substituir existindo objetos na instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Se esse atributo for omitido ou definido como False, a presença de um objeto existente gerará um erro.|  
|Escopo|Opcional `Enum` atributo. Define a duração de objetos definida no elemento `ObjectDefinition`. Se este atributo for omitido, os objetos definidos no elemento `ObjectDefinition` persistirão na instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Os seguintes valores estão disponíveis:<br /><br /> -   *sessão*<br />     Os objetos definidos no elemento `ObjectDefinition` só existem para a duração da sessão XMLA (XML for Analysis). **Observação:** ao usar o *sessão* configuração, o `ObjectDefinition` elemento só pode conter [dimensão](../../scripting/objects/dimension-element-assl.md), [cubo](../../scripting/objects/cube-element-assl.md), ou [MiningModel ](../../scripting/objects/miningmodel-element-assl.md) Elementos ASSL.|  
  
## <a name="remarks"></a>Remarks  
 Cada operação `Create` cria um objeto principal sob um pai fornecido pelo elemento `ParentObject`. Se o objeto pai for omitido, será considerada a instância de destino [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Isso gerará um erro se o pai de um objeto principal não for a instância de destino.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um banco de dados vazio chamado `Test Database` em uma instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
```  
  
      <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
   <ObjectDefinition>  
      <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
         <Name>Test Database</Name>  
         <Description>A test database.</Description>  
      </Database>  
   </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  