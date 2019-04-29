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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0bb38a73008d86144751ee324eb442bf711d65a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027677"
---
# <a name="propertyattributesenum"></a>PropertyAttributesEnum
Especifica os atributos de uma [propriedade](../../../ado/reference/ado-api/property-object-ado.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adPropNotSupported**|0|Indica que a propriedade não é suportada pelo provedor.|  
|**adPropRequired**|1|Indica que o usuário deve especificar um valor para essa propriedade antes que a fonte de dados seja inicializada.|  
|**adPropOptional**|2|Indica que o usuário não precisa especificar um valor para essa propriedade antes que a fonte de dados seja inicializada.|  
|**adPropRead**|512|Indica que o usuário pode ler a propriedade.|  
|**adPropWrite**|1024|Indica que o usuário pode definir a propriedade.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.PropertyAttributes.NOTSUPPORTED|  
|AdoEnums.PropertyAttributes.REQUIRED|  
|AdoEnums.PropertyAttributes.OPTIONAL|  
|AdoEnums.PropertyAttributes.READ|  
|AdoEnums.PropertyAttributes.WRITE|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
