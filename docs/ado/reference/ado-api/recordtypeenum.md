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
manager: craigg
ms.openlocfilehash: 195f76043cf65801289d081e497e28a41aff3209
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761434"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica o tipo de [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica um *simples* registro (não contém nós filho).|  
|**adCollectionRecord**|1|Indica um *coleção* registro (contém nós filho).|  
|**adRecordUnknown**|-1|Indica que o tipo deste **registro** é desconhecido.|  
|**adStructDoc**|2|Indica um especial de tipo de *coleção* estruturado de registro que representa COM documentos.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade RecordType (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)
