---
title: Elemento TuningOptions (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3050ce285cc98386f6de6278bedd2520cb39ba36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63061060"
---
# <a name="tuningoptions-element-dta"></a>Elemento TuningOptions (DTA)
  Contém as opções de ajuste de uma sessão de ajuste específica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Se usado, só poderá ser usado uma vez para cada elemento `DTAInput`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos filho**|`ReportSet`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `TuningLogTable`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `NumberOfEvents`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> [Elemento TuningTimeInMin &#40;DTA&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [Elemento StorageBoundInMB &#40;DTA&#41;](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `MaxColumnsInIndex`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `MinPercentageImprovement`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [Elemento TestServer &#40;DTA&#41;](server-element-dta.md)<br /><br /> [Elemento FeatureSet &#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Elemento Partitioning &#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [Elemento DropOnlyMode &#40;DTA&#41;](droponlymode-element-dta.md)<br /><br /> [Elemento KeepExisting &#40;DTA&#41;](keepexisting-element-dta.md)<br /><br /> [Elemento OnlineIndexOperation &#40;DTA&#41;](onlineindexoperation-element-dta.md)<br /><br /> [Elemento DatabaseToConnect &#40;DTA&#41;](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> `RetainShellDB`elementos. Para obter mais informações, consulte o esquema XML do [Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="example"></a>Exemplo  
 Para obter exemplos do `TuningOptions` elemento, consulte os [exemplos de arquivo de entrada XML &#40;DTA&#41;](xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
