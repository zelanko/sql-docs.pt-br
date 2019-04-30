---
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 204ffb54eb0a48f55d4ec1974b123ed4a0e430be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192843"
---
# <a name="fieldenum"></a>FieldEnum
Especifica os campos especiais referenciados em uma [registro](../../../ado/reference/ado-api/record-object-ado.md) do objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção.  
  
## <a name="remarks"></a>Comentários  
 Essas constantes fornecem um "atalho" para acessar campos especiais associados a um **registro**. Recuperar o [campo](../../../ado/reference/ado-api/field-object.md) objeto o **campos** coleção e, em seguida, obter seu conteúdo com o **campo** do objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Faz referência ao campo que contém o padrão [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto associado a um **registro**.|  
|**adRecordURL**|-2|Faz referência ao campo que contém a cadeia de caracteres de URL absoluta para o atual **registro**.|
