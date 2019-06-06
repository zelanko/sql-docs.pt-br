---
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: eb33d68fcaf32fa92ae9a65e2ca216a86792a1be
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711775"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica o tipo de [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica um *simples* registro (não contém nós filho).|  
|**adCollectionRecord**|1|Indica um *coleção* registro (contém nós filho).|  
|**adRecordUnknown**|-1|Indica que o tipo deste **registro** é desconhecido.|  
|**adStructDoc**|2|Indica um especial de tipo de *coleção* estruturado de registro que representa COM documentos.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
