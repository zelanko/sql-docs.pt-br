---
title: Elemento Statement (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Statement Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Statement
- microsoft.xml.analysis.statement
- urn:schemas-microsoft-com:xml-analysis#Statement
helpviewer_keywords: Statement command
ms.assetid: bfedc03c-d476-4d55-b5fd-36169f01351a
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 141c3ca99116720a594785496a326386e410c4b1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="statement-element-xmla"></a>Elemento Statement (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contém uma consulta ou instrução a ser enviada usando o **Execute** método para uma instância de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Cadeia de caracteres|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|Nenhum|  
  
## <a name="remarks"></a>Remarks  
 O **instrução** comando executa uma consulta ou instrução sobre o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte às linguagens a seguir:  
  
-   Linguagem MDX  
  
-   Extensões de mineração de dados (MDX)  
  
-   Um subconjunto de Linguagem SQL (SQL)  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
