---
title: Elemento MasterDatasourceID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MasterDatasourceID Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MasterDatasourceID
helpviewer_keywords:
- MasterDatasourceID element
ms.assetid: a9cbd3a9-581f-4a08-93d8-e1eea8757ce9
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 868bd8d56553f976915728c3ef59260f8c338cf0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="masterdatasourceid-element-assl"></a>Elemento MasterDatasourceID (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém o identificador de fonte de dados mestre (ID) para um [banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Database>  
   ...  
   <MasterDatasourceID>...</MasterDatasourceID>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|String|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-1: elemento obrigatório que pode ocorrer apenas uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Banco de dados](../../../analysis-services/scripting/objects/database-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 Para bancos de dados em instâncias remotas do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contêm partições remotas, o **MasterDatasourceID** elemento contém a ID da fonte de dados usada para identificar o mestre de fonte de dados instância de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que gerencia as partições remotas.  
  
 O elemento que corresponde ao pai do **MasterDatasourceID** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.Database>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
