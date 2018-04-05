---
title: Elemento Create (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Create Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f3e568fb190940822a6c6ef5cb65cf6b9476f4b1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="create-element-xmla"></a>Elemento Create (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo **Execute** método para criar objetos em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
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
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|AllowOverwrite|Atributo **Boolean** opcional. Se definido como True, os objetos definidos no **ObjectDefinition** elemento pode substituir objetos existentes na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. Se esse atributo for omitido ou definido como False, a presença de um objeto existente gerará um erro.|  
|Escopo|Atributo **Enum** opcional. Define a duração de objetos definida no elemento **ObjectDefinition** . Se esse atributo for omitido, os objetos definidos no **ObjectDefinition** elemento são mantidos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O valor a seguir está disponível:<br /><br /> *Sessão*: os objetos definidos no **ObjectDefinition** elemento existe apenas para a duração do XML para a sessão de análise (XMLA).<br />                  Observe que ao usar o *sessão* configuração, o **ObjectDefinition** elemento só pode conter [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), ou [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.|  
  
## <a name="remarks"></a>Remarks  
 Cada operação **Create** cria um objeto principal sob um pai fornecido pelo elemento **ParentObject** . Se o objeto pai for omitido, será considerada a instância de destino [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Isso gerará um erro se o pai de um objeto principal não for a instância de destino.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um banco de dados vazio chamado **banco de dados de teste** em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
