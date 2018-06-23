---
title: Elemento ALTER (XMLA) | Microsoft Docs
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
- Alter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5ea2c3ed3105c66b0c0848138acb5941978dd9bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013192"
---
# <a name="alter-element-xmla"></a>Elemento Alter (XMLA)
  Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo [Execute](../xml-elements-methods-execute.md) método para alterar objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[Objeto](../xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|AllowCreate|(Atributo `Boolean` opcional) Indica se os objetos definidos no comando `Alter` devem ser criados se ainda não existirem.<br /><br /> Se for definido como True, os objetos definidos no elemento `ObjectDefinition` serão criados na instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] se ainda não existirem. Em outras palavras, o comando `Alter` é tratado como um comando `Create` se os objetos ainda não existirem na instância.<br /><br /> Se esse atributo for omitido ou definido como `false`, ocorrerá um erro se os objetos ainda não existirem.|  
|ObjectExpansion|(Atributo `Enum` opcional) Define a extensão da alteração a ser executada pelo método `Execute`.<br /><br /> Se definido como *ObjectProperties*, o `ObjectDefinition` elemento deve conter somente a definição completa do principal objeto a ser alterado, incluindo os objetos menores subordinados. Os objetos grandes subordinados ao objeto a ser alterado permanecem iguais. **Observação:** ao usar o *ObjectProperties* configuração com o [ClrAssembly](../../scripting/data-type/assembly-data-type-assl.md) tipo de dados, o [dados](../../scripting/objects/data-element-assl.md) elemento associado [ ClrAssemblyFile](../../scripting/data-type/clrassemblyfile-data-type-assl.md) tipos de dados não precisa ser especificado. Se não for especificado, o elemento `ClrAssembly` usará os arquivos existentes. <br /><br /> Se definido como *ExpandFull*, o `ObjectDefinition` elemento deve conter não apenas a definição do objeto a ser alterado, mas também as definições de todos os principais objetos que são descendentes do objeto a ser alterado. **Observação:** o *ExpandFull* configuração não pode ser usada com a [Server](../../scripting/objects/server-element-assl.md) elemento.|  
|Escopo|(Atributo `Enum` opcional) Define a duração dos objetos definidos no elemento `ObjectDefinition`.<br /><br /> Se definido como *sessão*, os objetos definidos no `ObjectDefinition` elemento existe apenas para a duração da sessão XMLA. **Observação:** ao usar o *sessão* configuração, o `ObjectDefinition` elemento só pode conter [dimensão](../../scripting/objects/dimension-element-assl.md), [cubo](../../scripting/objects/cube-element-assl.md), ou [MiningModel ](../../scripting/objects/miningmodel-element-assl.md) Elementos ASSL. <br /><br /> Se este atributo for omitido, os objetos definidos no elemento `ObjectDefinition` persistirão na instância [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
## <a name="remarks"></a>Remarks  
 Cada `Alter` comando altera a definição de um objeto principal sob o objeto pai especificado o [ParentObject](../xml-elements-properties/parentobject-element-xmla.md) elemento.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  