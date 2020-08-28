---
description: RecordTypeEnum
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ded4106b770ff62edd4b79401885ee5ce3101798
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989657"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Especifica o tipo de objeto de [registro](./record-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica um registro *simples* (não contém nós filho).|  
|**adCollectionRecord**|1|Indica um registro de *coleção* (contém nós filho).|  
|**adRecordUnknown**|-1|Indica que o tipo desse **registro** é desconhecido.|  
|**adStructDoc**|2|Indica um tipo especial de registro de *coleção* que representa documentos estruturados com.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade RecordType (ADO)](./recordtype-property-ado.md)