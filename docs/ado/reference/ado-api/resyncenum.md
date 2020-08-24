---
description: ResyncEnum
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: rothja
ms.author: jroth
ms.openlocfilehash: addaaa07b14b88ed7d72714ba8698da1f2ef2ac9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777635"
---
# <a name="resyncenum"></a>ResyncEnum
Especifica se os valores subjacentes são substituídos por uma chamada para [ressincronização](./resync-method.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Padrão. Substitui dados e atualizações pendentes são canceladas.|  
|**adResyncUnderlyingValues**|1|Não substitui dados e atualizações pendentes não são canceladas.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. Ressync. by|  
|AdoEnums. Ressync. UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Resync](./resync-method.md)