---
title: Elemento ALTER (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Alter Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70986afb0f916e150ec203e3beb48684d9902f02
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-element-xmla"></a>Elemento Alter (XMLA)
  Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método para alterar objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Alter Scope="enum" AllowCreate="boolean" ObjectExpansion="enum">  
      <Object>...</Object>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Alter>  
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
|Elementos filho|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|AllowCreate|(Atributo **Boolean** opcional) Indica se os objetos definidos no comando **Alter** devem ser criados se ainda não existirem.<br /><br /> Se definido como true, os objetos definidos no **ObjectDefinition** criadas no elemento de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância se eles ainda não existir. Em outras palavras, o comando **Alter** é tratado como um comando **Create** se os objetos ainda não existirem na instância.<br /><br /> Se esse atributo for omitido ou definido como **false**, ocorrerá um erro se os objetos ainda não existirem.|  
|ObjectExpansion|(Atributo **Enum** opcional) Define a extensão da alteração a ser executada pelo método **Execute** .<br /><br /> Se for definido como *ObjectProperties*, o elemento **ObjectDefinition** deve conter somente a definição completa do principal objeto a ser alterado, incluindo os objetos menores subordinados. Os objetos grandes subordinados ao objeto a ser alterado permanecem iguais.<br /><br /> Observação: Ao usar o *ObjectProperties* configuração com o [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) tipo de dados, o [dados](../../../analysis-services/scripting/objects/data-element-assl.md) elemento associado [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) tipos de dados não precisa ser especificado. Se não for especificado, o elemento **ClrAssembly** usará os arquivos existentes.<br /><br /> Se for definido como *ExpandFull*, o elemento **ObjectDefinition** não deve conter apenas a definição do objeto a ser alterado, mas também as definições de todos os principais objetos que são descendentes do objeto a ser alterado.<br /><br /> Observação: O *ExpandFull* configuração não pode ser usada com a [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|Escopo|(Atributo **Enum** opcional) Define a duração dos objetos definidos no elemento **ObjectDefinition** .<br /><br /> Se for definido como *Session*, os objetos definidos no elemento **ObjectDefinition** existirão somente durante a sessão XMLA.<br /><br /> Observação: Ao usar o *sessão* configuração, o **ObjectDefinition** elemento só pode conter [dimensão](../../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), ou [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.<br /><br /> Se esse atributo for omitido, os objetos definidos no **ObjectDefinition** elemento são mantidos no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.|  
  
## <a name="remarks"></a>Comentários  
 Cada **Alter** comando altera a definição de um objeto principal sob o objeto pai especificado o [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

