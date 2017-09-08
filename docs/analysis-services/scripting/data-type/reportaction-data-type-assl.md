---
title: Tipo de dados ReportAction (ASSL) | Microsoft Docs
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
- ReportAction Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ReportAction
helpviewer_keywords:
- ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22ee650d376fc545a0dfc63b5173f5d48498b97a
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="reportaction-data-type-assl"></a>Tipo de dados ReportAction (ASSL)
  Define um tipo de dados derivado que representa uma ação que gera um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] relatório.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<ReportAction>  
   <!-- The following elements extend Action -->  
   <ReportServer>...</ReportServer>  
   <Path>...</Path>  
   <ReportParameters>...</ReportParameters>  
   <ReportFormatParameters>...</ReportFormatParameters>  
</ReportAction>  
```  
  
## <a name="data-type-characteristics"></a>Características do tipo de dados  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Tipos de dados base|[Ação](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|Tipos de dados derivados|Nenhuma|  
  
## <a name="data-type-relationships"></a>Relação do tipo de dados  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|Nenhuma|  
|Elementos filho|[Caminho](../../../analysis-services/scripting/properties/path-element-assl.md), [ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md), [ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md), [ReportServer](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|  
|Elementos derivados|[Ação](../../../analysis-services/scripting/objects/action-element-assl.md) ([ações](../../../analysis-services/scripting/collections/actions-element-assl.md) coleção de [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) ou [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentários  
 O servidor de relatório responde a solicitações baseadas na URL para relatórios. A ação de relatório é definida com um tipo *relatório*. São enviados os recursos e parâmetros ao servidor quando a ação é criada. O servidor expõe a ação como uma ação de conjunto de linhas de tipo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script &#40; do Analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
