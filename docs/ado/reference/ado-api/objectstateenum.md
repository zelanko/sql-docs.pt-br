---
description: ObjectStateEnum
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c387240e36225f03c8ba1287618ab59a98fb63c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443018"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Especifica se um objeto está aberto ou fechado, conectando-se a uma fonte de dados, executando um comando ou recuperando dados.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica que o objeto está fechado.|  
|**adStateOpen**|1|Indica que o objeto está aberto.|  
|**adStateConnecting**|2|Indica que o objeto está se conectando.|  
|**adStateExecuting**|4|Indica que o objeto está executando um comando.|  
|**adStateFetching**|8|Indica que as linhas do objeto estão sendo recuperadas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ObjectState. CLOSED|  
|AdoEnums. ObjectState. OPEN|  
|AdoEnums. ObjectState. CONECTAndo|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums. ObjectState. buscando|  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Propriedade State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)  
    :::column-end:::
    :::column:::
        [Propriedade State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)  
    :::column-end:::
:::row-end:::
