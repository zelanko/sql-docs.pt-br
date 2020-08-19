---
description: FieldEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b562d480cfbebefdee82703e0c953854de07d064
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443738"
---
# <a name="fieldenum"></a>FieldEnum
Especifica os campos especiais referenciados na coleção de [campos](../../../ado/reference/ado-api/fields-collection-ado.md) de um objeto de [registro](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="remarks"></a>Comentários  
 Essas constantes fornecem um "atalho" para acessar campos especiais associados a um **registro**. Recupere o objeto [Field](../../../ado/reference/ado-api/field-object.md) da coleção **Fields** e, em seguida, obtenha seu conteúdo com a propriedade [Value](../../../ado/reference/ado-api/value-property-ado.md) do objeto **Field** .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Faz referência ao campo que contém o objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) padrão associado a um **registro**.|  
|**adRecordURL**|-2|Faz referência ao campo que contém a cadeia de caracteres de URL absoluta para o **registro**atual.|
