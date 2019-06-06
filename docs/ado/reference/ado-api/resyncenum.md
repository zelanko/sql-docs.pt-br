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
manager: jroth
ms.openlocfilehash: 2bc43e772ab8f1e330d393461944cb2ecd585149
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711569"
---
# <a name="resyncenum"></a>ResyncEnum
Especifica se os valores subjacentes são substituídos por uma chamada para [ressincronizar](../../../ado/reference/ado-api/resync-method.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Padrão. Substitui os dados e as atualizações pendentes serão canceladas.|  
|**adResyncUnderlyingValues**|1|Não substituir os dados e as atualizações pendentes não serão canceladas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Resync.ALLVALUES|  
|AdoEnums.Resync.UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método Resync](../../../ado/reference/ado-api/resync-method.md)
