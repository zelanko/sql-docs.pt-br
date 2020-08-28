---
description: ResyncEnum
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 0c98c0b0bae307f57e5a77c7ca4ac6b473f4d149
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989457"
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