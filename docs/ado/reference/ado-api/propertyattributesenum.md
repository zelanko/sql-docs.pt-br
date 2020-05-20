---
title: PropertyAttributesEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- PropertyAttributesEnum
helpviewer_keywords:
- PropertyAttributesEnum enumeration [ADO]
ms.assetid: 96a01955-a6b4-4cbf-9c73-52bcd1e9fb25
author: rothja
ms.author: jroth
ms.openlocfilehash: dcb17116d7332e9afb359a7dd47d69cb3eb75df4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759932"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Especifica os atributos de um objeto de [Propriedade](../../../ado/reference/ado-api/property-object-ado.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|Indica que a propriedade não é suportada pelo provedor.|  
|**adPropRequired**|1|Indica que o usuário deve especificar um valor para essa propriedade antes que a fonte de dados seja inicializada.|  
|**adPropOptional**|2|Indica que o usuário não precisa especificar um valor para essa propriedade antes que a fonte de dados seja inicializada.|  
|**adPropRead**|512|Indica que o usuário pode ler a propriedade.|  
|**adPropWrite**|1024|Indica que o usuário pode definir a propriedade.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
