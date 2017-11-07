---
title: Elemento Statement (XMLA) | Microsoft Docs
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
- Statement Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Statement
- microsoft.xml.analysis.statement
- urn:schemas-microsoft-com:xml-analysis#Statement
helpviewer_keywords:
- Statement command
ms.assetid: bfedc03c-d476-4d55-b5fd-36169f01351a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 172e9961945bceca25e7826d5035f4b33ae797a5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="statement-element-xmla"></a>Elemento Statement (XMLA)
  Contém uma consulta ou instrução a ser enviada usando o **Execute** método para uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Comentários  
 O **instrução** comando executa uma consulta ou instrução sobre o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte às linguagens a seguir:  
  
-   Linguagem MDX  
  
-   Extensões de mineração de dados (MDX)  
  
-   Um subconjunto de Linguagem SQL (SQL)  
  
## <a name="see-also"></a>Consulte também  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

