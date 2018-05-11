---
title: Elemento Create (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb4183c650c82123693e3d217e52e585130f4d36
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="create-element-xmla"></a>Elemento Create (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo **Execute** método para criar objetos em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
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
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|AllowOverwrite|Atributo **Boolean** opcional. Se definido como True, os objetos definidos no **ObjectDefinition** elemento pode substituir objetos existentes na [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. Se esse atributo for omitido ou definido como False, a presença de um objeto existente gerará um erro.|  
|Escopo|Atributo **Enum** opcional. Define a duração de objetos definida no elemento **ObjectDefinition** . Se esse atributo for omitido, os objetos definidos no **ObjectDefinition** elemento são mantidos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O valor a seguir está disponível:<br /><br /> *Sessão*: os objetos definidos no **ObjectDefinition** elemento existe apenas para a duração do XML para a sessão de análise (XMLA).<br />                  Observe que ao usar o *sessão* configuração, o **ObjectDefinition** elemento só pode conter [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), ou [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.|  
  
## <a name="remarks"></a>Remarks  
 Cada operação **Create** cria um objeto principal sob um pai fornecido pelo elemento **ParentObject** . Se o objeto pai for omitido, será considerada a instância de destino [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Isso gerará um erro se o pai de um objeto principal não for a instância de destino.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
