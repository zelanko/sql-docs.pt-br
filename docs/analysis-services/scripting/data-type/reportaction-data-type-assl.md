---
title: Tipo de dados ReportAction (ASSL) | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e99b4259600f9bd6c288826e452f1d763316b2e1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34033747"
---
# <a name="reportaction-data-type-assl"></a>Tipo de dados ReportAction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
## <a name="remarks"></a>Remarks  
 O servidor de relatório responde a solicitações baseadas na URL para relatórios. A ação de relatório é definida com um tipo *relatório*. São enviados os recursos e parâmetros ao servidor quando a ação é criada. O servidor expõe a ação como uma ação de conjunto de linhas de tipo.  
  
 O elemento correspondente no modelo de objeto Analysis Management Objects (AMO) é <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados XML de linguagem de script & #40; do Analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
