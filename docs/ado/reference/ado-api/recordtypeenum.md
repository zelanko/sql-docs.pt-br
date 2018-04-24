---
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 28821a53dd58ecd757588a910bc1cda46121532c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica o tipo de [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica um *simples* registro (não tem nós filhos).|  
|**adCollectionRecord**|1|Indica um *coleção* registro (contém nós filho).|  
|**adRecordUnknown**|-1|Indica que o tipo deste **registro** é desconhecido.|  
|**adStructDoc**|2|Indica um especial de tipo de *coleção* estruturado de registro que representa COM documentos.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
