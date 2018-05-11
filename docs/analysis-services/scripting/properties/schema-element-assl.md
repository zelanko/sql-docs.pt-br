---
title: Elemento Schema (ASSL) | Microsoft Docs
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9822bbf6112673c5e03c382063af2ed017b8d5ca
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="schema-element-assl"></a>Elemento Schema (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contém o esquema da exibição da fonte de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Esquema|  
|Valor padrão|Nenhuma|  
|Cardinalidade|1-1: elemento obrigatório que ocorre apenas uma única vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elemento pai|[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|  
|Elementos filho|Nenhuma|  
  
## <a name="remarks"></a>Remarks  
 O **esquema** é representada usando o formato de linguagem de definição de esquema XML (XSD) de conjuntos de dados de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] do .NET Framework, com algumas extensões para DataSets e outras específicas para esse uso na definição de dados Language (DDL). DataSets define um mapeamento flexível de XSD em um esquema relacional, mas retorna XSD em uma forma mais canônica. Somente essa forma canônica é válida nas fontes de dados.  
  
 O elemento que corresponde ao pai do **esquema** no objeto Analysis Management Objects (AMO) o modelo é <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
