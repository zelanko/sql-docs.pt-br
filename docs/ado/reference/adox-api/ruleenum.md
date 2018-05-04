---
title: RuleEnum | Microsoft Docs
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
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 24fb427caf5d398099af5aa812280e8b45836575
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ruleenum"></a>RuleEnum
Especifica a regra para seguir quando um [chave](../../../ado/reference/adox-api/key-object-adox.md) é excluído.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Alterações em cascata.|  
|**adRINone**|0|Padrão. Nenhuma ação é tomada.|  
|**adRISetDefault**|3|Valor de chave estrangeira é definida como o padrão.|  
|**adRISetNull**|2|Valor de chave estrangeira é definida como null.|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade DeleteRule (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
