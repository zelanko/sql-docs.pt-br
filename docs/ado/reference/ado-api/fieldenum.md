---
title: FieldEnum | Microsoft Docs
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
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d00710700dae843695e4d1f970e2266f1113b54b
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="fieldenum"></a>FieldEnum
Especifica os campos especiais referenciados em uma [registro](../../../ado/reference/ado-api/record-object-ado.md) do objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
## <a name="remarks"></a>Remarks  
 Constantes fornecem um "atalho" para acessar campos especiais associados a um **registro**. Recuperar o [campo](../../../ado/reference/ado-api/field-object.md) de objeto o **campos** coleção e, em seguida, obter seu conteúdo com o **campo** do objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Faz referência ao campo que contém o padrão [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto associado a um **registro**.|  
|**adRecordURL**|-2|Faz referência ao campo que contém a cadeia de caracteres de URL absoluta atual **registro**.|
