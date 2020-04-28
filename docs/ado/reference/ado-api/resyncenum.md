---
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a872ee5f4af49d9fbe97621a5d2549fd9472202
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931235"
---
# <a name="resyncenum"></a>ResyncEnum
Especifica se os valores subjacentes são substituídos por uma chamada para [ressincronização](../../../ado/reference/ado-api/resync-method.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Padrão. Substitui dados e atualizações pendentes são canceladas.|  
|**adResyncUnderlyingValues**|1|Não substitui dados e atualizações pendentes não são canceladas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. Ressync. by|  
|AdoEnums. Ressync. UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)
