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
ms.openlocfilehash: 6caaf8db2b8f2e19060f6e9766bb3650ac9b5400
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="fieldenum"></a>FieldEnum
Especifica os campos especiais referenciados em uma [registro](../../../ado/reference/ado-api/record-object-ado.md) do objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
## <a name="remarks"></a>Remarks  
 Constantes fornecem um "atalho" para acessar campos especiais associados a um **registro**. Recuperar o [campo](../../../ado/reference/ado-api/field-object.md) de objeto o **campos** coleção e, em seguida, obter seu conteúdo com o **campo** do objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Faz referência ao campo que contém o padrão [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto associado a um **registro**.|  
|**adRecordURL**|-2|Faz referência ao campo que contém a cadeia de caracteres de URL absoluta atual **registro**.|
